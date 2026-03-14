# The myum.net Resolver -- Complete Deep Dive

**Summary:** The myum.net resolver is a thin, stateless lookup service that maps Universal Manifest Identifiers (UMIDs) to canonical manifest sources. It is not a database, not a storage layer, and not an identity provider -- it is a public registry of pointers. When a consumer sends a UMID to myum.net, the resolver returns either a 307 redirect to the manifest's canonical source, a 200 with the manifest payload, a 404 for unknown UMIDs, or a 410 for revoked ones. The manifest issuer always owns the data; the resolver just connects lookups to sources. This architecture means zero vendor lock-in, offline-tolerant operation after initial fetch, and embedded consent that travels with the document. Anyone can build a conformant resolver -- myum.net is the reference deployment of a spec-level concept.

---

## 1. What Is the Resolver?

The myum.net resolver is a lookup service. You give it a Universal Manifest Identifier (UMID), and it tells you where to find the manifest. That is the entire job.

It is **not** a database. It does not store manifest content in the way a traditional data store would. It stores mappings -- tiny records that say "this UMID lives at this URL" or "this UMID's manifest payload is this JSON document."

It is **not** an identity provider. It does not authenticate users, issue tokens, manage sessions, or grant permissions. It has no concept of "who is asking" -- every request is treated the same way.

It is **not** a storage layer. The canonical manifest lives wherever the issuer published it: their own server, a Solid Pod, IPFS, a CDN, a static file host. The resolver is a routing layer that connects UMID lookups to those sources.

The best analogy is DNS. DNS resolves domain names to IP addresses. The myum.net resolver resolves UMIDs to manifest locations. Just as DNS does not host websites, the resolver does not host manifests. Just as DNS is a public utility that anyone can query, the resolver is a public utility that any system with a UMID can query.

The resolver is defined at the specification level, not the product level. myum.net is the reference deployment -- a working, production-grade instance that proves the concept. But the Universal Manifest specification does not mandate using myum.net. Any organization can run a conformant resolver for their own ecosystem, just as anyone can run their own DNS server.

### What the resolver does

- Accepts a UMID via HTTP GET request
- Looks up the UMID in its registry (Cloudflare KV)
- Returns the result: redirect to canonical source, manifest payload, not-found, or revoked
- Adds standard headers for contract versioning, caching, CORS, and provenance
- Serves a well-known descriptor documenting its own behavior
- Provides a health endpoint for operational monitoring

### What the resolver does not do

- Interpret, parse, or validate manifest content
- Verify cryptographic signatures
- Enforce consent rules
- Check TTL or expiration
- Authenticate requestors
- Transform, filter, or modify manifest payloads
- Support search, discovery, or browsing
- Provide write APIs for manifest registration (currently)

---

## 2. The Resolution Flow

The resolution flow is deliberately simple. Every step is designed to be implementable in any language, on any platform, with minimal dependencies.

### Step-by-step resolution

**Step 1: Consumer acquires a UMID.**
The UMID might come from a QR code scan, an NFC tap, an API parameter, a URL shared in a message, a metaverse portal handoff, a Bluetooth beacon, or printed text on a business card. The transport mechanism does not matter -- the UMID is a self-contained identifier.

A typical UMID looks like: `urn:uuid:9b1d0e3f-7c4a-4e8b-a2d5-6f3e8c9d0b1a`

**Step 2: Consumer sends a GET request to the resolver.**
The consumer constructs the URL by appending the URL-encoded UMID to `https://myum.net/`:

```
GET https://myum.net/urn%3Auuid%3A9b1d0e3f-7c4a-4e8b-a2d5-6f3e8c9d0b1a
```

For UMIDs that contain characters incompatible with URL path syntax (such as forward slashes), the resolver supports a base64url escape hatch:

```
GET https://myum.net/b64u:dXJuOnV1aWQ6OWIxZDBlM2YtN2M0YS00ZThiLWEyZDUtNmYzZThjOWQwYjFh
```

**Step 3: Resolver looks up the UMID.**
The resolver parses the UMID from the path, constructs a KV key (`um:{UMID}`), and queries Cloudflare KV for the record.

**Step 4: Resolver returns the result.**

The resolver has exactly four possible outcomes for a valid UMID lookup:

- **307 Temporary Redirect** -- The UMID maps to a redirect record. The resolver returns a `Location` header pointing to the canonical manifest URL. The consumer follows the redirect to fetch the actual manifest from its authoritative source.

- **200 OK** -- The UMID maps to a payload record. The resolver returns the manifest JSON directly in the response body, with `Content-Type: application/ld+json; charset=utf-8`.

- **404 Not Found** -- The UMID is not registered. No record exists in the resolver's registry.

- **410 Gone** -- The UMID was registered but has been explicitly revoked. The manifest should not be used.

**Step 5: Consumer validates the manifest.**
This is critical. The resolver's job ends at delivery. The consumer is responsible for:

- **TTL check:** Is `now` before `expiresAt`? If the manifest is expired, reject it.
- **Signature verification:** Does the Ed25519 signature over the JCS-canonicalized payload verify against the issuer's public key? (Required for v0.2 manifests.)
- **Consent check:** Does the manifest's consent section allow the consumer's intended use?
- **Structure validation:** Does the manifest conform to the JSON Schema for its declared version?

The resolver never performs these checks. It is a delivery mechanism, not a trust authority.

### Additional response codes

Beyond the four core outcomes, the resolver returns:

- **304 Not Modified** -- When the consumer sends an `If-None-Match` header with a matching ETag. This enables efficient conditional revalidation without re-downloading the full manifest.

- **400 Bad Request** -- The UMID encoding is invalid (missing, empty, malformed base64url, or extra path segments).

- **405 Method Not Allowed** -- The request used a method other than GET, HEAD, or OPTIONS.

- **500 Internal Server Error** -- The KV record exists but cannot be parsed as valid JSON. This indicates a corrupt record in the resolver's registry.

### The flow visualized

```
Consumer                     myum.net Resolver                 Canonical Source
   │                              │                                  │
   │  GET /{UMID}                 │                                  │
   │─────────────────────────────>│                                  │
   │                              │                                  │
   │                              │  KV lookup: um:{UMID}            │
   │                              │                                  │
   │  307 + Location: {url}       │                                  │
   │<─────────────────────────────│                                  │
   │                              │                                  │
   │  GET {url}                   │                                  │
   │─────────────────────────────────────────────────────────────────>│
   │                              │                                  │
   │  200 + manifest JSON         │                                  │
   │<─────────────────────────────────────────────────────────────────│
   │                              │                                  │
   │  Validate: TTL, signature,   │                                  │
   │  consent, structure          │                                  │
   │                              │                                  │
```

---

## 3. Who Owns the Data?

The manifest issuer owns the data. Always.

This is a foundational design principle. The resolver is not a custodian, not a controller, and not a gatekeeper. It is a phone book -- it tells you where to find someone, but it does not own their house.

### The ownership model

- **The manifest issuer** creates the manifest, signs it with their private key, hosts it at a location they control, and registers the UMID-to-location mapping with the resolver.

- **The resolver** stores only the mapping: `UMID -> canonical source URL` (for redirect records) or `UMID -> manifest payload JSON` (for payload records). It does not modify, interpret, or claim ownership of the content.

- **The canonical manifest** lives wherever the issuer published it. This could be:
  - The issuer's own web server
  - A Solid Pod
  - IPFS or other decentralized storage
  - A CDN
  - A static file host
  - The resolver itself (when using payload records)

### What this means in practice

**No vendor lock-in.** Because the issuer controls where the manifest lives, they can move it at any time. If they migrate from one hosting provider to another, they update the resolver registration to point to the new location. The UMID does not change. Consumers who resolve the UMID get the new location transparently.

**The manifest survives resolver outage.** If myum.net goes down, the manifest still exists at its canonical source. Only the lookup path is disrupted. Any consumer that already knows the canonical URL (from a previous resolution, from a cached redirect, or from an out-of-band channel) can still fetch the manifest directly.

**No data exfiltration risk from the resolver.** The resolver does not accumulate a copy of the world's identity data. For redirect records, it stores only URLs. For payload records, the manifest content is available, but this is the issuer's explicit choice -- they chose to put the content in the resolver rather than hosting it elsewhere.

**The issuer controls revocation.** When a manifest should no longer be used, the issuer marks the resolver record as revoked. The resolver then returns `410 Gone` for that UMID. The issuer can also simply stop hosting the manifest at its canonical URL.

### Comparison with centralized identity providers

In traditional centralized identity (OAuth, SAML, social login), the identity provider owns and controls the authoritative identity data. If the provider goes down, access is lost. If the provider changes their terms, the user has limited recourse. If the provider decides to revoke access, the user's identity disappears.

Universal Manifest inverts this model. The identity data lives where the subject (or their issuer) chooses. The resolver is a utility that makes it easy to find, not a gatekeeper that controls access. This is user-sovereign identity lookup.

---

## 4. Where Is Data Stored?

The resolver system involves three distinct data locations, each with a different role.

### 4.1 The resolver registry: Cloudflare KV

The resolver's internal registry is a Cloudflare Workers KV namespace. KV is a globally distributed key-value store designed for read-heavy workloads with eventual consistency.

**What is stored:** JSON records keyed by `um:{UMID}`. Each record is one of two kinds:

**Payload record:**
```json
{
  "kind": "payload",
  "status": "active",
  "contentType": "application/ld+json; charset=utf-8",
  "body": { /* the full manifest JSON */ },
  "createdAt": "2026-02-17T00:00:00.000Z",
  "updatedAt": "2026-02-17T00:00:00.000Z"
}
```

**Redirect record:**
```json
{
  "kind": "redirect",
  "status": "active",
  "url": "https://example.com/manifests/my-manifest.jsonld",
  "createdAt": "2026-02-17T00:00:00.000Z"
}
```

Either kind can be revoked by setting `"status": "revoked"` and optionally adding a `"revokedAt"` timestamp.

**Infrastructure details:**
- Production KV namespace ID: `f13cd9e9d4db43918b287b2d2c943456`
- Staging KV namespace ID: `bafa21a750e74b09b353509ed97098ac`
- Production and staging use separate KV namespaces to prevent data contamination
- The KV binding in the Worker is named `UMID_KV`

### 4.2 The canonical manifest: wherever the issuer hosts it

For redirect records, the actual manifest JSON lives at the URL specified in the record's `url` field. This is entirely under the issuer's control. The resolver does not cache, mirror, or transform it.

For payload records, the manifest JSON is embedded directly in the KV record. In this case, the resolver is also the host -- but this is the issuer's choice, not a requirement.

### 4.3 The consumer frontend: static assets on universalmanifest.net

When a browser visits the resolver consumer page at `universalmanifest.net/resolver/`, it gets a human-readable interface for looking up UMIDs. This consumer frontend is a static HTML/CSS/JavaScript application that:

- Accepts a UMID input from the user
- Makes a fetch request to myum.net
- Displays the result with trust verdict, provenance labels, and diagnostics
- Distinguishes between live KV-backed responses and built-in demo fixtures

This frontend is served from the documentation site (universalmanifest.net), not from the resolver itself (myum.net). The resolver only serves API responses.

### 4.4 The built-in fallback fixture

The resolver contains one hardcoded demo fixture for the UMID `urn:uuid:11111111-1111-4111-8111-111111111111`. This fixture is a v0.2 signed manifest that is returned even when the KV namespace is empty, enabling smoke testing, harness validation, and demo workflows without requiring KV seeding.

The resolver marks this response with `X-UM-Resolver-Source: fallback_fixture` so consumers can distinguish it from real published data.

---

## 5. The HTTP Contract

The resolver exposes a strict, documented HTTP contract. Every response code, header, and behavior is intentional and specified.

### Contract version

Every resolver response includes:
```
X-UM-Resolver-Contract: myum-resolver/v0.1
```

This header tells consumers which version of the resolver contract they are interacting with. If the contract changes in a breaking way, the version will be bumped.

### Response provenance

Every resolver response includes:
```
X-UM-Resolver-Source: runtime | kv | fallback_fixture
```

This tells consumers where the response came from:
- `runtime` -- generated by resolver logic (health checks, well-known descriptor, error responses for unknown UMIDs or bad requests)
- `kv` -- fetched from a KV-backed record (real published data)
- `fallback_fixture` -- the built-in demo fixture (not authoritative publisher data)

### Status codes: the complete matrix

| Status | Meaning | When returned | Cache behavior |
|--------|---------|---------------|----------------|
| **200 OK** | Manifest payload returned | KV payload record found, or fallback fixture matched | `public, max-age=60` |
| **204 No Content** | CORS preflight response | OPTIONS request | `no-store` |
| **304 Not Modified** | ETag matches, no re-download needed | `If-None-Match` header matches current ETag | (same as 200) |
| **307 Temporary Redirect** | UMID found, follow Location | KV redirect record found | `public, max-age=60` |
| **400 Bad Request** | Invalid UMID encoding | Malformed path, empty UMID, bad base64url | `no-store` |
| **404 Not Found** | UMID not registered | No KV record and no fixture match | `no-store` |
| **405 Method Not Allowed** | Wrong HTTP method | POST, PUT, DELETE, PATCH, etc. | `no-store` |
| **410 Gone** | UMID revoked | KV record exists with `status: "revoked"` | `no-store` |
| **500 Internal Server Error** | Corrupt record | KV record exists but cannot be parsed as JSON | `no-store` |

### Why 307 specifically

The resolver uses 307 Temporary Redirect rather than 301 (Permanent) or 302 (Found) for deliberate reasons:

**307 preserves the original request method.** Unlike 302, which historically allowed clients to change POST to GET, 307 guarantees the method is preserved. This matters for HEAD requests -- a HEAD to the resolver should result in a HEAD to the canonical source.

**307 signals that the redirect is temporary.** Unlike 301, which tells clients to cache the redirect permanently, 307 tells clients that the resolver is the authoritative lookup point and the canonical source URL may change. This is correct -- issuers can update their resolver registration to point to a new location at any time.

**307 keeps the resolver in the resolution path.** With a 301, well-behaved clients would skip the resolver on subsequent requests and go directly to the canonical source. With a 307, clients always go through the resolver first, ensuring they get the latest mapping. This is essential for the resolver's "always-current" guarantee.

### Headers

**Common headers on every response:**
- `Access-Control-Allow-Origin: *` -- open CORS for read-only access
- `Access-Control-Allow-Methods: GET,HEAD,OPTIONS`
- `Access-Control-Allow-Headers: *`
- `Access-Control-Expose-Headers: etag, cache-control, content-type, location, x-um-resolver-contract, x-um-resolver-source` -- allows browser tooling to read non-simple headers
- `X-Content-Type-Options: nosniff` -- prevents MIME type sniffing
- `Referrer-Policy: no-referrer` -- prevents referrer leakage
- `X-UM-Resolver-Contract: myum-resolver/v0.1`
- `X-UM-Resolver-Source: runtime | kv | fallback_fixture`

**Successful resolution headers (200):**
- `Content-Type: application/ld+json; charset=utf-8` (default; may vary per record)
- `Cache-Control: public, max-age=60`
- `ETag: W/"sha256-..."` -- weak ETag derived from SHA-256 hash of response body

**Redirect headers (307):**
- `Location: {canonical_source_url}`
- `Cache-Control: public, max-age=60`

**Error headers:**
- `Cache-Control: no-store` -- errors are not cached

### Content negotiation

The resolver does not perform content negotiation in the traditional sense. It serves the same response regardless of `Accept` header. API clients, browsers, and automated systems all receive the same JSON responses and redirects.

The human-readable consumer frontend is served from universalmanifest.net, not from myum.net. This separation ensures the resolver contract stays clean and machine-readable.

### Well-known descriptor

The resolver publishes a machine-readable descriptor at `/.well-known/myum-resolver.json` that documents its own behavior:

```json
{
  "contract": "myum-resolver/v0.1",
  "resolver": "myum-resolver",
  "umidPathRule": [
    "GET /{UMID_PATH}",
    "If path segment starts with \"b64u:\" then remainder is base64url UTF-8 UMID.",
    "Otherwise the segment is treated as the UMID directly (URL-decoded)."
  ],
  "kv": {
    "binding": "UMID_KV",
    "keyPattern": "um:{UMID}"
  },
  "caching": {
    "defaultResolveCacheControl": "public, max-age=60",
    "note": "Consumers MUST enforce manifest expiresAt (TTL) regardless of HTTP caching."
  },
  "privacy": {
    "note": "This minimal runtime assumes resolved manifests are publicly readable."
  },
  "endpoints": {
    "health": "/health",
    "resolve": "/{UMID_PATH}"
  }
}
```

This descriptor enables automated tooling to discover and interact with any conformant resolver without hardcoded assumptions.

### ETag and conditional requests

The resolver generates weak ETags by computing a SHA-256 hash of the response body, encoding it as base64url, and wrapping it in the standard weak ETag format: `W/"sha256-{hash}"`.

Consumers can use `If-None-Match` with the ETag value. If the manifest has not changed, the resolver returns 304 Not Modified with no body, saving bandwidth. This is especially valuable for polling consumers that periodically check for manifest updates.

---

## 6. What You Can Do With It

### Instant lookup

Any system with a UMID can resolve it to a full manifest in one HTTP call. No authentication, no token exchange, no API key, no session. Just a GET request. The entire resolution is a single network round trip (or two, if the resolver returns a redirect).

### QR code portability

Print a QR code containing a UMID. Anyone with a phone, tablet, smart glasses, or any QR-capable device can scan the code, resolve the UMID through myum.net, and get the full manifest. The QR code does not need to contain the manifest data itself -- just the identifier. This keeps QR codes small and scannable even at small physical sizes.

### Cross-platform identity

The same UMID works everywhere. A browser, a mobile app, a smart glasses AR overlay, a metaverse portal, an IoT display device, and a command-line script can all resolve the same UMID and get the same manifest. Each consumer reads the facets it understands and respects the consent toggles relevant to its context.

This is the "resolve once, use everywhere" principle. The UMID is the universal key; the manifest is the universal document; the resolver is the universal lookup.

### Always-current

Unlike distributing a static file (which becomes stale immediately), resolving a UMID through the resolver always returns the latest published version. If the issuer updates their manifest, the next resolution picks up the change. The resolver's short cache TTL (60 seconds) and ETag support ensure freshness without excessive load.

### Transport agnosticism

The UMID itself is just a string -- a URN in UUID format. It can be transported via any medium:

- URL: `https://myum.net/urn%3Auuid%3A9b1d0e3f-...`
- QR code containing the UMID string
- NFC tag with the UMID as payload
- Bluetooth Low Energy beacon broadcasting the UMID
- API parameter in a JSON payload
- Printed on a business card, gallery placard, or conference badge
- Spoken aloud and typed into a lookup interface
- Embedded in a metaverse portal handoff protocol

The resolver does not care how the consumer acquired the UMID. It just resolves it.

### Zero vendor lock-in

The issuer controls their manifest. They host it where they want, sign it with their own keys, and register it with the resolver on their own terms. If they want to move to a different host, they update the resolver registration. If they want to stop using myum.net, they can run their own conformant resolver or distribute manifests through other channels entirely.

The resolver is infrastructure, not a platform. It has no user accounts, no subscription model, no data retention policies beyond the KV records, and no terms of service that grant it rights over the content it routes.

---

## 7. What Is Revolutionary

### User-sovereign identity lookup

Traditional identity lookup systems are controlled by the provider. OAuth requires the identity provider to be online and cooperative. SAML requires federation agreements. Social login requires the social platform's API. In all these models, the entity that operates the lookup infrastructure controls access to the identity.

The Universal Manifest resolver inverts this. The lookup infrastructure is a public utility. The identity data is controlled by the subject (or their issuer). The resolver cannot deny access to a manifest based on who is asking, cannot modify the manifest in transit, and cannot withhold the data for commercial reasons. It is a routing layer, not an authority layer.

This is user-sovereign identity lookup: the subject decides what is in their manifest, where it is hosted, and what consent rules govern it. The resolver just makes it findable.

### Offline-tolerant operation

Once a consumer fetches a manifest through the resolver, it can operate independently until the manifest's TTL expires. There is no need to maintain a persistent connection to the resolver, no need to refresh tokens, no need to ping a session endpoint.

This is critical for:
- **Edge devices** (gallery displays, public kiosks) that may have intermittent connectivity
- **Smart glasses** that need to operate in areas with poor cellular coverage
- **IoT devices** with limited network capabilities
- **Metaverse environments** that need to render identity immediately, not after a round-trip to an external service

The resolver is the on-ramp. After that, the manifest is self-contained.

### Default-deny consent travels with the data

The resolver delivers a document that includes its own privacy rules. The manifest's `consents` section specifies what downstream systems are allowed to do with the data, using a default-deny model: if a consent is not explicitly granted, it is denied.

This means:
- No separate consent API to call
- No cookie banner to display
- No terms-of-service page to link to
- No consent database to maintain

The consent rules travel with the data, through the resolver, to the consumer. Every system in the chain has the same consent information because it is part of the document itself.

### Spec-level, not product-level

The resolver is defined as a specification concept, not a product. myum.net is one deployment. The specification documents the contract (status codes, headers, path rules, KV schema) so that anyone can build a conformant resolver.

An enterprise could run a private resolver for their internal UMID registry. A standards body could run a resolver for their member organizations. A metaverse platform could run a resolver for their user manifests. All of these would be conformant resolvers implementing the same contract, queryable the same way, with the same guarantees.

### One lookup, infinite contexts

A single UMID resolution returns a manifest that serves multiple consumer contexts simultaneously. A gallery display reads the `publicProfile` facet and checks the `publicDisplay` consent. A smart glasses AR system reads the `crossWorldProfile` facet and checks the `ar.recording.faceVisible` consent. A metaverse portal reads avatar pointers and checks metaverse consent toggles.

All from one resolution. One manifest. One UMID. The resolver does not need to know which context the consumer operates in -- it returns the whole manifest, and each consumer reads the parts it understands.

---

## 8. Limitations and Boundaries

### The resolver does NOT verify signatures

Signature verification is the consumer's responsibility. The resolver delivers the manifest as-is. It does not check whether the Ed25519 signature is valid, whether the public key is trustworthy, or whether the signing algorithm is supported. A consumer that does not verify signatures is trusting the transport chain, not the issuer.

### The resolver does NOT enforce consent

The manifest contains consent rules, but the resolver does not read, interpret, or enforce them. It returns the full manifest to every requestor. Consent enforcement happens at the consumer level -- the system that reads the manifest must check the `consents` section before using the data.

### The resolver does NOT check TTL

The resolver does not validate whether a manifest has expired. It returns whatever is in the KV record, regardless of the manifest's `expiresAt` timestamp. Consumers MUST check `expiresAt` and reject expired manifests. HTTP cache headers (`max-age=60`) control transport caching, not application-level validity.

### Single point of lookup, not single point of failure for data

If myum.net goes offline, UMID lookups fail. But the manifests themselves still exist at their canonical sources. Any consumer that already knows the canonical URL can fetch the manifest directly. The resolver is a convenience and discoverability layer, not a data custodian.

That said, for consumers that rely solely on the resolver for manifest discovery, resolver downtime means effective service interruption. This is a practical consideration that future federation work would address.

### No federation model yet

Currently, there is no specification for resolver federation. myum.net is the only reference deployment. There is no mechanism for multiple resolvers to share registrations, no gossip protocol for UMID propagation, and no standard for resolver discovery beyond the well-known descriptor.

This is an acknowledged limitation. Future work may define:
- A federation protocol for resolver-to-resolver synchronization
- A discovery mechanism for finding the authoritative resolver for a given UMID
- A fallback chain for resolving UMIDs across multiple resolvers

### No self-service registration UI

Publishing a manifest to the resolver currently requires direct KV manipulation -- either through the Cloudflare dashboard, the Wrangler CLI, or a future write API. There is no self-service web interface where an issuer can register their UMID, upload their manifest, or manage their records.

This is what the proposed "equip interface" would address: a guided workflow for manifest publishing and resolver registration.

### No search or discovery

The resolver is strictly a lookup service. You must already have a UMID to use it. There is no search endpoint, no directory listing, no browse capability, and no way to discover UMIDs. This is by design -- the resolver is a phone book where you look up a number you already have, not a search engine for finding new numbers.

### Privacy posture is public-only

The current resolver assumes all resolved manifests are publicly readable. There is no access control, no authentication, no authorization. Anyone who knows a UMID can resolve it.

Private or authenticated resolution is explicitly out of scope for the current contract version and is recognized as a future profile that needs separate design work.

### Rate limiting is an infrastructure concern

The resolver does not currently enforce rate limits. Abuse prevention (DDoS protection, request throttling) is handled at the infrastructure level by Cloudflare's built-in protections, not by the resolver application code. Future contract versions may define rate limiting behavior.

### No manifest content validation

The resolver does not validate manifest content on ingestion or retrieval. It does not check whether a payload record contains valid JSON-LD, whether required fields are present, or whether the manifest conforms to any version of the Universal Manifest specification. It is a pass-through routing layer.

---

## 9. Resolver vs. Other Systems

### vs. DNS

The closest conceptual match. DNS resolves domain names (like `example.com`) to IP addresses (like `93.184.216.34`). The myum.net resolver resolves UMIDs (like `urn:uuid:9b1d0e3f-...`) to manifest locations (like `https://pod.example/profile.jsonld`).

Key differences:
- DNS is hierarchical and delegated. The resolver is flat -- all UMIDs are peers.
- DNS resolves to network addresses. The resolver resolves to document locations.
- DNS has a mature federation model. The resolver does not (yet).
- DNS is critical internet infrastructure. The resolver is specialized for identity documents.

### vs. DID resolution

Complementary, not competing. A DID (Decentralized Identifier) resolves to a DID Document, which contains verification methods, service endpoints, and authentication information. A UMID resolves to a Universal Manifest, which contains identity state, consent rules, claims, and pointers.

A Universal Manifest may reference DIDs. The `subject` field typically contains a DID. The `signature.keyRef` field may point to a DID verification method. The two systems work together: DIDs provide cryptographic identity, and Universal Manifest provides portable state that references those identities.

### vs. OAuth / OIDC

Fundamentally different. OAuth is an authorization framework. OIDC is an authentication layer on top of OAuth. Both involve:
- Tokens (access tokens, ID tokens, refresh tokens)
- Sessions (login state, session cookies)
- Scopes (permission grants)
- Provider dependency (the IdP must be online)

The resolver involves none of these. It is a stateless document lookup. No tokens, no sessions, no scopes, no login. The consumer gets a manifest and uses it according to the embedded consent rules. The resolver has no concept of "granting" or "denying" access.

### vs. Solid Pod

Complementary. A Solid Pod is a data store -- it holds your data and controls access to it. The resolver is a lookup layer -- it tells consumers where to find data.

A manifest could live inside a Solid Pod. The resolver would store a redirect record pointing to the Pod URL. When a consumer resolves the UMID, they get redirected to the Solid Pod, where the Pod's access control policies determine whether they can read the manifest.

In this model, Solid provides storage and access control. The resolver provides discoverability. Universal Manifest provides the document format and consent semantics.

### vs. Verifiable Credentials

Complementary. Verifiable Credentials (VCs) are individual signed statements about a subject. A Universal Manifest is a container that can carry VCs as claims within facets, along with consent rules, device registrations, and pointers. The resolver provides lookup for the container; the VC infrastructure provides verification for individual claims within it.

---

## 10. The Consumer Frontend

When a user visits the resolver consumer page at `universalmanifest.net/resolver/`, they get a human-readable interface for resolving UMIDs. This is not served by the resolver itself (myum.net) -- it is a client-side application hosted on the documentation site that makes API calls to the resolver.

### What the consumer frontend shows

**Lookup interface:** A text input for entering a UMID, with preset examples for the demo fixture, redirect demo, revoked demo, and unknown UMID. Options to select the resolver base URL and to use the b64u encoding escape hatch.

**Resolution result:** After resolving, the page displays:
- **Trust verdict:** SAFE TO USE, DO NOT USE, or MANUAL REVIEW based on structure validation, TTL freshness, and signature verification
- **Provenance label:** Whether the response came from a KV-backed record, the built-in demo fixture, or runtime logic
- **Status and headers:** HTTP status code, resolver contract version, resolver source, ETag, cache-control
- **Manifest preview:** The JSON payload (for 200 responses)
- **Redirect information:** The Location URL and option to follow the redirect (for 307 responses)
- **Error details:** Machine-parseable error JSON (for 400/404/410/500 responses)

**Diagnostics:** Request URL, latency, raw headers, and the ability to copy a cURL command for reproducing the request.

### What the consumer frontend does NOT show

- Raw JSON-LD without interpretation -- it presents a structured summary
- Internal resolver implementation details (no Cloudflare, no KV, no Worker references)
- Write or registration capabilities -- it is read-only

### Provenance discipline

The consumer frontend clearly labels every response with its provenance:
- **KV-backed resolver record** -- real published data from a manifest issuer
- **Built-in demo fixture** -- deterministic demo data baked into the resolver runtime, not authoritative publisher data
- **Runtime-generated** -- error or metadata response from the resolver logic

This labeling was specifically hardened in production QA to prevent users from mistaking demo fixture data for real published identity data.

---

## 11. Infrastructure and Deployment

### Runtime platform

The resolver runs as a Cloudflare Worker -- a serverless function that executes at Cloudflare's global edge network. This provides:
- Sub-millisecond cold start times
- Global distribution (the resolver runs in the nearest Cloudflare data center to the requestor)
- Automatic scaling (no capacity planning needed)
- Built-in DDoS protection from Cloudflare's infrastructure

### Route bindings

The resolver is bound to two route patterns:
- `myum.net/*` -- apex domain
- `www.myum.net/*` -- www subdomain

Both route to the same Worker, ensuring consistent behavior regardless of which hostname is used.

### Environment separation

Production and staging use separate Cloudflare Worker environments with separate KV namespaces:
- **Production:** Routes on `myum.net` and `www.myum.net`, production KV namespace
- **Staging:** Routes on `staging.myum.net` and `www.staging.myum.net`, staging KV namespace, with `workers_dev = true` for development URL access

### Contract test suite

The resolver has a dedicated contract test suite (`services/myum-resolver/scripts/contract-tests.mjs`) that validates the complete status matrix, path parsing, header contract, and ETag behavior. This suite runs in CI and locally via `npm run test:contract`.

### Compatibility date

The Worker's Cloudflare compatibility date is `2026-02-17`, pinning the runtime behavior to a specific version of the Workers platform APIs.

---

## NotebookLM Video Brief

### L3-05-DEEP: The myum.net Resolver -- Complete Deep Dive
**Level:** 3 | **Length:** 6 min
**Audience:** Developers, architects, and standards evaluators wanting the complete resolver story.

```
FOCUS: What the resolver is and is not: a thin stateless lookup service that maps UMIDs to canonical manifest sources, not a database or identity provider. The step-by-step resolution flow from UMID acquisition through GET request, KV lookup, 307 redirect or 200 payload, to consumer-side validation. Who owns the data: the manifest issuer always owns it, the resolver stores only pointers. The HTTP contract: 307 Temporary Redirect for found UMIDs, 404 for unknown, 410 for revoked, with contract versioning and provenance headers. What is revolutionary: user-sovereign identity lookup where the subject controls their data, offline-tolerant operation after initial fetch, default-deny consent embedded in the document itself. Limitations: no signature verification, no consent enforcement, no federation model, no search or discovery. Comparison to DNS, DID resolution, OAuth, and Solid. The resolver is spec-level infrastructure that anyone can deploy.

DO NOT COVER: Do not explain manifest internals such as facets, pointers, claims, or the consent model in detail. Do not cover specific integration lanes like metaverse portaling or smart glasses. Do not discuss the TypeScript implementation, Cloudflare Workers infrastructure, or deployment tooling. Do not cover the equip interface proposal or consumer frontend redesign plans. Do not discuss signature mechanics beyond noting the consumer's verification responsibility.

WHY THIS EXISTS: The definitive explanation of what the resolver does, why it matters, and where its boundaries are.
```
