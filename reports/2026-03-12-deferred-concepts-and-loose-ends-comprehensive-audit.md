# Deferred Concepts and Loose Ends -- Comprehensive Audit

**Date:** 2026-03-12
**Purpose:** Single catalog of everything not yet integrated into the Universal Manifest specification. Prepared for the OMA3 meeting on 2026-03-12.
**Scope:** All deferred concepts, open work orders, research-first tracks, proposed extensions, architecture decisions pending, standards alignment gaps, unprocessed inbox items, concept documents not yet integrated, integration lane gaps, and operational gaps.

---

## Summary Statistics

- **Total deferred items:** 62
- **By category:**
  - Specification gaps: 8
  - Open work orders (NOT_STARTED or IN_PROGRESS): 3
  - Research-first tracks (PIP-RS / MUM-RS): 10
  - Proposed extensions (from deep dives): 9
  - Architecture decisions pending: 7
  - Standards alignment gaps: 7
  - Unprocessed inbox items: 6
  - Concept documents not yet integrated: 3
  - Integration lane gaps: 5
  - Operational/infrastructure gaps: 4

---

## 1. Specification Gaps (things the spec should address but does not yet)

### 1.1 No encryption profile in v0.1 or v0.2

- **What:** All facets are plaintext. There is no normative encryption mechanism for private data within a manifest document. Privacy is enforced only through consent toggles (policy signals) and the projection model (derived manifests).
- **Where documented:** `docs/explainers/facet-encryption-deep-dive.md` (sections 1-2), `docs/workorders/WO-0143-private-encrypted-inline-facets-vs-projection-model-analysis.md`
- **Status:** Proposed (WO-0143 NOT_STARTED). Deep dive completed (WO-0153).
- **Blocking?:** Does not block v0.2 adoption, but blocks use cases requiring cryptographic privacy at rest.
- **Priority assessment:** P0 -- foundational spec gap for sensitive data handling.

### 1.2 No revocation protocol beyond HTTP 410

- **What:** Revocation is handled only by the resolver returning HTTP 410 Gone. There is no batch revocation mechanism, no revocation list, and no standardized revocation notification protocol. The `signature.statusRef` and `signature.revocationCursor` fields exist in the v0.2 signature profile as optional metadata, but no normative protocol defines how they are consumed.
- **Where documented:** `spec/v0.2/SIGNATURE-PROFILE.md` (sections 5.2, 6), `docs/explainers/hashing-and-data-bundling-deep-dive.md` (section 7)
- **Status:** Deferred. Bitstring status lists identified as future consideration.
- **Blocking?:** Does not block current adoption. Blocks scaled ecosystems with many manifests.
- **Priority assessment:** P1 -- important for ecosystem scale.

### 1.3 No content integrity for pointer targets (digestMultibase)

- **What:** Pointer URIs are signed (changing the URI breaks the manifest signature), but the content at the target URI is not hash-bound. A CDN compromise or MITM could substitute pointer target content undetected.
- **Where documented:** `docs/explainers/hashing-and-data-bundling-deep-dive.md` (sections 2, 5)
- **Status:** Proposed. `digestMultibase` on pointers recommended but not yet in spec.
- **Blocking?:** No. Pointer-first architecture works without it. Creates integrity gap for high-security use cases.
- **Priority assessment:** P1 -- important extension for trust-critical deployments.

### 1.4 No context integrity (digestMultibase on @context)

- **What:** The `@context` URLs reference JSON-LD context documents that define semantic meaning. If a context document is tampered with, the interpretation of the manifest changes. No hash-pinning mechanism exists.
- **Where documented:** `docs/explainers/hashing-and-data-bundling-deep-dive.md` (section 5)
- **Status:** Proposed. Aligned with W3C VC Data Integrity approach.
- **Blocking?:** No. Context URLs are on domains the project controls.
- **Priority assessment:** P2 -- defense-in-depth measure.

### 1.5 No permissions firewall / audience-scoped consent in spec

- **What:** The current `consents` array uses simple name/value pairs. The adopted v0.3+ direction (permissions firewall model) adds audience matching, context scoping, and per-rule TTL, but none of this is normative yet.
- **Where documented:** `docs/design/PERMISSIONS-FIREWALL-DESIGN.md`, `docs/DECISIONS.md` (2026-03-03 decision)
- **Status:** Architecture direction adopted. Non-normative until promoted to `spec/v0.3/`.
- **Blocking?:** No. Current consent model is sufficient for baseline interop. Blocks sophisticated per-audience consent use cases.
- **Priority assessment:** P1 -- important for real-world deployment complexity.

### 1.6 No Data Integrity proof profile (W3C VC ecosystem alignment)

- **What:** v0.2 uses JCS + Ed25519 (signs the JSON representation). A future Data Integrity profile would sign the RDF graph meaning using RDFC-1.0 canonicalization. This is noted as additive, not replacing the current profile.
- **Where documented:** `spec/v0.2/SIGNATURE-PROFILE.md` (sections 0, 8)
- **Status:** Deferred. Explicitly documented as "future, not v0.2."
- **Blocking?:** No. JCS + Ed25519 is sufficient for current adoption.
- **Priority assessment:** P2 -- needed for deep W3C VC ecosystem alignment.

### 1.7 No resolver write API or self-service registration

- **What:** Publishing a manifest to the resolver requires direct KV manipulation via Cloudflare dashboard or Wrangler CLI. There is no programmatic write API and no self-service registration UI.
- **Where documented:** `docs/explainers/resolver-deep-dive.md` (section 8), `docs/reports/2026-02-23-remaining-work-to-final-vision.md`
- **Status:** Acknowledged gap. The proposed "equip interface" and myum.net expansion would address this.
- **Blocking?:** Blocks third-party self-service publishing. Does not block spec adoption.
- **Priority assessment:** P1 -- critical for any ecosystem beyond the project maintainers.

### 1.8 No authenticated/private resolution profile

- **What:** The resolver assumes all manifests are publicly readable. There is no access control, authentication, or authorization on resolution. Private or authenticated resolution is explicitly out of scope for the current contract version.
- **Where documented:** `docs/explainers/resolver-deep-dive.md` (section 8), `docs/security/THREAT-MODEL.md`
- **Status:** Deferred. Recognized as a future profile needing separate design.
- **Blocking?:** No. Blocks private manifest use cases.
- **Priority assessment:** P2 -- needed for enterprise and healthcare scenarios.

---

## 2. Open Work Orders (NOT_STARTED or IN_PROGRESS)

### 2.1 WO-0142 -- Payment Handles and Fiat/Crypto Gateway Integration

- **What:** Create explicit standard pointers/overlays for fiat (Stripe/PayPal) and crypto gateways, establishing universal payment handle integration without leaking financial data.
- **Where documented:** `docs/workorders/WO-0142-payment-handles-and-fiat-crypto-gateway-integration.md`
- **Status:** NOT_STARTED (since 2026-03-07)
- **Blocking?:** Blocks the payments gap identified in both UM and IWPS. Does not block OMA3 presentation.
- **Priority assessment:** P1 -- IWPS alignment analysis identifies payments as a joint development area with OMA3.

### 2.2 WO-0143 -- Private Encrypted Inline Facets vs Projection Model Analysis

- **What:** Deep architectural analysis comparing the projection model with encrypted inline facets. Addresses projection lifecycles, key rotation, and ensuring multiple valid universal fallback methods.
- **Where documented:** `docs/workorders/WO-0143-private-encrypted-inline-facets-vs-projection-model-analysis.md`
- **Status:** NOT_STARTED (since 2026-03-07). Research foundation completed in WO-0153 (facet encryption deep dive).
- **Blocking?:** Blocks the architectural decision on encryption approach for the spec.
- **Priority assessment:** P1 -- foundational for private data handling strategy.

### 2.3 WO-0145 -- Vignette Video Library

- **What:** Create a dedicated library of Universal Manifest vignette explainers for UI integration and YouTube publishing. UI audit complete, 5 priority vignette scripts delivered (V-01 through V-05), production workflow documented.
- **Where documented:** `docs/workorders/WO-0145-vignette-video-library.md`
- **Status:** IN_PROGRESS. Partially superseded by WO-0149 (video hierarchy of discovery).
- **Blocking?:** No. Content creation, not spec work.
- **Priority assessment:** P2 -- marketing and adoption support.

---

## 3. Research-First Tracks (explicitly deferred to research)

### Portable Identity Profile (PIP-RS) Research-First Tracks

All five PIP-RS tracks are NOT_STARTED. Defined in `docs/reports/2026-03-05-portable-identity-profile-comprehensive-human-review-report.md`.

### 3.1 PIP-RS-01 -- Encrypted Private Fragment Profile

- **What:** Define an interoperable profile for private data handling in manifests -- packaging model, key distribution, signature/canonicalization interactions with encrypted sections.
- **Status:** NOT_STARTED
- **Blocking?:** Blocks encrypted facet normative adoption.
- **Priority assessment:** P1 -- directly feeds WO-0143.

### 3.2 PIP-RS-02 -- Selective Disclosure / ZK Proof Profile

- **What:** Select and validate a practical proof approach (BBS+, SD-JWT, or other) for minimal disclosure. Covers proof binding in UM, replay/privacy guarantees.
- **Status:** NOT_STARTED
- **Blocking?:** Blocks privacy-preserving credential presentation claims.
- **Priority assessment:** P1 -- BBS+ is W3C CR; SD-JWT is IETF RFC 9901.

### 3.3 PIP-RS-03 -- Wallet Recovery Profile

- **What:** Define minimum interoperable metadata for wallet recovery without coupling to wallet-vendor internals.
- **Status:** NOT_STARTED
- **Blocking?:** No. Blocks real-world resilience claims.
- **Priority assessment:** P2 -- operational concern, not spec blocker.

### 3.4 PIP-RS-04 -- Wallet Protocol Binding Profile

- **What:** Define a protocol-agnostic state model for UM payload portability across OIDC4VP, OIDC4VCI, and DIDComm transport families.
- **Status:** NOT_STARTED
- **Blocking?:** Blocks interoperability claims across presentation protocol families.
- **Priority assessment:** P1 -- needed for proximity and wallet integration.

### 3.5 PIP-RS-05 -- Avatar Translation Profile

- **What:** Cross-engine avatar portability metadata conventions -- anchor formats, minimum translation facet shape, runtime-agnostic viability.
- **Status:** NOT_STARTED
- **Blocking?:** No. Blocks cross-platform avatar fidelity claims.
- **Priority assessment:** P2 -- relevant to OMA3/IWPS portaling scenarios.

### Metaverse Universal Manifest (MUM-RS) Research-First Tracks

All five MUM-RS tracks are NOT_STARTED. Defined in `docs/reports/2026-03-05-metaverse-universal-manifest-comprehensive-human-review-report.md`.

### 3.6 MUM-RS-01 -- Selective Disclosure and Compliance Proof Profile

- **What:** Select a proof system for privacy-preserving compliance checks (e.g., age verification without PII exposure). Covers UM claim/proof binding, replay/substitution mitigation.
- **Status:** NOT_STARTED
- **Blocking?:** Blocks metaverse compliance proof claims.
- **Priority assessment:** P1 -- directly relevant to OMA3 portaling with age-gated content.

### 3.7 MUM-RS-02 -- Anti-Cloning and Holder-Binding Profile

- **What:** Reduce manifest theft/copy misuse without eliminating portability. Holder-binding methods, risk-tier policies, low-capability fallback behavior.
- **Status:** NOT_STARTED
- **Blocking?:** No. Blocks anti-fraud claims.
- **Priority assessment:** P2 -- security hardening.

### 3.8 MUM-RS-03 -- Platform Attestation and Secure Enclave Profile

- **What:** Standard way to describe requester trust posture for high-trust requests. Abstract attestation evidence model, trust-level semantics, optional secure enclave metadata conventions.
- **Status:** NOT_STARTED
- **Blocking?:** No. Blocks high-trust verification scenarios.
- **Priority assessment:** P2 -- aligns with OMA3 Security Certification tiers.

### 3.9 MUM-RS-04 -- Synchronization Conflict-Resolution Protocol

- **What:** Versioning model and deterministic conflict rules for concurrent manifest updates across multiple worlds/agents.
- **Status:** NOT_STARTED
- **Blocking?:** Blocks multi-device / multi-world real-time consistency claims.
- **Priority assessment:** P1 -- critical for live multi-world portaling scenarios.

### 3.10 MUM-RS-05 -- Social/Reputation Portability Profile

- **What:** Consistent schema and provenance conventions for social graph pointers and reputation signals across worlds.
- **Status:** NOT_STARTED
- **Blocking?:** No. Blocks cross-world reputation continuity claims.
- **Priority assessment:** P2 -- important for social metaverse use cases.

---

## 4. Proposed Extensions (proposed in deep dives but not adopted)

### 4.1 JWE per-facet encryption (Method 1)

- **What:** Encrypt individual facets as JWE objects (RFC 7516) using ECDH-ES+A256KW / A256GCM with X25519 key agreement. Multi-recipient support via JWE JSON Serialization. Recommended as primary encryption method.
- **Where documented:** `docs/explainers/facet-encryption-deep-dive.md` (section 3, Method 1)
- **Status:** Proposed. Recommended by research. Not in spec.
- **Blocking?:** No.
- **Priority assessment:** P1 -- the recommended primary encryption approach.

### 4.2 BBS+ selective disclosure (Method 2)

- **What:** Multi-message signature scheme on BLS12-381 curves for unlinkable presentation privacy. Each N-Quad from canonicalized JSON-LD becomes a separate BBS message; holder generates ZK proof revealing selected quads.
- **Where documented:** `docs/explainers/facet-encryption-deep-dive.md` (section 3, Method 2)
- **Status:** Research-first. W3C Candidate Recommendation. Explicitly marked as uncertain.
- **Blocking?:** No. Contingent on W3C spec finalization and library maturity.
- **Priority assessment:** P2 -- requires BLS12-381 (separate key infrastructure from Ed25519).

### 4.3 SD-JWT selective disclosure (Method 3)

- **What:** IETF RFC 9901 selective disclosure for JWT-compatible systems. Bridge profile for OIDC, EU eIDAS, enterprise systems.
- **Where documented:** `docs/explainers/facet-encryption-deep-dive.md` (section 3, Method 3)
- **Status:** Research-first. Full IETF standard. Relevant for interop bridges, not native format.
- **Blocking?:** No.
- **Priority assessment:** P2 -- bridge profile for JWT ecosystem interop.

### 4.4 CBOR-LD + COSE binary encoding profile

- **What:** Binary encoding of JSON-LD manifests using CBOR-LD for 60%+ compression. Relevant for NFC, QR, BLE transports. Paired with COSE_Sign1 for binary signing.
- **Where documented:** `docs/explainers/hashing-and-data-bundling-deep-dive.md` (sections 4, 7)
- **Status:** Deferred. Contingent on CBOR-LD reaching W3C Recommendation and having production-grade implementations in at least three languages.
- **Blocking?:** No. Blocks constrained-transport use cases (NFC, BLE beacons).
- **Priority assessment:** P3 -- future. CBOR-LD is W3C Experimental Draft.

### 4.5 Merkle history for manifests

- **What:** Tamper-evident version history for each UMID using a Merkle tree. Enables audit trails, dispute resolution, and transparency verification.
- **Where documented:** `docs/explainers/hashing-and-data-bundling-deep-dive.md` (section 7)
- **Status:** Conceptual. Requires resolver architecture change (currently stateless KV).
- **Blocking?:** No.
- **Priority assessment:** P3 -- future consideration.

### 4.6 Bitstring status lists for batch revocation

- **What:** W3C Bitstring Status List (Candidate Recommendation) where each bit represents one manifest's revocation status. Single 16 KB download covers 131,072 manifests.
- **Where documented:** `docs/explainers/hashing-and-data-bundling-deep-dive.md` (section 7)
- **Status:** Deferred. Current individual HTTP 410 checks may remain more practical for UM's distributed issuer model.
- **Blocking?:** No. Only relevant at very large ecosystem scale.
- **Priority assessment:** P3 -- future.

### 4.7 CID (Content Identifier) snapshots alongside UMIDs

- **What:** Content-addressed identifiers for immutable manifest snapshots. Would enable deduplication, verifiable history, and IPFS interop.
- **Where documented:** `docs/explainers/hashing-and-data-bundling-deep-dive.md` (section 4)
- **Status:** Deferred. No concrete use case yet justifies the added complexity.
- **Blocking?:** No.
- **Priority assessment:** P3 -- future.

### 4.8 Portal loading content pointers

- **What:** Four new pointer names for destination-world loading content during portal transitions: `metaverse.portal.loadingScreen`, `metaverse.portal.loadingBranding`, `metaverse.portal.loadingInstructions`, `metaverse.portal.estimatedLoadTime`.
- **Where documented:** `docs/MANDATE-portal-loading-content.md`, `integrations/metaverse.md` (line 120+), `docs/reports/2026-03-11-iwps-um-alignment-analysis.md` (section 4, point 7)
- **Status:** CEO mandate fulfilled (WO-0152 COMPLETED). Integrated into integration lane docs. Not yet normative in spec.
- **Blocking?:** No. UX enhancement for portaling flows.
- **Priority assessment:** P1 -- CEO mandate; directly relevant to IWPS integration.

### 4.9 Encrypt-then-sign ordering convention

- **What:** Recommendation that encrypted inline facets use encrypt-then-sign ordering so all consumers can verify the signature regardless of decryption access. Not yet a normative spec requirement.
- **Where documented:** `docs/explainers/facet-encryption-deep-dive.md` (section 4)
- **Status:** Proposed. Recommended by deep dive but contingent on WO-0143 architectural decision.
- **Blocking?:** Only if encrypted facets are adopted.
- **Priority assessment:** P1 -- must be decided alongside WO-0143.

---

## 5. Architecture Decisions Pending

### 5.1 Encrypted inline facets vs projection model (WO-0143)

- **What:** The fundamental architectural decision on whether UM should support encrypted inline facets (JWE per-facet), rely solely on the projection model, or support both. Lifecycle, key rotation, revocation, and payload size trade-offs.
- **Where documented:** `docs/workorders/WO-0143-private-encrypted-inline-facets-vs-projection-model-analysis.md`, `docs/explainers/facet-encryption-deep-dive.md`
- **Status:** NOT_STARTED. Deep dive research completed but architectural decision not made.
- **Blocking?:** Blocks PIP-RS-01, normative encryption profile, and key management design.
- **Priority assessment:** P0 -- the most significant open architectural decision.

### 5.2 Federation model for resolvers

- **What:** No specification for resolver federation. No mechanism for multiple resolvers to share registrations, no gossip protocol, no resolver discovery standard beyond the well-known descriptor.
- **Where documented:** `docs/explainers/resolver-deep-dive.md` (section 8), `docs/reports/2026-03-06-federation-and-bridge-strategy-decision-package.md`
- **Status:** Acknowledged gap. Role-based federation taxonomy adopted but no protocol specified.
- **Blocking?:** Blocks decentralized resolver ecosystem.
- **Priority assessment:** P2 -- not needed for current single-resolver deployment.

### 5.3 Record-as-core-primitive vision

- **What:** Vision direction (captured 2026-02-13) that UM composition should center on a "Record" primitive with leaf/nested containers, push/pull exchange, self-declared schemas, and permissioned attributes.
- **Where documented:** `docs/DECISIONS.md` (2026-02-13 decision), `.dev/INBOX/sticky.md`
- **Status:** Vision-level guidance only. Not translated into normative spec artifacts.
- **Blocking?:** No. Would require significant spec evolution if pursued.
- **Priority assessment:** P2 -- long-term architectural direction.

### 5.4 Consent delegation model

- **What:** Can a subject delegate consent management to a trusted agent (parent, guardian, legal representative)?
- **Where documented:** `docs/design/PERMISSIONS-FIREWALL-DESIGN.md` (section 9.4)
- **Status:** Open question. Acknowledged as a future version concern.
- **Blocking?:** No. Blocks guardian/minor use cases.
- **Priority assessment:** P2 -- needed for real-world deployment.

### 5.5 Audience verification mechanism

- **What:** How does a consumer prove it matches an audience requirement in the consent rules? Options: self-declaration, verifiable credential, DID resolution.
- **Where documented:** `docs/design/PERMISSIONS-FIREWALL-DESIGN.md` (section 9.1)
- **Status:** Open question. Identified as v0.3+ concern.
- **Blocking?:** Blocks audience-scoped consent enforcement.
- **Priority assessment:** P2 -- dependent on v0.3 consent evolution.

### 5.6 Emergency override for consent

- **What:** Should the spec define a standard mechanism for emergency access that bypasses normal consent rules when the subject is incapacitated?
- **Where documented:** `docs/design/PERMISSIONS-FIREWALL-DESIGN.md` (section 9.3)
- **Status:** Open question. Policy question with ethical dimensions.
- **Blocking?:** No.
- **Priority assessment:** P3 -- future consideration.

### 5.7 TS helper package npm publication timing

- **What:** The TypeScript helper package is private/internal. No npm or public registry publishing until v0.2 artifacts are published at stable URLs and the docs site is "implementer-grade."
- **Where documented:** `docs/DECISIONS.md` (2026-02-17 decision)
- **Status:** Pending. Publication prerequisites are now met (stable URLs, implementer-grade site), but decision to publish has not been revisited.
- **Blocking?:** No. External adopters can use the spec directly.
- **Priority assessment:** P2 -- ecosystem convenience.

---

## 6. Standards Alignment Gaps (external standards not yet integrated)

### 6.1 IWPS `assets` parameter binding

- **What:** The IWPS v0.3 Query and Teleport API payloads both include an `assets` field marked "Reserved for Future Use." UM is proposed as the payload format for this field. No formal binding specification exists yet.
- **Where documented:** `docs/reports/2026-03-11-iwps-um-alignment-analysis.md` (sections 3.1, 7.3)
- **Status:** Proposed. Alignment analysis completed. OMA3 recommendation drafted.
- **Blocking?:** Blocks formal IWPS-UM integration at the spec level.
- **Priority assessment:** P0 -- the primary OMA3 meeting agenda item.

### 6.2 Joint IWPS + UM conformance profile

- **What:** A joint conformance profile for world operators: implement IWPS transport, accept UM manifests as `assets`, enforce UM consent at arrival, support graceful degradation. Could be tiered alongside OMA3 Security Certification levels.
- **Where documented:** `docs/reports/2026-03-11-iwps-um-alignment-analysis.md` (section 8.5)
- **Status:** Proposed. Recommendation in the alignment analysis.
- **Blocking?:** No. Would accelerate OMA3 adoption.
- **Priority assessment:** P1 -- important for OMA3 standardization path.

### 6.3 Proximity-aware credential presentation profile

- **What:** UM has no explicit answer for how proximity-triggered credential presentation should work across same-device, cross-device, QR, NFC, BLE, or browser/OS wallet mediation patterns.
- **Where documented:** `docs/reports/2026-03-06-proximity-credential-and-presentation-profile-assessment.md`, `docs/reports/2026-03-06-protocol-volatility-proximity-and-federation-research-first-decision-package.md` (section 4.2)
- **Status:** GAP. Classified as the clearest remaining practical gap. Public integration lane deferred until executable proof exists.
- **Blocking?:** Blocks proximity presentation claims. Dependent on OpenID4VP, W3C Digital Credentials API maturity.
- **Priority assessment:** P1 -- real-world use case gap.

### 6.4 Protocol recommendation governance needs initial population

- **What:** A standards-currency matrix and recommendation governance model has been adopted (WO-0133, COMPLETED). The matrix itself is defined but not yet populated with initial protocol family assessments.
- **Where documented:** `docs/reports/2026-03-06-protocol-recommendation-governance-and-standards-currency-matrix.md`
- **Status:** Framework complete. Initial population not done.
- **Blocking?:** Blocks evidence-based protocol family recommendations.
- **Priority assessment:** P1 -- governance infrastructure exists but is empty.

### 6.5 OpenID Federation trust model mapping

- **What:** OpenID Federation is identified as the strongest current standards-family fit for verifier/issuer trust establishment, but it does not solve subject-state portability. No mapping document exists connecting OpenID Federation trust chains to UM resolver/verifier trust posture.
- **Where documented:** `docs/reports/2026-03-06-federation-and-bridge-strategy-decision-package.md` (section 3)
- **Status:** Partial. Role identified but no integration lane or profile created.
- **Blocking?:** No.
- **Priority assessment:** P2 -- trust infrastructure alignment.

### 6.6 Real-time asset streaming (neither IWPS nor UM)

- **What:** Neither standard addresses continuous synchronization of live world state. Both are designed for discrete transfer events, not real-time replication.
- **Where documented:** `docs/reports/2026-03-11-iwps-um-alignment-analysis.md` (section 7.3)
- **Status:** Acknowledged gap in both standards.
- **Blocking?:** No. Different architectural concern (streaming vs. document).
- **Priority assessment:** P3 -- future scope, if ever.

### 6.7 Multi-party portaling

- **What:** IWPS defines single-user portal flows. UM manifests are per-subject. Group portaling (moving a party of users together) is not addressed by either standard.
- **Where documented:** `docs/reports/2026-03-11-iwps-um-alignment-analysis.md` (section 7.3)
- **Status:** Not addressed. Not currently planned.
- **Blocking?:** No.
- **Priority assessment:** P3 -- future.

---

## 7. Unprocessed Inbox Items

Source: `.dev/INBOX/` directory. Audit: `docs/reports/2026-03-11-inbox-audit-report.md`.

### 7.1 `sticky.md` -- Record-as-core-primitive concept

- **What:** Raw idea exploring records as the core UM primitive with leaf/nested containers, push/pull exchange, self-declared schemas, and permissioned attributes. Voice memo transcript.
- **Where documented:** `.dev/INBOX/sticky.md`
- **Status:** UNPROCESSED. Vision captured in `docs/DECISIONS.md` (2026-02-13) but never formalized into a design work order.
- **Blocking?:** No.
- **Priority assessment:** P2 -- long-term architectural exploration.

### 7.2 `CEO-mandate-feb-26-26.md` -- Commercial explainer production directive

- **What:** CEO directive for creating consumer-friendly animated explainer documents with characters, user journeys, and visual identity. Directly relates to WO-0145 scope.
- **Where documented:** `.dev/INBOX/CEO-mandate-feb-26-26.md`
- **Status:** UNPROCESSED. Should be consolidated with WO-0145.
- **Blocking?:** No.
- **Priority assessment:** P1 -- CEO directive.

### 7.3 `README copy.md` -- Sandbox UI/UX feedback

- **What:** Raw CEO feedback on sandbox UI/UX issues including stacking behavior, step-through experience, manifest visibility, and visual design quality. This feedback drove the V2 sandbox redesign (WO-0069 through WO-0080, now COMPLETED).
- **Where documented:** `.dev/INBOX/README copy.md`
- **Status:** UNPROCESSED as an inbox item, but the feedback has been acted on. Should be archived.
- **Blocking?:** No.
- **Priority assessment:** P3 -- archive candidate.

### 7.4 `AI agents with UM.md` -- AI agent use case

- **What:** Idea fragment for adding AI agent user journeys and use cases to the Universal Manifest. Proposes a suite of examples for how AI agents would use UM.
- **Where documented:** `.dev/INBOX/AI agents with UM.md`
- **Status:** UNPROCESSED. No formal integration lane, journey, or work order exists.
- **Blocking?:** No. Missed opportunity for a growing adoption sector.
- **Priority assessment:** P2 -- timely given AI agent ecosystem growth.

### 7.5 `permissions-system.md` -- Little Snitch-inspired firewall model

- **What:** Architecture idea for a firewall-inspired permissions system modeled on Little Snitch. Starts with zero permissions, creates rules as the world requests access, user can modify rules later.
- **Where documented:** `.dev/INBOX/permissions-system.md`
- **Status:** UNPROCESSED as inbox item. The concept has been integrated into `docs/design/PERMISSIONS-FIREWALL-DESIGN.md` (adopted as v0.3+ direction per `docs/DECISIONS.md` 2026-03-03 decision). Should be archived.
- **Blocking?:** No.
- **Priority assessment:** P3 -- already integrated conceptually, inbox item can be archived.

### 7.6 `digital-you/` -- Digital YOU research (3 files)

- **What:** Three files: a LinkedIn article by Tracey Swales describing the "Digital YOU" concept (closely aligned with UM vision, mentions Universal Manifest explicitly), a diagram outline for the Digital YOU visual (avatar + 8 capability groups), and a reference image.
- **Where documented:** `.dev/INBOX/digital-you/tracey-linkedin.md`, `.dev/INBOX/digital-you/digital_you_diagram_outline.md`, `.dev/INBOX/digital-you/image-read for more details.jpeg`
- **Status:** MIXED. The LinkedIn article validates external adoption interest. The diagram outline maps directly to UM facet categories. Neither has been formally integrated.
- **Blocking?:** No.
- **Priority assessment:** P2 -- valuable external validation and visual concept for adoption materials.

---

## 8. Concept Documents Not Yet Integrated

### 8.1 Avatar Equip Tool

- **What:** Gamified visual interface concept for building and managing a Universal Manifest, inspired by AAA game equip menus. Users "equip" data elements (facets, pointers, claims, consents) to avatar slots. Includes 3D avatar rendering, drag-and-drop management, real-time manifest preview, and resolver integration. Identified as a spec completeness forcing function.
- **Where documented:** `docs/concepts/avatar-equip-tool.md` (WO-0151, COMPLETED as concept doc)
- **Status:** Concept only. Lives in a separate repository (not part of the spec). Seven open questions documented (section 8).
- **Blocking?:** No. Consumer application, not spec work.
- **Priority assessment:** P2 -- consumer product concept that would drive spec completeness.

### 8.2 myum.net Equip Interface Proposal

- **What:** Proposal to transform myum.net from a read-only resolver into a consumer-facing platform with login, manifest management, and gamified equip interface.
- **Where documented:** `.dev/ai/proposals/2026-03-11-myum-equip-interface-proposal.md`
- **Status:** DRAFT proposal. Not approved.
- **Blocking?:** No.
- **Priority assessment:** P2 -- product direction, not spec work.

### 8.3 Spatial Fabric Hackathon Learnings (not yet normative)

- **What:** Proof-of-concept implementation validated UM concepts in a live spatial rendering environment (portal server + Three.js + ActivityPub). Demonstrated pointer-first architecture, dual-format normalization, consent enforcement, TTL management, and identity fallback chains. Directly maps to IWPS flow.
- **Where documented:** `docs/reports/2026-03-11-spatial-fabric-hackathon-learnings.md` (WO-0150, COMPLETED)
- **Status:** Report complete. Learnings documented. Concepts validated but not translated into spec changes or conformance updates.
- **Blocking?:** No.
- **Priority assessment:** P1 -- strong validation evidence for OMA3 presentation.

---

## 9. Integration Lane Gaps

### 9.1 No AI agent integration lane

- **What:** No integration lane, journey, or fixture exists for AI agent use cases despite being identified as a priority in the inbox.
- **Where documented:** `.dev/INBOX/AI agents with UM.md`
- **Status:** Idea fragment only. Not formalized.
- **Blocking?:** No. Missing market opportunity.
- **Priority assessment:** P2 -- growing ecosystem relevance.

### 9.2 Payments integration lane (IWPS TBD)

- **What:** Neither UM nor IWPS defines a complete payment portability model. UM has `prefs.financial.*` overlay family but no explicit payment handle schema. WO-0142 tracks this.
- **Where documented:** `docs/reports/2026-03-11-iwps-um-alignment-analysis.md` (section 7.3), `docs/workorders/WO-0142-payment-handles-and-fiat-crypto-gateway-integration.md`
- **Status:** NOT_STARTED. Joint IWPS + UM development area.
- **Blocking?:** Blocks payment portability in metaverse commerce.
- **Priority assessment:** P1 -- identified as natural OMA3 collaboration area.

### 9.3 Cross-chain asset ownership verification

- **What:** Both UM and IWPS can reference blockchain-based assets, but neither defines a normative on-chain verification protocol.
- **Where documented:** `docs/reports/2026-03-11-iwps-um-alignment-analysis.md` (section 7.3)
- **Status:** Not addressed. May be handled through OMATrust attestation layer.
- **Blocking?:** No.
- **Priority assessment:** P3 -- future, dependent on OMATrust evolution.

### 9.4 Education and healthcare integration lanes lack depth

- **What:** Education and healthcare are listed among the 13 integration lanes but have minimal fixture and journey coverage compared to metaverse, social, and smart glasses lanes.
- **Where documented:** `docs/CRITICAL-PATH.md` (Phase 8), integration lane files under `integrations/`
- **Status:** Documented but shallow.
- **Blocking?:** No.
- **Priority assessment:** P2 -- important for demonstrating cross-domain applicability.

### 9.5 Loading content pointers not yet tested in journey/fixture

- **What:** Portal loading content pointers (`metaverse.portal.loadingScreen`, etc.) are integrated into the integration lane docs (WO-0152 COMPLETED) but have no executable journey or conformance fixture proving the flow.
- **Where documented:** `integrations/metaverse.md` (lines 120-127), `docs/MANDATE-portal-loading-content.md`
- **Status:** Documented but not fixture-proven.
- **Blocking?:** No. UX-level enhancement.
- **Priority assessment:** P2 -- would strengthen OMA3 demonstration.

---

## 10. Operational/Infrastructure Gaps

### 10.1 No resolver rate limiting at application level

- **What:** Rate limiting is handled only by Cloudflare infrastructure, not by the resolver application code. The threat model recommends per-IP rate limiting (e.g., 100 requests/minute) but this is not implemented.
- **Where documented:** `docs/security/THREAT-MODEL.md` (section on rate limiting), `docs/explainers/resolver-deep-dive.md` (section 8)
- **Status:** Acknowledged. Deferred to future contract versions.
- **Blocking?:** No. Cloudflare provides infrastructure-level protection.
- **Priority assessment:** P3 -- operational hardening.

### 10.2 No resolver content validation on ingestion

- **What:** The resolver does not validate manifest content on ingestion or retrieval. It does not check JSON-LD validity, required fields, or spec conformance. Pass-through routing only.
- **Where documented:** `docs/explainers/resolver-deep-dive.md` (section 8)
- **Status:** By design (the resolver is deliberately a thin routing layer). Could be an optional validation mode.
- **Blocking?:** No.
- **Priority assessment:** P3 -- design choice, not gap.

### 10.3 NotebookLM knowledge vault needs rebuild

- **What:** Many new files created in recent sessions (explainers, reports, concepts, presentations, IWPS spec) are not in the current zip. The zip needs rebuilding before further video production.
- **Where documented:** `.dev/ai/handoffs/2026-03-12-03-16-54Z-handoff-universalmanifest.md` (step 2)
- **Status:** Pending. Operational task.
- **Blocking?:** Blocks video production from current content.
- **Priority assessment:** P1 -- needed for OMA3 video assets.

### 10.4 Standards-currency matrix initial population needed

- **What:** The governance mechanism exists (WO-0133 COMPLETED) but the actual matrix has not been populated with initial assessments for any protocol family.
- **Where documented:** `docs/reports/2026-03-06-protocol-recommendation-governance-and-standards-currency-matrix.md`
- **Status:** Framework complete; content empty.
- **Blocking?:** Blocks evidence-based protocol recommendations in docs.
- **Priority assessment:** P1 -- governance infrastructure without content.

---

## Cross-Reference: Items Most Relevant to OMA3 Meeting (2026-03-12)

The following items are directly relevant to the OMA3 discussion:

| # | Item | Section | Priority |
|---|------|---------|----------|
| 1 | IWPS `assets` parameter binding | 6.1 | P0 |
| 2 | Joint IWPS + UM conformance profile | 6.2 | P1 |
| 3 | Payments framework (joint gap) | 2.1, 9.2 | P1 |
| 4 | Portal loading content (mandate fulfilled, not fixture-proven) | 4.8, 9.5 | P1 |
| 5 | Multi-party portaling (gap in both standards) | 6.7 | P3 |
| 6 | Real-time asset streaming (gap in both) | 6.6 | P3 |
| 7 | Cross-chain asset ownership verification | 9.3 | P3 |
| 8 | Avatar translation profile (MUM-RS/PIP-RS) | 3.5 | P2 |
| 9 | Encrypted inline facets decision | 5.1 | P0 |
| 10 | Selective disclosure / compliance proof | 3.6 | P1 |

---

## Cross-Reference: Highest Priority Items (P0)

| # | Item | Section | Status |
|---|------|---------|--------|
| 1 | Encrypted inline facets vs projection decision | 5.1 | NOT_STARTED (WO-0143) |
| 2 | IWPS `assets` parameter binding | 6.1 | Proposed (alignment analysis complete) |
| 3 | No encryption profile in spec | 1.1 | Proposed (deep dive done, decision pending) |

---

## Source Files Consulted

This audit examined the following primary sources:

- `docs/workorders/WO-INDEX.md` and all individual WO files for NOT_STARTED/IN_PROGRESS items
- `docs/CRITICAL-PATH.md` -- phases 1-18 and future phases
- `docs/DECISIONS.md` -- all 25+ decisions including pending/deferred items
- `docs/explainers/facet-encryption-deep-dive.md` -- encryption proposals and open questions
- `docs/explainers/hashing-and-data-bundling-deep-dive.md` -- CID deferral, digestMultibase, CBOR-LD
- `docs/explainers/resolver-deep-dive.md` -- resolver limitations and boundaries
- `docs/concepts/avatar-equip-tool.md` -- equip tool concept and open questions
- `docs/MANDATE-portal-loading-content.md` -- CEO mandate for loading content
- `docs/design/PERMISSIONS-FIREWALL-DESIGN.md` -- v0.3+ consent evolution and open questions
- `docs/reports/2026-03-11-iwps-um-alignment-analysis.md` -- IWPS gaps and recommendations
- `docs/reports/2026-03-11-inbox-audit-report.md` -- inbox item inventory
- `docs/reports/2026-03-11-spatial-fabric-hackathon-learnings.md` -- hackathon validation
- `docs/reports/2026-03-06-protocol-volatility-proximity-and-federation-research-first-decision-package.md`
- `docs/reports/2026-03-06-proximity-credential-and-presentation-profile-assessment.md`
- `docs/reports/2026-03-06-federation-and-bridge-strategy-decision-package.md`
- `docs/reports/2026-03-06-protocol-recommendation-governance-and-standards-currency-matrix.md`
- `docs/reports/2026-03-05-portable-identity-profile-comprehensive-human-review-report.md` -- PIP-RS tracks
- `docs/reports/2026-03-05-metaverse-universal-manifest-comprehensive-human-review-report.md` -- MUM-RS tracks
- `docs/governance/SPEC-IMPROVEMENT-QUEUE.md` -- currently empty queue
- `docs/security/THREAT-MODEL.md` -- rate limiting and authenticated resolution gaps
- `spec/v0.1/CONFORMANCE.md` -- deferred signature interoperability
- `spec/v0.2/SIGNATURE-PROFILE.md` -- future compatibility, Data Integrity path
- `.dev/INBOX/` -- all 6 unprocessed items
- `.dev/ai/handoffs/2026-03-12-03-16-54Z-handoff-universalmanifest.md` -- latest session context
- `.dev/ai/research/2026-02-19-gap-deferred-risk-register.md` -- historical gap register
- `.dev/ai/proposals/2026-03-11-myum-equip-interface-proposal.md` -- equip interface proposal
- `integrations/metaverse.md` -- loading content pointers, lane structure
