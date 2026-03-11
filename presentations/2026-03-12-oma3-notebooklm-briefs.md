# OMA3 Presentation -- NotebookLM Section Briefs

**Date:** 2026-03-12
**Usage:** Copy-paste each brief into NotebookLM (or equivalent production agent) as a focused directive for generating section-specific audio/content.

---

## Section 1: The Problem

Focus on the data fragmentation problem across platforms. Emphasize that point-to-point integrations don't scale and that no standard exists for portable state (identity + consent + credentials in one document). Keep it abstract and platform-neutral. Do NOT name specific platforms or competitors. Do NOT discuss solutions yet -- this section is problem-only.

---

## Section 2: What Is Universal Manifest

Introduce Universal Manifest as a portable JSON-LD state envelope. Cover four elements: UMID (UUID URN for global ID), TTL (issuedAt/expiresAt for offline tolerance), subject (DID/URI for identity binding), and JSON-LD context for semantic richness. Frame UM as a specification and document format. Do NOT mention TypeScript, npm, or any specific programming language. Do NOT discuss internal data structures yet -- that is the next section.

---

## Section 3: Data Structures -- Facets and Pointers

Cover the two core data structures: facets (named modular compartments like publicProfile, deviceIdentity) and pointers (URIs referencing external authoritative data instead of embedding it). Emphasize the pattern: facets organize, pointers reference, manifests stay small (1-3 KB). Do NOT list every possible facet name -- focus on the extensible pattern. Do NOT discuss consent or signatures -- those are separate sections.

---

## Section 4: Consent Model

Cover the default-deny consent model: if a permission isn't explicitly granted, it's denied. Three states: allowed, denied, not-set (= denied). Consent travels inside the envelope so downstream systems know permissions without calling back. Frame as portable privacy compliance. Do NOT mention GDPR, cookie banners, or any specific regulation. Do NOT discuss implementation details of how consent is stored.

---

## Section 5: Integrity and Signatures

Cover v0.2 signatures: Ed25519 + JCS canonicalization for deterministic signing. Emphasize modular signature profiles (verify what you support, ignore what you don't) and forward compatibility (unknown fields preserved, not rejected). Frame as integrity assurance, like a notary stamp. Do NOT deep-dive into Ed25519 key generation, JCS algorithm internals, or cryptographic implementation specifics.

---

## Section 6: The Composite Stack

Cover the three-layer composite stack: Storage/Registry (bottom), Transit/State Envelope = UM (middle), Execution/Runtime (top). UM is the transit layer that bridges storage and runtime without replacing either. Frame as architecture-agnostic -- works with any storage backend and any runtime environment. Do NOT name specific storage or runtime products as required dependencies.

---

## Section 7: How UM Fits Into IWPS

THE KEY SECTION. Frame IWPS as transport plumbing (Query + Teleport APIs, capability negotiation, session binding) and UM as cargo (identity, consent, facets, pointers, TTL, signatures). IWPS's TBD assets parameter is where UM fits. Walk through the integration flow: Portal -> Query with UMID -> resolve manifest -> Teleport with payload. Show mutual value: UM adds consent/facets/pointers/TTL/signatures; IWPS adds negotiation/transport/sessions. Do NOT frame UM as replacing IWPS. Do NOT criticize IWPS's TBD sections -- frame them as collaboration opportunities.

---

## Section 8: Hackathon Demo

Cover the hackathon proof-of-concept that validated UM in a spatial environment. Portal server resolved manifests by UMID for a Three.js 3D space. Key demonstrations: dual-format normalization (UM v0.1 + Manifest Commons), avatar loading via pointer URLs, identity traversal across renderers, and runtime consent checking. Do NOT mention PeerMesh as a product -- frame as "a hackathon proof-of-concept." Do NOT position the hackathon code as production-ready or as the reference implementation.

---

## Section 9: Next Steps / Call to Action

Cover three next steps: (1) publish UM as an OMA3 standard complementing IWPS, (2) position UM as the payload format for IWPS's Asset Transfer Framework, (3) collaborate on aligning the two specs (UMID in Query/Teleport params, consent-to-capability mapping, pointer resolution). Frame as partnership, not competition. Do NOT make commitments or promises about timelines. Do NOT discuss internal roadmap items beyond the OMA3 collaboration scope.
