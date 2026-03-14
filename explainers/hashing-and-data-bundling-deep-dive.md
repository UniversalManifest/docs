# Hashing, Caching, and Data Bundling — Complete Deep Dive

**Summary:** Universal Manifest uses a layered integrity and performance architecture. SHA-256 content hashing generates ETags for HTTP conditional revalidation. Ed25519 signatures over JCS-canonicalized payloads provide cryptographic tamper detection. The pointer-first architecture keeps manifests lightweight (1-3 KB typical) by referencing external resources rather than embedding them. HTTP caching with short TTLs (60 seconds) and ETag/304 support ensures freshness without excessive resolver load. Content-addressed identifiers (CIDs) are deliberately deferred -- the UMID is a stable identity, not a content hash, and this separation is a design strength. For constrained transports (NFC, QR, Bluetooth), CBOR-LD binary encoding is a future opt-in profile that could achieve 60%+ compression over JSON.

---

## 1. How Hashing Works Today

Universal Manifest uses hashing in two distinct roles: transport-layer integrity (ETags) and application-layer integrity (signatures). These serve different purposes and operate at different layers.

### Transport layer: SHA-256 ETags

The myum.net resolver computes SHA-256 hashes of response bodies to generate weak ETags. The process:

1. The manifest JSON payload is serialized as a UTF-8 string
2. SHA-256 is computed using the Web Crypto API (`crypto.subtle.digest`)
3. The digest is base64url-encoded
4. The result is wrapped as a weak ETag: `W/"sha256-{base64url-digest}"`

This ETag is returned with every 200 OK response. When a consumer sends `If-None-Match` with a previously received ETag, the resolver returns 304 Not Modified if the content has not changed, saving bandwidth. The hash is computed per-request from the response body -- it is not pre-stored.

**What SHA-256 ETags provide:**
- Bandwidth savings for polling consumers
- Implicit content verification (the hash covers the exact bytes delivered)
- Standard HTTP cache revalidation semantics

**What SHA-256 ETags do not provide:**
- Issuer authentication (anyone could produce the same hash)
- Tamper detection across the full lifecycle (ETags only cover the resolver-to-consumer hop)
- Content addressing (the ETag is ephemeral, not a stable identifier)

### Application layer: Ed25519 + JCS signatures

The v0.2 signature profile provides end-to-end integrity from issuer to consumer, independent of the transport.

**Signing input construction:**
1. Start with the complete manifest JSON object
2. Remove the `signature` property entirely
3. Canonicalize the remaining JSON using JCS (RFC 8785) -- keys sorted lexicographically, no whitespace, deterministic number serialization
4. Encode the canonical form as UTF-8 bytes
5. Sign with Ed25519

**Signature coverage:**
Everything in the manifest is signed except the signature block itself: `@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`, all facets, all claims, all consents, all devices, all pointers. Changing any byte in any of these fields invalidates the signature.

**Why JCS, not RDFC-1.0:**
UM chose JCS (RFC 8785) for canonicalization rather than W3C's RDF Dataset Canonicalization (RDFC-1.0). JCS operates on JSON directly -- sorted keys, deterministic serialization -- without requiring a full RDF processing pipeline. This keeps the signing/verification path simple: parse JSON, remove signature, sort keys, serialize, hash, verify. No JSON-LD expansion, no N-Quads serialization, no blank node relabeling. The trade-off is that JCS canonicalization is JSON-format-specific and would not survive a format conversion (e.g., JSON to CBOR-LD) without re-signing.

**Why Ed25519:**
- 64-byte signatures (compact for portable documents)
- Fast verification (important for constrained consumers)
- No curve parameter negotiation (single fixed curve)
- Compatible with X25519 key agreement via birational mapping (relevant for the JWE per-facet encryption proposed in the facet encryption deep dive)
- Widely implemented across all major languages and platforms

---

## 2. The Pointer-First Architecture

The most important optimization in Universal Manifest is not a hashing algorithm or a compression scheme -- it is the decision to reference external data rather than embed it. This is the pointer-first architecture.

### How pointers work

A pointer is a named URI reference to an external resource:

```json
{
  "pointers": [
    {
      "@type": "um:Pointer",
      "rel": "canonical",
      "href": "https://example.pod.provider/bob/profile.jsonld"
    },
    {
      "@type": "um:Pointer",
      "rel": "avatar",
      "href": "https://cdn.example.com/avatars/bob/mesh.glb"
    }
  ]
}
```

The manifest carries the reference, not the data. A 50 MB avatar mesh is a 60-byte pointer. A full social graph stored on a Solid Pod is a 70-byte pointer. The manifest stays at 1-3 KB regardless of how much data it references.

### Why pointers are the primary optimization

**Size budget:** The UM specification recommends a 1 MB total manifest size. In practice, well-designed manifests are 1-3 KB. Pointers are why. Without them, embedding avatar assets, social graphs, credential bundles, and venue policies would push manifests into megabyte territory.

**Freshness:** Embedded data goes stale the moment the manifest is issued. A pointer to an authoritative source ensures the consumer always fetches the current version when they follow the pointer. The pointer URI is covered by the manifest signature, so the consumer can trust that the issuer intended this specific source -- but the content at that source can be updated without re-issuing the manifest.

**Access control:** External resources can enforce their own access controls independently. A Solid Pod pointer lets the Pod's ACL system gate access. An API endpoint pointer lets the API server enforce authentication. The manifest does not need to carry access control for every resource it references.

**Transport agnosticism:** The manifest travels by whatever transport works -- QR code, NFC, Bluetooth, HTTP, metaverse portal. Keeping it small means it works on every transport. Large embedded data would break size-constrained transports.

### What pointers do not provide today

**Content integrity for pointer targets.** The pointer URI is signed (changing it breaks the manifest signature), but the content at that URI is not hash-bound. If the external resource changes, the consumer has no way to verify that it matches what the issuer intended. This is a genuine gap that content hashing could address (see Section 5).

**Offline access.** Following a pointer requires network access. A consumer with a cached manifest but no connectivity cannot fetch pointer targets. The manifest itself is offline-tolerant (it is self-contained JSON), but the resources it points to are not.

---

## 3. HTTP Caching and Conditional Requests

The resolver implements a deliberate caching strategy optimized for the UM access pattern: frequent reads, infrequent writes, and freshness-critical revocations.

### Cache-Control: public, max-age=60

Every successful resolution (200 OK or 307 Temporary Redirect) includes `Cache-Control: public, max-age=60`. This means:

- **public:** Any intermediary (CDN, shared proxy) may cache the response
- **max-age=60:** The response is considered fresh for 60 seconds

The 60-second TTL is deliberately short. It balances two concerns:

1. **Performance:** Consumers that poll the same UMID multiple times per minute hit the cache instead of the resolver
2. **Freshness:** When a manifest is updated or revoked, the stale cached version expires within 60 seconds

Error responses (400, 404, 405, 410, 500) use `Cache-Control: no-store` -- errors are not cached, so a consumer that retries immediately gets a fresh lookup.

### ETag and 304 Not Modified

The resolver generates a weak ETag for every 200 response:

```
ETag: W/"sha256-{base64url-digest-of-response-body}"
```

When a consumer sends `If-None-Match: W/"sha256-..."` and the manifest has not changed, the resolver returns:

```
304 Not Modified
(no body -- same headers, same cache directives)
```

This saves the bandwidth of re-downloading the manifest body. For a typical 2 KB manifest, the 304 response is under 300 bytes. For consumers that poll every 60 seconds, this reduces bandwidth by 85%+ when the manifest has not changed.

### The two TTL layers

There are two distinct TTL concepts in UM, and they must not be confused:

1. **HTTP TTL** (`Cache-Control: max-age=60`): Controls transport-layer caching. After 60 seconds, the cached response is stale and the consumer should revalidate. This is the resolver's domain.

2. **Manifest TTL** (`expiresAt` field): Controls application-layer validity. After this timestamp, the manifest is invalid and must be rejected regardless of HTTP caching. This is the consumer's responsibility.

The specification is explicit: "Consumers MUST enforce manifest `expiresAt` (TTL) regardless of HTTP caching." A consumer that receives a manifest via a CDN cache hit must still check `expiresAt`. HTTP caching is a performance optimization; manifest TTL is a trust boundary.

### SLO target

The operational SLO for ETag revalidation is >= 99.5% success rate for 304 Not Modified responses. This is monitored by the synthetic monitoring system.

---

## 4. What UM Does Not Hash (And Why)

Several hashing and content-addressing technologies are deliberately absent from the current specification. Understanding why is as important as understanding what is present.

### Content Identifiers (CIDs) are deferred

CIDs (IPFS/IPLD Content Identifiers) are self-describing, content-addressed labels. A CID encodes both the hash algorithm and the hash digest, creating a universally verifiable content address. Two identical payloads always produce the same CID.

**Why UM defers CIDs:**

The UMID is a **stable identity**, not a content hash. A UMID (`urn:uuid:9b1d0e3f-...`) persists across manifest updates. The issuer updates the manifest, re-signs it, and publishes it under the same UMID. Consumers who resolve the UMID get the latest version.

A CID would change every time the manifest content changes. This is the fundamental tension: CIDs identify content, UMIDs identify the entity that the manifest describes. Both are useful, but they serve different purposes and must not be conflated.

**Where CIDs could add value:**

- **Immutable snapshots:** A CID of a specific manifest version would create a tamper-evident snapshot. The resolver could store `UMID -> [current CID, CID history]` alongside the current mapping.
- **Pointer integrity:** A CID or Multihash digest alongside a pointer URI would let consumers verify that the external resource matches what the issuer intended (see Section 5).
- **Deduplication:** Manifests that share identical facets could reference the same CID, reducing storage in systems that cache many manifests.

**Current position:** CIDs are not rejected -- they are deferred until a concrete use case justifies the added complexity. The pointer-first architecture and ETag-based caching solve the immediate performance and integrity needs.

### No content hashing for pointer targets

When a consumer follows a pointer to an external resource, there is no hash in the manifest to verify the resource against. The pointer URI is signed (changing the URI breaks the manifest signature), but the content at the URI is not hash-bound.

This is a known gap. Two approaches could address it:

1. **digestMultibase (W3C):** Add a `digestMultibase` property to pointer objects, containing a Multibase-encoded Multihash of the expected content. This is the approach used in W3C Verifiable Credential Data Integrity for `@context` integrity.

2. **Hashlink-style URIs:** Encode the hash directly in the pointer URI using the Hashlink parameterized format: `https://example.com/resource?hl=zQm...`. This approach is conceptually clean but based on an expired IETF draft.

The `digestMultibase` approach is recommended if this gap is addressed, as it aligns with the W3C VC ecosystem and does not require modifying the pointer URI format.

### No binary encoding (yet)

UM manifests are JSON-LD -- human-readable text. Binary formats like CBOR-LD could reduce manifest size by 60%+ through semantic compression (replacing JSON-LD terms with integer codes derived from the `@context`). COSE (the CBOR analog of JOSE) could provide binary signing.

**Why not now:**

- JSON-LD is universally parseable. Every language, every platform, every tool can handle JSON.
- Human readability is a feature. Developers can inspect manifests with `curl | jq`.
- The pointer-first architecture already keeps manifests small (1-3 KB). Binary encoding would save 1-2 KB -- meaningful for NFC/QR but not critical for HTTP.
- CBOR-LD is a W3C Experimental Draft with limited implementations (JS, Java). Relying on it as a primary format would be premature.

**Where binary encoding would help:**

- **NFC tap:** NFC NDEF payloads are limited. A 800-byte CBOR-LD manifest fits; a 2 KB JSON-LD manifest may not.
- **QR codes:** Smaller payloads mean higher error correction and smaller physical QR sizes.
- **Bluetooth beacons:** BLE advertisement payloads are extremely constrained.
- **Batch processing:** Systems processing millions of manifests would benefit from smaller wire format and faster parsing.

**Current position:** CBOR-LD is a future opt-in profile, not a replacement for JSON-LD. If added, the specification would define deterministic round-tripping between JSON-LD and CBOR-LD so both formats represent the same logical document.

---

## 5. Content Integrity for External Resources

This section addresses the genuine gap identified in Section 2: pointer targets have no hash-bound integrity verification.

### The problem

A manifest contains a pointer:
```json
{
  "@type": "um:Pointer",
  "rel": "avatar",
  "href": "https://cdn.example.com/avatars/bob/mesh.glb"
}
```

The URI `https://cdn.example.com/avatars/bob/mesh.glb` is covered by the manifest signature. If someone changes the URI to point to a different resource, the signature breaks. But if someone changes the content at that URI (compromises the CDN, man-in-the-middles the download), the consumer has no way to detect the substitution.

### Proposed solution: digestMultibase on pointers

Add an optional `digestMultibase` property to pointer objects:

```json
{
  "@type": "um:Pointer",
  "rel": "avatar",
  "href": "https://cdn.example.com/avatars/bob/mesh.glb",
  "digestMultibase": "zQmYtUc4iTCbbfVSDNKvtQqrfyeyzSma1ztOnLSTfp2Fn9H"
}
```

The `digestMultibase` value is a Multibase-encoded Multihash:
- `z` prefix indicates base58btc encoding
- The decoded value starts with the Multihash header identifying the hash algorithm (e.g., SHA-256) and digest length
- The remaining bytes are the digest

**Consumer verification flow:**
1. Follow the pointer URI and download the resource
2. Compute the Multihash of the downloaded content using the algorithm indicated in the `digestMultibase` header
3. Compare the computed digest with the `digestMultibase` value
4. If they match, the resource is authentic. If not, reject or flag.

**Advantages:**
- Aligns with W3C VC Data Integrity's `digestMultibase` property
- Self-describing hash format (Multihash) future-proofs against algorithm changes
- Optional -- consumers that do not understand `digestMultibase` safely ignore it (forward compatibility)
- The `digestMultibase` value is covered by the manifest signature, so it cannot be tampered with independently

**Limitations:**
- The digest binds the pointer to a specific version of the external resource. If the resource is legitimately updated, the manifest must be re-issued with a new digest and signature.
- This creates a coupling between manifest freshness and resource freshness that the pointer-first architecture was designed to avoid.
- For resources that change frequently (real-time social graphs, live avatar states), a static digest is not appropriate. The pointer without a digest is the correct model for dynamic resources.

**Status:** Proposed. Not yet in the specification. Would be defined as an optional extension to the pointer schema.

### Context integrity

The `@context` URLs in UM manifests reference JSON-LD context documents that define the semantic meaning of terms in the manifest. If a context document is tampered with, the semantic interpretation of the entire manifest changes.

Adding `digestMultibase` to the `@context` array (as W3C VC Data Integrity does) would pin the context to a specific version:

```json
{
  "@context": [
    {
      "@id": "https://universalmanifest.net/context/v0.2",
      "digestMultibase": "zQm..."
    }
  ]
}
```

This is a defense against context-manipulation attacks where an attacker serves a modified context file to change the meaning of manifest properties.

---

## 6. Comparison to Other Systems

| System | Content Hashing | Signing | Caching | Bundling |
|--------|----------------|---------|---------|----------|
| **Universal Manifest** | SHA-256 ETags (transport); no content addressing (by design) | Ed25519 + JCS (application layer) | HTTP max-age=60 + ETag/304 | JSON-LD with pointers to external resources |
| **W3C Verifiable Credentials** | digestMultibase for context integrity | Data Integrity proofs (EdDSA, ECDSA, BBS+) or JOSE/COSE envelopes | Not specified (VC is a document, not a service) | JSON-LD or JWT; claims embedded, not pointed |
| **IPFS/IPLD** | CID (Multihash) for everything | None built in (layer above) | Content-addressed (immutable by definition) | Merkle DAG; data chunked and linked by CID |
| **DIDComm v2** | None | JWS for signed messages | Not applicable (messaging, not caching) | JWE layers; entire messages encrypted |
| **Solid Pods** | None at document level | WebID-TLS or DPoP | HTTP standard caching | RDF/Turtle; linked data in pods |
| **DNS** | DNSSEC (RSA/ECDSA) | DNSSEC chain of trust | TTL per record (seconds to days) | Zone files; records not self-describing |
| **Certificate Transparency** | SHA-256 Merkle tree | Ed25519/ECDSA SCTs | Append-only log (immutable) | Merkle tree of certificates |

### Key differentiator: UMID stability vs. content addressing

Most content-addressed systems (IPFS, git, Certificate Transparency) use the hash as the identifier. Changing the content changes the identifier. This is correct for immutable artifacts.

UM uses the UMID as a stable identifier that persists across content changes. The UMID is the entity's address; the manifest content at that address evolves. This is correct for living identity documents that change as the subject updates their profile, rotates credentials, or modifies consent settings.

The resolver bridges these models: it maps stable UMIDs to current content, with ETags providing content hashing at the transport layer and signatures providing integrity at the application layer.

---

## 7. Future Considerations

### Merkle history for manifests

A Merkle tree of manifest versions would create an auditable, tamper-evident history for each UMID. Each leaf would be the hash of a manifest snapshot. The root hash would commit to the entire version history.

**Use cases:**
- Audit trail: when did the issuer change a consent setting? When was a facet added?
- Dispute resolution: prove that a specific manifest version existed at a specific time
- Transparency: public verifiability that the resolver has not retroactively altered history

**Trade-off:** This adds storage and computation complexity to the resolver. The current resolver is stateless (KV lookup, no history). Adding history tracking changes its architectural character. This should be an optional extension, not a core requirement.

### Batch revocation with status lists

For ecosystems with many manifests, checking individual revocation status (HTTP 410 per UMID) does not scale. The W3C Bitstring Status List (Candidate Recommendation) uses a compressed bitstring where each bit represents one credential's revocation status. A single 16 KB download covers 131,072 credentials.

UM could adopt a similar model: a status list URL published by the resolver, where each bit position maps to a registered UMID. Consumers would download the status list periodically and check their UMID's bit, rather than making individual resolver calls.

**Trade-off:** Bitstring status lists are designed for issuers who control large credential populations. The UM model (many independent issuers, each with few manifests) may not benefit as much. Individual 410 checks with HTTP caching may remain more practical.

### CBOR-LD + COSE as an optional profile

For constrained transports, a CBOR-LD encoding with COSE_Sign1 signing would provide:
- 60%+ size reduction over JSON-LD (semantic compression)
- Binary signing without base64url overhead
- Alignment with EU Digital Identity Wallet (EUDI) and ISO mDL ecosystems

This would be defined as an optional profile alongside the primary JSON-LD format. Both formats would represent the same logical document, with deterministic conversion between them. Consumers would accept either format based on their capabilities.

**Prerequisite:** CBOR-LD must reach W3C Recommendation status and have production-grade implementations in at least three languages before UM adopts it as a profile.

---

## 8. What Is Revolutionary

### Separation of identity from content

Most identity systems either use content-addressed identifiers (which break when content changes) or use opaque identifiers with no integrity guarantees (which provide no tamper detection). UM provides both: a stable UMID for identity persistence and Ed25519 signatures for content integrity. The resolver bridges them with SHA-256 ETags for transport efficiency.

### Pointer-first as an optimization strategy

Traditional portable document formats embed everything. A PDF contains all fonts, images, and text. A W3C Verifiable Credential embeds all claims. UM inverts this: the manifest is a lightweight envelope of references. The data lives where it naturally belongs -- the avatar on a CDN, the social graph on a Solid Pod, the credentials at an issuer's endpoint. The manifest connects them with signed pointers.

This is not just a size optimization. It is an architectural decision that preserves the autonomy of every system the manifest references. No system needs to surrender its data to the manifest. The manifest just makes it findable.

### Layered integrity without over-engineering

UM achieves integrity at three levels without requiring exotic cryptography or complex infrastructure:

1. **Transport integrity:** SHA-256 ETags and HTTP caching (standard web infrastructure)
2. **Document integrity:** Ed25519 + JCS signatures (compact, fast, widely implemented)
3. **Pointer integrity:** URI signing via signature coverage (the pointer URI is part of the signed payload)

Each layer uses established, well-understood technology. The stack avoids the complexity of Merkle trees, content-addressed storage, or zero-knowledge proofs -- not because these are bad, but because the simpler approach is sufficient for the current use cases.

---

## 9. The Path Forward

### Immediate (v0.2 current)
- SHA-256 ETags with 304 conditional revalidation: **implemented**
- Ed25519 + JCS signing: **implemented**
- HTTP caching with 60s max-age: **implemented**
- Pointer-first architecture: **implemented**

### Near-term (research-first)
- `digestMultibase` for pointer integrity: **proposed, not yet in spec**
- Context integrity via `digestMultibase` on `@context`: **proposed, not yet in spec**
- CID snapshots alongside UMIDs: **deferred, no concrete use case yet**

### Future (contingent on ecosystem maturity)
- CBOR-LD + COSE binary profile: **contingent on CBOR-LD reaching W3C Recommendation**
- Merkle history for manifest audit trails: **conceptual, requires resolver architecture change**
- Bitstring status lists for batch revocation: **contingent on UM ecosystem scale**

### Design principles that govern all additions

1. **Internal decisions are source of truth.** External standards inform but do not override UM's architectural choices.
2. **Pointer-first is the primary optimization.** Any addition that weakens the pointer model (by encouraging embedding or coupling manifest freshness to resource freshness) must justify itself.
3. **UMID is identity, not content.** Content-addressing is a tool, not a replacement for stable identifiers.
4. **Simple beats clever.** SHA-256 + Ed25519 + HTTP caching solve the problem. Exotic alternatives must demonstrate concrete superiority, not just theoretical elegance.
5. **Opt-in profiles, not mandates.** New encoding formats, hash schemes, or signing mechanisms are optional profiles. The base specification remains JSON-LD with Ed25519 + JCS.

---

## NotebookLM Video Brief

### L3-11: Hashing, Caching, and Data Bundling Deep Dive
**Level:** 3 | **Length:** 6 min
**Audience:** Engineers, architects, and performance-minded evaluators wanting the complete integrity and optimization story.

```
FOCUS: How Universal Manifest achieves integrity and performance through three layers: SHA-256 content hashing for HTTP ETag generation and conditional revalidation (304 Not Modified), Ed25519 signatures over JCS-canonicalized payloads for end-to-end tamper detection, and the pointer-first architecture that keeps manifests at 1-3 KB by referencing external resources rather than embedding them. The two TTL layers: HTTP max-age=60 for transport caching and manifest expiresAt for application-level validity. Why content-addressed identifiers (CIDs) are deliberately deferred -- the UMID is a stable identity that persists across content changes, not a content hash that breaks on every update. The genuine gap: pointer targets have no hash-bound integrity verification today, and digestMultibase is the proposed solution. Future considerations: CBOR-LD binary encoding for constrained transports (NFC, QR, Bluetooth) achieving 60%+ compression, Merkle history for audit trails, and bitstring status lists for batch revocation. What is revolutionary: the separation of identity from content, pointer-first as an optimization strategy, and layered integrity without over-engineering.

DO NOT COVER: Do not explain the resolver flow in detail -- that is L3-05-DEEP. Do not cover facet encryption or consent mechanics -- those are L3-10 and L3-03. Do not discuss specific integration lanes or portaling. Do not mention implementation code, TypeScript, Cloudflare Workers, or deployment infrastructure. Stay at the specification architecture level. Do not mention PeerMesh or any runtime.

WHY THIS EXISTS: The definitive explanation of how UM achieves data integrity and performance through hashing, caching, pointer-first architecture, and deliberate technology choices -- covering what is implemented, what is proposed, and what is deferred.
```
