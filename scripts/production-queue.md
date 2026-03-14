# Video Production Queue — Prioritized for NotebookLM

**Created:** 2026-03-11
**Purpose:** Produce videos in priority order using NotebookLM audio generation.

---

## Instructions

1. Upload `notebooklm-knowledge-vault.zip` to NotebookLM as a source.
2. For each video below, paste the brief (inside the code fence) as a prompt to generate the audio content.
3. Work through the list in order — Priority 1 is needed for the OMA3 meeting on 2026-03-12.

---

## Custom visual style. 
A AAA game with Unreal 6 high resolution award winning game UI interfaces so realistic, it feels like a metaverse that you can't tell is virtual. It feels and looks real.

---


## Priority 1: OMA3 Meeting (produce tonight)

These are needed for the presentation tomorrow. Produce in this order.

---

### 0. L3-10: Facet Privacy — Public, Encrypted, and Selective Disclosure
**Level:** 3 | **Length:** 6 min | **Audience:** Engineers, architects, and security-minded evaluators wanting the complete facet privacy story

**Why this is first:** A hardcore engineering deep dive on facet encryption that will impress the OMA3 audience — demonstrates UM's cryptographic sophistication and standards alignment.

**Source document:** `docs/explainers/facet-encryption-deep-dive.md`

```
FOCUS: How facets work today as plaintext data compartments gated by default-deny consent toggles. The three privacy approaches: projection model (consumer-specific derived manifests), consent-gated access control (policy signals), and encrypted inline facets (cryptographic enforcement). The three encryption methods: JWE per-facet encryption with ECDH-ES+A256KW and X25519 key agreement, BBS+ selective disclosure with BLS12-381 for unlinkable presentation privacy, and SD-JWT for JWT ecosystem interoperability. How encryption interacts with signing: encrypt-then-sign so every consumer can verify the signature regardless of decryption access. Key management: DID Document keyAgreement for key discovery, envelope encryption for efficient key rotation, TTL-based expiration for revocation. What is revolutionary: per-facet encryption in a portable self-contained document where different recipients decrypt different facets from one manifest — something no other standard offers at the envelope level. Consent plus encryption as defense in depth. The path forward: all three methods as opt-in layers above the base protocol.

DO NOT COVER: Do not explain the resolver, portaling, IWPS, or integration lanes. Do not cover the consent model in isolation — that is L3-03. Do not discuss implementation code, TypeScript, or specific library choices. Do not cover the projection model in detail — that is established and documented elsewhere. Stay at the specification architecture level. Do not mention PeerMesh or any runtime.

WHY THIS EXISTS: The definitive explanation of how UM handles facet privacy from plaintext through cryptographic enforcement, covering the full spectrum of privacy mechanisms available to specification adopters.
```

---

### 1. L2-03: Universal Manifest for Standards Bodies
**Level:** 2 | **Length:** 2 min | **Audience:** OMA3, W3C, MSF participants, and governance-focused evaluators

**Why this is first:** The most directly relevant video for the OMA3 audience. This is the one they will watch.

```
FOCUS: Architectural positioning: UM as a portable state envelope specification that complements (not replaces) existing standards. How UM relates to W3C Verifiable Credentials (UM carries VCs as claims within facets), DIDComm (UM is a document format, DIDComm is a messaging protocol), Solid (UM uses pointers to Solid Pods), and OIDC (UM carries broader state). The IWPS complementarity: UM provides the portable identity and consent layer, IWPS provides the inter-world transport protocol. The spec-vs-implementation boundary: UM is language-neutral, JSON Schema validated, with open-source governance.

DO NOT COVER: Do not explain how to build or parse a manifest. Do not cover user-facing scenarios (gallery, smart glasses). Do not discuss the TypeScript reference implementation or npm packages. Keep it at the standards architecture level.

WHY THIS EXISTS: Positions UM in the standards landscape so evaluators understand where it fits without implementation details.
```

---

### 2. L3-09: IWPS + UM: The Complete Portaling Stack
**Level:** 3 | **Length:** 6 min | **Audience:** Standards-aware metaverse architects wanting to understand the full portaling architecture

**Why this is here:** Alfred Tom specifically asked about fitting UM into IWPS. This answers that directly.

```
FOCUS: The two-layer portaling architecture: IWPS (Inter-World Portaling System) handles the transport protocol for moving between virtual worlds, UM handles the portable identity, consent, and credential envelope that travels through the portal. How they complement each other: IWPS defines how a portal connection is established and how data flows between worlds; UM defines what data the user carries and what permissions govern it. The handoff: IWPS initiates the portal, requests the user's UMID, UM manifest is resolved and delivered to the destination world. Consent enforcement at the destination: the receiving world reads UM consent toggles before rendering avatar, loading social graph, or capturing voice/face. Why neither layer alone is sufficient — IWPS without UM has no portable identity; UM without IWPS has no transport mechanism.

DO NOT COVER: Do not explain UM data structures or consent model in depth — reference them. Do not cover non-portaling UM use cases. Do not discuss IWPS protocol internals (handshake, packet format) beyond the conceptual architecture. Do not position this as UM-vs-IWPS — they are partners.

WHY THIS EXISTS: The definitive explanation of how UM and IWPS together solve the metaverse portaling problem.
```

---

### 3. L1-01: Everything You Need to Know About Universal Manifest
**Level:** 1 | **Length:** 6 min | **Audience:** Anyone who wants the complete picture — potential adopters, conference attendees, curious technologists

**Why this is here:** The master explainer to have as a complete overview if needed during the meeting.

```
FOCUS: Cover the full UM story: the data fragmentation problem, the portable envelope concept (JSON-LD, UMID, TTL), facets and pointers as modular data architecture, default-deny consent model, manifest resolution via myum.net, cryptographic signatures (Ed25519 + JCS in v0.2), the composite stack (storage/transit/runtime), and real-world scenarios (gallery, smart glasses, metaverse portaling, proof of personhood). End with the adoption path.

DO NOT COVER: Do not go deep on any single integration lane — keep each scenario to one or two sentences. Do not discuss IWPS protocol details, specific standards body positioning, or implementation-level code. This is the complete map, not the territory.

WHY THIS EXISTS: The single canonical overview — replaces needing to watch multiple videos to get the full picture.
```

---

### 4. L3-07: The Composite Stack Architecture
**Level:** 3 | **Length:** 6 min | **Audience:** System architects and technical leaders wanting to understand where UM fits

**Why this is here:** Alfred asked for "architectural overview (data structures, file formats, etc.)" — this covers exactly that.

```
FOCUS: The three-layer composite stack: Storage/Registry (Solid Pods, databases, canonical data stores), Transit/State Envelope (Universal Manifest), and Execution/Runtime (web apps, native clients, spatial engines, edge devices). UM is the transit layer — it does not replace storage and it does not replace runtime. It bridges them by securely carrying identity, pointers, and consents from storage into execution. How each layer has its own responsibilities and UM only claims the transit role. Integration patterns: read-only consumption, bidirectional publishing, full lifecycle management. Why this separation matters: existing storage and runtime investments are preserved, UM just standardizes the handoff.

DO NOT COVER: Do not explain specific data structures, consent mechanics, or signature details — those are separate L3 videos. Do not discuss specific implementations or runtime frameworks. Do not cover IWPS or metaverse-specific architecture.

WHY THIS EXISTS: The definitive explanation of UM's architectural position in a system stack.
```

---

### 5. L3-05-DEEP: The myum.net Resolver -- Complete Deep Dive
**Level:** 3 | **Length:** 6 min | **Audience:** Developers, architects, and standards evaluators wanting the complete resolver story

**Why this is here:** Alfred asked about "data structures, file formats" and the resolver is the core architectural component that connects UMIDs to manifests. This explains the resolution infrastructure that makes the whole system work.

**Source document:** `docs/explainers/resolver-deep-dive.md`

```
FOCUS: What the resolver is and is not: a thin stateless lookup service that maps UMIDs to canonical manifest sources, not a database or identity provider. The step-by-step resolution flow from UMID acquisition through GET request, KV lookup, 307 redirect or 200 payload, to consumer-side validation. Who owns the data: the manifest issuer always owns it, the resolver stores only pointers. The HTTP contract: 307 Temporary Redirect for found UMIDs, 404 for unknown, 410 for revoked, with contract versioning and provenance headers. What is revolutionary: user-sovereign identity lookup where the subject controls their data, offline-tolerant operation after initial fetch, default-deny consent embedded in the document itself. Limitations: no signature verification, no consent enforcement, no federation model, no search or discovery. Comparison to DNS, DID resolution, OAuth, and Solid. The resolver is spec-level infrastructure that anyone can deploy.

DO NOT COVER: Do not explain manifest internals such as facets, pointers, claims, or the consent model in detail. Do not cover specific integration lanes like metaverse portaling or smart glasses. Do not discuss the TypeScript implementation, Cloudflare Workers infrastructure, or deployment tooling. Do not cover the equip interface proposal or consumer frontend redesign plans. Do not discuss signature mechanics beyond noting the consumer's verification responsibility.

WHY THIS EXISTS: The definitive explanation of what the resolver does, why it matters, and where its boundaries are.
```

---

### 6. L3-11: Hashing, Caching, and Data Bundling Deep Dive
**Level:** 3 | **Length:** 6 min | **Audience:** Engineers, architects, and performance-minded evaluators wanting the complete integrity and optimization story

**Why this is here:** Completes the trio of engineering deep dives (encryption, resolver, hashing) that demonstrate UM's technical sophistication.

**Source document:** `docs/explainers/hashing-and-data-bundling-deep-dive.md`

```
FOCUS: How Universal Manifest achieves integrity and performance through three layers: SHA-256 content hashing for HTTP ETag generation and conditional revalidation (304 Not Modified), Ed25519 signatures over JCS-canonicalized payloads for end-to-end tamper detection, and the pointer-first architecture that keeps manifests at 1-3 KB by referencing external resources rather than embedding them. The two TTL layers: HTTP max-age=60 for transport caching and manifest expiresAt for application-level validity. Why content-addressed identifiers (CIDs) are deliberately deferred -- the UMID is a stable identity that persists across content changes, not a content hash that breaks on every update. The genuine gap: pointer targets have no hash-bound integrity verification today, and digestMultibase is the proposed solution. Future considerations: CBOR-LD binary encoding for constrained transports (NFC, QR, Bluetooth) achieving 60%+ compression, Merkle history for audit trails, and bitstring status lists for batch revocation. What is revolutionary: the separation of identity from content, pointer-first as an optimization strategy, and layered integrity without over-engineering.

DO NOT COVER: Do not explain the resolver flow in detail -- that is L3-05-DEEP. Do not cover facet encryption or consent mechanics -- those are L3-10 and L3-03. Do not discuss specific integration lanes or portaling. Do not mention implementation code, TypeScript, Cloudflare Workers, or deployment infrastructure. Stay at the specification architecture level. Do not mention PeerMesh or any runtime.

WHY THIS EXISTS: The definitive explanation of how UM achieves data integrity and performance through hashing, caching, pointer-first architecture, and deliberate technology choices -- covering what is implemented, what is proposed, and what is deferred.
```

---

## Priority 2: Core Library (produce this week)

The foundational videos that make the channel work.

---

### 5. L0-01: Welcome to Universal Manifest
**Level:** 0 | **Length:** 2 min | **Audience:** Anyone arriving for the first time — the YouTube channel trailer and site landing video

**Why this is here:** Channel trailer and orientation. Every viewer's first contact.

```
FOCUS: Introduce Universal Manifest as a portable data specification. Explain that the video library is organized by audience and depth. Name the five audience paths (executives, developers, standards bodies, metaverse builders, privacy/compliance) and point each to their Level 2 summary. Mention that the Master Explainer (L1-01) covers everything in one video.

DO NOT COVER: Do not explain any technical concepts in depth — no JSON-LD, no facets, no signatures, no resolver mechanics. This video is a map, not a lesson. Do not mention PeerMesh or any specific implementation.

WHY THIS EXISTS: The single orientation point so no viewer ever feels lost about where to start.
```

---

### 6. L2-01: Universal Manifest for Executives and Decision Makers
**Level:** 2 | **Length:** 2 min | **Audience:** CTOs, product leaders, business strategists evaluating UM for adoption

**Why this is here:** Broadest audience appeal. The business case for decision makers.

```
FOCUS: The business case: data fragmentation costs (custom integrations, duplicated effort, compliance burden), how UM reduces integration cost with one portable format, competitive positioning vs. VCs/DIDComm/Solid/OIDC, native privacy compliance (default-deny consent travels with data), and the progressive adoption path (parse, validate, consume, issue, sign). Emphasize that UM is a specification, not a vendor product.

DO NOT COVER: Do not explain JSON-LD structure, facet internals, pointer mechanics, or cryptographic details. Do not mention specific fixture names, schema files, or TypeScript. No metaverse portaling or smart glasses scenarios — keep it boardroom-relevant.

WHY THIS EXISTS: Gives decision makers the value proposition and competitive landscape without technical detail.
```

---

### 7. L2-02: Universal Manifest for Developers and Integrators
**Level:** 2 | **Length:** 2 min | **Audience:** Software engineers, system architects, API integrators evaluating UM for technical adoption

**Why this is here:** Technical adoption path. The developer on-ramp.

```
FOCUS: The data structures: JSON-LD document format, UMID as UUID URN, issuedAt/expiresAt TTL, facets as named modular sections, pointers as URI references to authoritative data. Consuming a manifest: JSON parsing, JSON Schema validation, facet reading, consent checking. The resolver at myum.net/{UMID}. Forward compatibility (ignore unknown fields). The adoption ladder from Level 1 (parse JSON) through Level 5 (sign and verify). Mention the TypeScript reference implementation exists as one option.

DO NOT COVER: Do not cover business value propositions, competitive positioning, or standards body politics. Do not explain specific integration lanes (metaverse, smart glasses, venue enrollment) — those are Level 3. Do not frame UM as a TypeScript library.

WHY THIS EXISTS: Gives developers the technical mental model to start integrating without needing the full spec.
```

---

### 8. L3-01: The Portable Envelope
**Level:** 3 | **Length:** 6 min | **Audience:** Anyone wanting to deeply understand the core manifest structure

**Why this is here:** Core concept deep dive. The foundation everything else builds on.

```
FOCUS: The complete anatomy of a Universal Manifest document. JSON-LD as the base format: @context for semantic richness, valid JSON for universal parsing. The UMID: UUID URN format, globally unique, offline-generatable, resolvable at myum.net. The subject field: DID or URI identifying who/what the manifest is about. TTL mechanics: issuedAt and expiresAt timestamps, validity window checking, why expired means rejected (no renewal mechanism). The minimal valid manifest (~300 bytes). How the envelope stays lightweight (1-3 KB typical) by using pointers instead of embedding data.

DO NOT COVER: Do not explain facet internals, consent model, signatures, or the resolver in depth — those are separate L3 videos. Do not cover specific use cases or integration scenarios. Stay on the envelope itself.

WHY THIS EXISTS: The definitive explanation of the manifest document structure, separate from what goes inside it.
```

---

### 9. L3-02: Facets and Pointers
**Level:** 3 | **Length:** 6 min | **Audience:** Developers and architects wanting to understand UM's modular data architecture

**Why this is here:** Data architecture deep dive. How information is organized inside manifests.

```
FOCUS: Facets as named, typed data compartments within the manifest. Well-known facet names: publicProfile, deviceIdentity, venuePolicy, crossWorldProfile, gameProfile. How facets are arrays of objects with @type and name fields. Pointers: URI references to authoritative external data instead of copying it. Why pointers keep manifests small and avoid stale-copy problems. Pointer names: solidPod.creatorCanonical, matrix.userId, activityPub.actor, metaverse.avatar, metaverse.socialGraph. The difference between a facet (data inside the manifest) and a pointer (reference to data outside). Extensibility: defining custom facets for new use cases.

DO NOT COVER: Do not cover consent mechanics, signatures, resolution, or the envelope structure — those are separate L3 videos. Do not discuss specific integration lane scenarios beyond brief examples.

WHY THIS EXISTS: The definitive explanation of how data is organized and referenced inside a manifest.
```

---

### 10. L3-03: Default-Deny Consent
**Level:** 3 | **Length:** 6 min | **Audience:** Anyone wanting to deeply understand UM's privacy model

**Why this is here:** Privacy deep dive. The consent architecture that makes UM trustworthy.

```
FOCUS: The consent architecture: consents as an array of objects with @type, name, and value. The four states: allowed (green), denied (red), restricted (amber), and not-set (treated as denied). Default-deny principle: if a consent is absent, the answer is no. How consent travels inside the manifest so downstream systems enforce it without calling back. Facet-level consent granularity: different permissions for different data compartments. Real examples: publicDisplay allowed, analytics.tracking denied, ar.recording.faceVisible not-set (therefore denied). How consuming systems check consent before accessing facet data.

DO NOT COVER: Do not explain the envelope structure, pointer mechanics, signatures, or resolution. Do not go deep on specific integration lanes — use brief examples only. Do not discuss compliance frameworks by name (GDPR, CCPA) — stay on the UM consent architecture itself.

WHY THIS EXISTS: The definitive explanation of how consent works as a structural, portable, default-deny system.
```

---

## Priority 3: Complete Coverage (produce next)

Fill out the full video library.

---

### 11. L2-04: Universal Manifest for Metaverse Builders
**Level:** 2 | **Length:** 2 min | **Audience:** Virtual world developers, XR platform architects, spatial computing teams

**Why this is here:** Audience-specific summary for the metaverse/XR community.

```
FOCUS: Cross-world identity portability: one manifest carries avatar, display name, social graph, and achievements across virtual worlds. Portaling: how a manifest travels through a portal from World A to World B with identity intact. The crossWorldProfile facet and metaverse pointers (avatar assets, social graph, achievements). Consent controls for metaverse contexts (voice capture, face visibility, profile publicity). How UM + IWPS together form the complete portaling stack — UM handles identity/consent, IWPS handles transport.

DO NOT COVER: Do not explain the full UM specification, JSON-LD details, or the resolver system. Do not cover non-metaverse scenarios (galleries, smart glasses privacy, device enrollment). Do not discuss standards body governance or business ROI.

WHY THIS EXISTS: Shows metaverse builders exactly how UM solves cross-world identity without needing the full spec context.
```

---

### 12. L2-05: Universal Manifest for Privacy and Compliance
**Level:** 2 | **Length:** 2 min | **Audience:** Privacy officers, compliance teams, data protection evaluators, regulators

**Why this is here:** Audience-specific summary for privacy and compliance stakeholders.

```
FOCUS: The default-deny consent model: nothing is shared unless explicitly granted. Consent travels inside the manifest, so every downstream system knows what it can and cannot do without calling back. Facet-level controls: each data compartment can have independent consent settings. Smart glasses scenario as a privacy exemplar (face visibility, voice recording — denied by default). Offline tolerance: TTL-based expiry means no revocation infrastructure needed, reducing data-retention surface. How UM aligns with privacy-by-design principles.

DO NOT COVER: Do not explain JSON-LD, data structures, resolver mechanics, or cryptographic signatures. Do not cover metaverse portaling, developer adoption paths, or competitive positioning against other standards. Keep it focused on the privacy and consent architecture.

WHY THIS EXISTS: Demonstrates to privacy stakeholders that consent is structural, not an afterthought bolted on top.
```

---

### 13. L3-04: Cross-World Identity and Portaling
**Level:** 3 | **Length:** 6 min | **Audience:** Metaverse developers and XR architects wanting the full portaling story

**Why this is here:** Deep dive on cross-world identity, expanding on the L2-04 summary.

```
FOCUS: The cross-world identity problem: re-registration, lost progress, fragmented social graphs across virtual worlds. How UM solves it: the crossWorldProfile facet carries avatar preferences, display name, and achievements. Metaverse pointers (metaverse.avatar, metaverse.socialGraph, metaverse.achievements) reference authoritative assets without copying them. The portaling flow: user enters a portal in World A, their manifest UMID travels to World B, World B resolves the manifest, reads the crossWorldProfile facet, loads avatar from pointer, checks metaverse consent toggles. The UM + IWPS relationship: UM provides the identity/consent envelope, IWPS provides the inter-world transport protocol. Together they form the complete portaling stack.

DO NOT COVER: Do not explain the general UM envelope, consent model in full, or signature mechanics — those are separate L3 videos. Do not cover non-metaverse scenarios. Do not describe IWPS protocol internals beyond the complementarity relationship.

WHY THIS EXISTS: The definitive explanation of how manifests enable persistent identity across virtual worlds.
```

---

### 14. L3-05: Manifest Resolution
**Level:** 3 | **Length:** 6 min | **Audience:** Developers and integrators wanting to understand the resolver system

**Why this is here:** Deep dive on the resolver and manifest lookup system.

```
FOCUS: The resolution problem: how does a consumer get a manifest when they only have a UMID? The myum.net resolver: a lookup service where manifests are published and fetched by UMID. The publish flow: issuer pushes manifest to myum.net. The resolve flow: consumer sends UMID to myum.net/{UMID}, receives the manifest. Always-current guarantee: the resolver serves the latest published version. Transport agnosticism: manifests can also be shared via QR code, Bluetooth, API call, or file transfer — the resolver is one option, not the only path. How resolution fits into the validate-then-consume lifecycle. The provenance chain: fetched manifest still requires TTL check, signature verification, and consent checking by the consumer.

DO NOT COVER: Do not explain the manifest structure, facets, consent model, or signatures in depth — reference them briefly. Do not discuss resolver implementation details (Cloudflare Workers, caching strategy). Stay at the specification level.

WHY THIS EXISTS: The definitive explanation of how manifests are published and looked up across the network.
```

---

### 15. L3-06: Signatures and Integrity
**Level:** 3 | **Length:** 6 min | **Audience:** Security-minded developers and architects wanting the trust model

**Why this is here:** Deep dive on cryptographic integrity and tamper detection.

```
FOCUS: The tamper-detection problem: how does a consumer know a manifest has not been modified in transit? The v0.2 signature profile: JCS (JSON Canonicalization Scheme, RFC 8785) for deterministic serialization, Ed25519 for compact and fast cryptographic signatures. The signing flow: canonicalize the manifest payload with JCS, sign with the issuer's Ed25519 private key, embed the signature block in the manifest. The verification flow: extract the signature, re-canonicalize the payload, verify with the issuer's public key. Modular signature profiles: consumers verify the profiles they support, safely ignore unknown ones — forward compatibility. What signatures do not cover: they prove integrity and issuer identity, not consent or freshness (those are separate checks).

DO NOT COVER: Do not explain the full manifest structure, facets, consent, or resolution — reference briefly. Do not discuss specific key management infrastructure, PKI choices, or DID method details. Do not cover v0.1 (which has no signature support).

WHY THIS EXISTS: The definitive explanation of how cryptographic integrity works in UM v0.2.
```

---

### 16. L3-08: Integration Lanes Overview
**Level:** 3 | **Length:** 6 min | **Audience:** Product managers and integrators evaluating which UM integration paths are relevant

**Why this is here:** The survey of all integration possibilities so evaluators can pick their lanes.

```
FOCUS: Survey of all major integration lanes: gallery/venue display (manifest-driven art display with consent and content policy), smart glasses (AR/XR consent enforcement for recording and face visibility), metaverse portaling (cross-world identity via IWPS + UM), proof of personhood (multi-provider human verification without personal data exposure), social profile portability (one profile across platforms), device enrollment (edge devices auto-configure from manifest policies), and professional credentials (portable licenses and certifications). For each lane: the problem it solves, which facets/consents are involved, and the current status (proven in fixtures vs. conceptual).

DO NOT COVER: Do not go deep on any single lane — each gets approximately 45 seconds. Do not explain the underlying data structures or consent mechanics in detail. Do not discuss implementation specifics or code. This is the menu, not the meal.

WHY THIS EXISTS: The single survey of all integration possibilities so evaluators can identify which lanes matter to them.
```

---

## Quick Reference

| # | ID | Title | Length | Priority |
|---|-----|-------|--------|----------|
| 0 | L3-10 | Facet Privacy — Public, Encrypted, and Selective Disclosure | 6 min | OMA3 Meeting |
| 1 | L2-03 | UM for Standards Bodies | 2 min | OMA3 Meeting |
| 2 | L3-09 | IWPS + UM: The Complete Portaling Stack | 6 min | OMA3 Meeting |
| 3 | L1-01 | Everything You Need to Know About UM | 6 min | OMA3 Meeting |
| 4 | L3-07 | The Composite Stack Architecture | 6 min | OMA3 Meeting |
| 5 | L3-05-DEEP | The myum.net Resolver Deep Dive | 6 min | OMA3 Meeting |
| 6 | L3-11 | Hashing, Caching, and Data Bundling Deep Dive | 6 min | OMA3 Meeting |
| 7 | L0-01 | Welcome to Universal Manifest | 2 min | Core Library |
| 8 | L2-01 | UM for Executives | 2 min | Core Library |
| 9 | L2-02 | UM for Developers | 2 min | Core Library |
| 10 | L3-01 | The Portable Envelope | 6 min | Core Library |
| 11 | L3-02 | Facets and Pointers | 6 min | Core Library |
| 12 | L3-03 | Default-Deny Consent | 6 min | Core Library |
| 13 | L2-04 | UM for Metaverse Builders | 2 min | Complete Coverage |
| 14 | L2-05 | UM for Privacy and Compliance | 2 min | Complete Coverage |
| 15 | L3-04 | Cross-World Identity and Portaling | 6 min | Complete Coverage |
| 16 | L3-05 | Manifest Resolution | 6 min | Complete Coverage |
| 17 | L3-06 | Signatures and Integrity | 6 min | Complete Coverage |
| 18 | L3-08 | Integration Lanes Overview | 6 min | Complete Coverage |
