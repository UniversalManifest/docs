# OMA3 Architectural Overview Presentation

**Date:** 2026-03-12
**Audience:** Alfred Tom and OMA3 evaluation group (IWPS context)
**Duration:** ~13 minutes (9 sections)
**Objective:** Present Universal Manifest architecture -- data structures, file formats, consent model, and integrity layer -- and show how UM complements IWPS as the portable state payload for inter-world portaling.
**Tone:** Authoritative, collaborative, specification-focused. UM is a standard, not a product.

---

## Section 1: The Problem (1 min)

### Key Points

- Every pair of systems that needs to exchange user state today builds a custom integration. Social profiles, device registrations, privacy preferences, verified credentials -- all stored in different formats, in different places, with no shared structure.
- Point-to-point API integrations create a fragile web that doesn't scale. Adding one new system means building N new integrations.
- There is no standard for portable state -- a document that carries identity, consent, and credentials between systems without prior bilateral agreement.
- This fragmentation costs engineering effort, creates privacy blind spots (consent doesn't travel), and blocks interoperability between platforms.

### Visual Suggestion

Diagram showing isolated platform silos (social, enterprise, spatial, IoT) connected by a tangled web of point-to-point arrows. Each arrow represents a custom integration. The visual communicates: this doesn't scale.

### NotebookLM Brief

> Focus on the data fragmentation problem across platforms. Emphasize that point-to-point integrations don't scale and that no standard exists for portable state (identity + consent + credentials in one document). Keep it abstract and platform-neutral. Do NOT name specific platforms or competitors. Do NOT discuss solutions yet -- this section is problem-only.

---

## Section 2: What Is Universal Manifest (2 min)

### Key Points

- Universal Manifest (UM) is a portable JSON-LD document format -- a standardized envelope that carries identity, credentials, preferences, and consent between systems.
- Every manifest has a UMID (Universal Manifest Identifier), a UUID-based URN (`urn:uuid:...`) that provides global identification without a central registry. Any system can look up a manifest by its UMID through the resolver at `myum.net`.
- Built-in TTL via `issuedAt` and `expiresAt` timestamps. This makes manifests offline-tolerant: a caching device knows exactly when to stop trusting the document without needing to call home for revocation checks.
- The `subject` field binds the manifest to an identity using a DID or URI. The manifest says: this is who this data is about.
- Any system that can parse JSON can consume a manifest. Systems that understand JSON-LD get richer, unambiguous semantics through the `@context`.

### Visual Suggestion

A clean JSON document showing the root structure: `@context`, `@type`, `id` (UMID), `issuedAt`, `expiresAt`, `subject`. Annotations call out each field's purpose. The document looks simple and approachable -- not a wall of code.

### NotebookLM Brief

> Introduce Universal Manifest as a portable JSON-LD state envelope. Cover four elements: UMID (UUID URN for global ID), TTL (issuedAt/expiresAt for offline tolerance), subject (DID/URI for identity binding), and JSON-LD context for semantic richness. Frame UM as a specification and document format. Do NOT mention TypeScript, npm, or any specific programming language. Do NOT discuss internal data structures yet -- that is the next section.

---

## Section 3: Data Structures -- Facets and Pointers (2 min)

### Key Points

- **Facets** are named, modular data compartments inside a manifest. Each facet carries a specific slice of data: `publicProfile`, `deviceIdentity`, `venuePolicy`, `gameProfile`, etc. Think of them as functional modules that can be mixed, matched, and extended.
- **Pointers** are URIs referencing external authoritative data. Instead of embedding a 50 MB 3D avatar into the manifest, include a pointer URL to where the avatar lives at its canonical source. This is the difference between photocopying a document and handing out a business card.
- This pointer-first design keeps manifests lightweight -- typically 1-3 KB -- small enough for QR codes, Bluetooth, or edge-device caching.
- Facets are extensible. Well-known names exist (`publicProfile`, `deviceIdentity`, `canonicalProfilePointer`), but any adopter can define domain-specific facets for their use case.
- Consumers read the facets they understand and safely ignore the rest (forward compatibility).

### Visual Suggestion

Exploded-view diagram of a manifest envelope. The envelope opens to reveal modular facet compartments (color-coded). One facet is magnified to show a pointer URL instead of raw data, with an arrow pointing to an external data source. Size comparison: manifest (1-3 KB) vs. the assets it points to (MBs/GBs).

### NotebookLM Brief

> Cover the two core data structures: facets (named modular compartments like publicProfile, deviceIdentity) and pointers (URIs referencing external authoritative data instead of embedding it). Emphasize the pattern: facets organize, pointers reference, manifests stay small (1-3 KB). Do NOT list every possible facet name -- focus on the extensible pattern. Do NOT discuss consent or signatures -- those are separate sections.

---

## Section 4: Consent Model (1 min)

### Key Points

- UM uses a **default-deny** consent model. If a specific permission isn't explicitly granted within the manifest, the receiving system must treat it as denied.
- Consent travels inside the manifest envelope. Every downstream system that receives the manifest immediately knows what it's allowed to do with the data -- without calling back to the issuing system.
- Three consent states: **allowed** (explicitly granted), **denied** (explicitly refused), and **not-set** (treated as denied by default). There is no ambiguity.
- This makes privacy compliance portable. Consent decisions follow the data, not the platform.

### Visual Suggestion

Lock icon next to data fields. A simple three-state indicator: green (allowed), red (denied), grey (not-set = denied). The visual emphasizes that the default state is locked/denied.

### NotebookLM Brief

> Cover the default-deny consent model: if a permission isn't explicitly granted, it's denied. Three states: allowed, denied, not-set (= denied). Consent travels inside the envelope so downstream systems know permissions without calling back. Frame as portable privacy compliance. Do NOT mention GDPR, cookie banners, or any specific regulation. Do NOT discuss implementation details of how consent is stored.

---

## Section 5: Integrity and Signatures (1 min)

### Key Points

- The v0.2 specification draft adds cryptographic signatures using **Ed25519** combined with **JCS (JSON Canonicalization Scheme, RFC 8785)** for deterministic serialization.
- Signature profiles are modular: a consuming system verifies the profiles it supports and safely ignores unknown ones. This preserves forward compatibility.
- Unknown fields in a signed manifest are preserved, not rejected. A system doesn't need to understand every field to verify the signature over the fields it does understand.
- The signature proves the manifest hasn't been tampered with in transit and was issued by the claimed source -- like a notary stamp on a document.

### Visual Suggestion

A JSON document flowing through a "JCS Canonicalization" step, then stamped with an "Ed25519 Signature" seal. The visual conveys: canonicalize, then sign, then verify.

### NotebookLM Brief

> Cover v0.2 signatures: Ed25519 + JCS canonicalization for deterministic signing. Emphasize modular signature profiles (verify what you support, ignore what you don't) and forward compatibility (unknown fields preserved, not rejected). Frame as integrity assurance, like a notary stamp. Do NOT deep-dive into Ed25519 key generation, JCS algorithm internals, or cryptographic implementation specifics.

---

## Section 6: The Composite Stack (1 min)

### Key Points

- UM operates within a three-layer composite stack:
  1. **Storage/Registry** -- where canonical data lives (databases, Solid Pods, any persistent store)
  2. **Transit/State Envelope** -- Universal Manifest (the portable document that moves between layers)
  3. **Execution/Runtime** -- where data is consumed and acted upon (web apps, native clients, spatial engines)
- UM is the **transit layer**. It doesn't replace your storage and it doesn't replace your runtime. It bridges them.
- This architecture is storage-agnostic and runtime-agnostic. UM works with any storage backend and any execution environment.

### Visual Suggestion

Three-layer horizontal stack diagram. Storage at the bottom, UM (Transit/State Envelope) in the middle, Execution/Runtime at the top. Arrows show data flowing up through UM from storage to runtime. The middle layer is highlighted as the focus.

### NotebookLM Brief

> Cover the three-layer composite stack: Storage/Registry (bottom), Transit/State Envelope = UM (middle), Execution/Runtime (top). UM is the transit layer that bridges storage and runtime without replacing either. Frame as architecture-agnostic -- works with any storage backend and any runtime environment. Do NOT name specific storage or runtime products as required dependencies.

---

## Section 7: How UM Fits Into IWPS (2 min) -- THE KEY SECTION

### Key Points

- **IWPS is the transport plumbing**: it defines the communication protocol for inter-world portaling via two API calls (Query and Teleport). It handles capability negotiation, session binding, and communication paths between source and destination worlds.
- **UM is the cargo**: it defines what travels with the user -- identity, consent, facets, pointers, credentials, and validity metadata.
- IWPS v0.3 has a TBD `assets` parameter in its Teleport API. UM fills this gap precisely -- the manifest *is* the asset payload.
- **Integration flow**: Source world initiates Portal -> Query call includes UMID for the traveling subject -> Destination fetches/resolves the manifest -> Teleport call carries identity, consent, and asset references from the manifest -> Destination projects the user with their portable state intact.
- **What UM adds to IWPS**: consent that travels with the user, modular facets for extensible data, pointers to authoritative assets, TTL for offline tolerance, and cryptographic signatures for integrity.
- **What IWPS adds to UM**: capability negotiation between worlds, standardized communication paths, session binding at the destination, and a defined transport protocol for the portaling event.
- Together, IWPS + UM form a complete portaling stack: IWPS handles the "how do I get there" and UM handles the "what comes with me."

### Visual Suggestion

Two-column diagram. Left column: IWPS (Query API, Teleport API, capability negotiation, session binding -- labeled "Transport/Plumbing"). Right column: UM (identity, consent, facets, pointers, TTL, signatures -- labeled "Cargo/Payload"). Arrows connect them at the integration point: IWPS's `assets` parameter links to UM's manifest. A flow diagram below shows: Source World -> Query (UMID) -> Destination -> Resolve Manifest -> Teleport (with UM payload) -> Arrival with state.

### NotebookLM Brief

> THE KEY SECTION. Frame IWPS as transport plumbing (Query + Teleport APIs, capability negotiation, session binding) and UM as cargo (identity, consent, facets, pointers, TTL, signatures). IWPS's TBD assets parameter is where UM fits. Walk through the integration flow: Portal -> Query with UMID -> resolve manifest -> Teleport with payload. Show mutual value: UM adds consent/facets/pointers/TTL/signatures; IWPS adds negotiation/transport/sessions. Do NOT frame UM as replacing IWPS. Do NOT criticize IWPS's TBD sections -- frame them as collaboration opportunities.

---

## Section 8: Hackathon Demo (2 min)

### Key Points

- A hackathon proof-of-concept validated the core UM concepts in a live spatial environment.
- A portal server (running on port 3333) resolved Universal Manifests for users entering a Three.js-based 3D space. The resolver looked up manifests by UMID and returned the full portable state envelope.
- The implementation handled dual-format normalization: both UM v0.1 manifests and Manifest Commons format, demonstrating interoperability across document formats.
- Avatars were loaded from pointer URLs in the manifest -- the 3D space didn't store avatar data, it followed the manifest's pointers to the canonical source.
- Identity traversed across renderers: the same UMID and subject identity worked across different rendering contexts within the spatial environment.
- Consent was checked at runtime by consuming systems before rendering profile data or enabling features like voice capture.

### Visual Suggestion

Screenshot or diagram of the hackathon setup: Portal Server (port 3333) in the center, connected to a Three.js 3D space on one side and a manifest resolver on the other. Arrows show the flow: user enters portal -> UMID resolved -> manifest returned -> avatar loaded from pointer -> consent checked -> user projected into the space.

### NotebookLM Brief

> Cover the hackathon proof-of-concept that validated UM in a spatial environment. Portal server resolved manifests by UMID for a Three.js 3D space. Key demonstrations: dual-format normalization (UM v0.1 + Manifest Commons), avatar loading via pointer URLs, identity traversal across renderers, and runtime consent checking. Do NOT mention PeerMesh as a product -- frame as "a hackathon proof-of-concept." Do NOT position the hackathon code as production-ready or as the reference implementation.

---

## Section 9: Next Steps / Call to Action (1 min)

### Key Points

- **Publish UM as an OMA3 standard** that complements IWPS. UM fills the portable-state and asset-transfer gaps that IWPS has identified as TBD.
- **Position UM as the payload format** for IWPS's Asset Transfer Framework. The manifest becomes the standardized answer to "what travels with the user during a portal event."
- **Collaborate on spec alignment**: work together to define how UMID integrates with IWPS's Query and Teleport parameters, how consent maps to IWPS's capability negotiation, and how pointer resolution interacts with IWPS's communication paths.
- The goal is two complementary specifications maintained by OMA3, not competing standards.

### Visual Suggestion

A simple roadmap graphic with three milestones: (1) Publish UM as OMA3 standard, (2) Define IWPS + UM integration points, (3) Collaborate on aligned spec evolution. The OMA3 logo ties them together.

### NotebookLM Brief

> Cover three next steps: (1) publish UM as an OMA3 standard complementing IWPS, (2) position UM as the payload format for IWPS's Asset Transfer Framework, (3) collaborate on aligning the two specs (UMID in Query/Teleport params, consent-to-capability mapping, pointer resolution). Frame as partnership, not competition. Do NOT make commitments or promises about timelines. Do NOT discuss internal roadmap items beyond the OMA3 collaboration scope.

---

## Appendix: Terminology Quick Reference

| Term | Definition |
|------|-----------|
| **UM** | Universal Manifest -- the specification and portable document format |
| **UMID** | Universal Manifest Identifier -- UUID-based URN for global identification |
| **Facets** | Named, modular data compartments inside a manifest |
| **Pointers** | URIs referencing external authoritative data |
| **TTL** | Time-to-live via `issuedAt`/`expiresAt` timestamps |
| **IWPS** | Inter-World Portaling Standard (OMA3) |
| **OMA3** | Open Metaverse Alliance for Web3 (the consortium) |
| **OMATrust** | OMA3 product/protocol references |
| **JCS** | JSON Canonicalization Scheme (RFC 8785) |

## Appendix: Presentation Flow Summary

| # | Section | Duration | Core Message |
|---|---------|----------|-------------|
| 1 | The Problem | 1 min | Data fragmentation; point-to-point doesn't scale |
| 2 | What Is UM | 2 min | JSON-LD envelope with UMID, TTL, subject binding |
| 3 | Facets and Pointers | 2 min | Modular compartments + lightweight URI references |
| 4 | Consent Model | 1 min | Default-deny; consent travels with the data |
| 5 | Integrity and Signatures | 1 min | Ed25519 + JCS; modular, forward-compatible |
| 6 | Composite Stack | 1 min | Transit layer between storage and runtime |
| 7 | UM + IWPS | 2 min | Plumbing (IWPS) + Cargo (UM) = complete portaling |
| 8 | Hackathon Demo | 2 min | Proof-of-concept validated concepts in spatial env |
| 9 | Next Steps | 1 min | Publish, position, collaborate |
