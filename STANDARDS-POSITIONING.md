# Standards Positioning — Universal Manifest

This document is the single authoritative reference for Universal Manifest's relationship to formal standards, adjacent specifications, and standards bodies. It covers what UM builds on, how UM relates to neighboring efforts, which standards organizations are relevant, and what the project's current standardization intent is.

---

## 1. Standards UM Builds On

Universal Manifest is built on established, widely implemented standards. Every foundational dependency was chosen for broad adoption, proven interoperability, and availability across programming languages and platforms.

### JSON-LD (W3C Recommendation)

UM documents are valid JSON-LD. The `@context`, `@id`, and `@type` fields follow JSON-LD conventions, and a published JSON-LD context file at `universalmanifest.net` defines the UM vocabulary. JSON-LD awareness is optional for consumers -- every manifest is also valid plain JSON, and systems that do not process linked data can still parse and use the document.

- **W3C specification:** JSON-LD 1.1 (W3C Recommendation, 2020-07-16)
- **UM usage:** Document structure, vocabulary definition, semantic interoperability

### Decentralized Identifiers / DIDs (W3C Recommendation)

DIDs are the recommended format for the `subject` field in a manifest. UM supports `did:key`, `did:web`, and `did:plc` as initial DID method coverage (per decision record 2026-02-20), with `did:chia` supported as an extension lane. However, UM does not require DIDs -- any stable URI works as a subject identifier.

- **W3C specification:** Decentralized Identifiers (DIDs) v1.0 (W3C Recommendation, 2022-07-19)
- **UM usage:** Subject identifier format (recommended, not required)

### Verifiable Credentials Data Model (W3C Recommendation)

UM can carry W3C Verifiable Credentials as claims within shards. The UM manifest is the container; VCs are one type of payload it can hold. UM does not implement the VC issuance or verification protocol itself -- it provides a portable envelope that can transport VC-based claims alongside other data types.

- **W3C specification:** Verifiable Credentials Data Model v2.0 (W3C Recommendation, 2024-10-24)
- **UM usage:** Claims within shards can be structured as VCs

### JSON Canonicalization Scheme / JCS (IETF RFC 8785)

The v0.2 signature profile uses JCS to produce a deterministic byte representation of the manifest before signing. JCS was chosen because it operates at the JSON level (not the RDF graph level), making it implementable in any language with a JSON parser -- no JSON-LD processing library required.

- **IETF specification:** RFC 8785 — JSON Canonicalization Scheme (JCS), published 2020-06
- **UM usage:** Canonicalization step in the v0.2 signing and verification algorithm

### Ed25519 (IETF RFC 8032)

The v0.2 signature profile uses Ed25519 for public-key signatures. Ed25519 is fast, produces compact signatures (64 bytes), and is widely implemented across every major language and platform, including constrained environments like edge devices and Android TV.

- **IETF specification:** RFC 8032 — Edwards-Curve Digital Signature Algorithm (EdDSA), published 2017-01
- **UM usage:** Signature algorithm in the v0.2 signature profile

### Well-Known URIs (IETF RFC 8615)

The reference runtime integration lane uses `.well-known` URIs for service discovery (e.g., `/.well-known/um/edge.json`). This follows the IANA well-known URI registry conventions.

- **IETF specification:** RFC 8615 — Well-Known Uniform Resource Identifiers (URIs), published 2019-05
- **UM usage:** Service discovery in the reference runtime integration lane

### JSON Schema (IETF draft / OpenJS Foundation)

UM publishes JSON Schema files for both v0.1 and v0.2 that can be used with any JSON Schema validator for structural validation.

- **Specification:** JSON Schema Draft 2020-12
- **UM usage:** Structural validation of manifest documents

---

## 2. How UM Relates to Adjacent Standards and Efforts

UM occupies a specific position in the identity, credential, and data portability landscape. It is a **portable state document format** -- not a credential format, not a messaging protocol, not a storage system, and not an authentication mechanism. The following comparisons clarify where UM sits relative to commonly referenced adjacent efforts.

### W3C Verifiable Credentials (VCs)

**Relationship:** Complementary. UM is a container; VCs are a payload type.

VCs are individual claims issued by an authority and verifiable by a third party. A UM manifest can carry VCs as claims within shards. The analogy: VCs are stamps in a passport; UM is the passport itself. A system that already issues VCs can embed them in a manifest to make them portable alongside consents, device registrations, and pointers to canonical data.

UM does not replace the VC issuance/verification protocol. It provides a transport envelope and composition mechanism that allows VCs to coexist with other data types in a single document.

### DIDComm

**Relationship:** Complementary. UM is a document format; DIDComm is a messaging protocol.

DIDComm defines how DID-based systems exchange messages securely. A DIDComm message could carry a UM manifest as its payload. UM defines what the document looks like; DIDComm defines how it gets from A to B when DID-based messaging is the transport. They operate at different layers.

### Solid Pods (W3C)

**Relationship:** Complementary. UM is a portable summary layer; Solid is canonical storage.

Solid provides decentralized data storage with fine-grained access control. UM manifests use `pointers` to reference data stored in Solid Pods (e.g., `solidPod.creatorCanonical`). Rather than duplicating data from a Solid Pod into the manifest, the manifest carries a lightweight reference. Solid provides the authoritative, persistent store; UM provides the portable, time-bounded projection that can be handed to any consumer.

### OpenID Connect (OIDC)

**Relationship:** Different architectural purpose. OIDC is authentication; UM is state portability.

OIDC tokens carry authentication state -- proof that a user has logged in through an identity provider. UM manifests carry a broader set of portable state: identity references, verified claims, privacy consents, device registrations, and pointers to canonical data sources. A UM manifest might include a claim derived from an OIDC flow, but it serves a fundamentally different purpose. OIDC answers "has this user authenticated?" UM answers "what is true about this entity right now, in a way any system can use?"

### ActivityPub / AT Protocol (Bluesky)

**Relationship:** Complementary. UM can reference federated identities via pointers.

ActivityPub and the AT Protocol are federation protocols for social networking. UM manifests can carry pointers to ActivityPub actors (`activityPub.actor`) and AT Protocol identities. The social integration lane demonstrates how a single manifest can drive a profile projection across multiple federated social surfaces. UM does not replace federation protocols; it provides a portable identity layer that links to them.

### W3C Data Integrity

**Relationship:** Future additive profile option.

W3C Data Integrity provides a framework for signing linked data at the RDF graph level. The UM v0.2 signature profile uses JCS + Ed25519 (JSON-level canonicalization) as the pragmatic first profile. A Data Integrity profile (RDF canonicalization + linked data proofs) is a planned future additive profile, not an either-or choice. The signature profile architecture is designed for multiple coexisting profiles -- consumers verify the profiles they support and safely skip unknown ones.

---

## 3. Relationship to Standards Bodies and Organizations

### Metaverse Standards Forum (MSF)

**Relationship type:** Historical lineage.

Universal Manifest is explicitly descended from the **Metaverse Universal Manifest (MUM)** concept document, which was created within an MSF working group repository. The original MUM v1.0 concept document is the intellectual lineage source for the entire project.

**Current status:** UM has evolved beyond the original MUM scope. While MUM focused on metaverse cross-world identity portability, UM has been broadened into a cross-domain standard that treats metaverse as one of many integration lanes (alongside social, IoT/edge, smart glasses, spatial computing, proof of personhood, and others). The metaverse integration lane remains a first-class integration target with dedicated fixtures, journeys, and site documentation.

**Current organizational relationship:** There is no active formal relationship between the UM project and the MSF as an organization. The lineage is historical. The MSF is acknowledged as the origin context for the concept that became Universal Manifest.

**Future plans:** The project is open to contributing UM back to MSF working groups if there is mutual interest and alignment. This is not currently planned or in progress. The MSF's metaverse interoperability working groups remain a natural venue for collaboration if UM's metaverse integration lane matures to the point where formal standards submission is appropriate.

For a detailed treatment of the MSF relationship, see [`docs/MSF-RELATIONSHIP.md`](MSF-RELATIONSHIP.md).

### OMA3 / OMATrust

**Relationship type:** Active integration lane with assessed compatibility.

OMA3 is a consortium focused on Web3 interoperability and open metaverse standards. OMATrust is an OMA3 product that provides a decentralized trust layer with attestations, identity, and reputation for internet services. (Terminology convention: use `OMA3` for consortium/standards-body context, `OMATrust` for product/lane semantics.)

**Current status:** OMATrust is the most extensively developed standards-adjacent integration in the UM project. The integration was formally assessed in February 2026 ([`docs/reports/2026-02-22-omatrust-integration-assessment.md`](reports/2026-02-22-omatrust-integration-assessment.md)), with the finding of high conceptual compatibility and a "GO, but as a staged integration lane first" recommendation. The integration includes:

- A complete integration lane document ([`integrations/oma-trust.md`](../integrations/oma-trust.md))
- Published site documentation at `/integrations/oma-trust/`
- Three dedicated fixture manifests (proof-based service, trusted-attester service, lifecycle-edge service)
- A user journey (J11) proving interoperability patterns
- Suggested claim keys, pointer keys, and shard names for OMATrust signals

**Maturity note:** The assessment acknowledges that OMATrust portals are in preview/pre-alpha/testnet state. The domain structure (`docs.omatrust.org` vs `docs.oma3.org`) is in transition. Integration is staged to accommodate OMATrust's own maturation timeline.

**Future plans:** Deepen the integration as OMATrust matures toward production. The UM project does not currently plan to submit UM as a formal OMA3 standard, but the integration lane architecture is designed to allow progressive alignment. If OMA3 working groups develop standards for portable trust attestation envelopes, UM would be a natural carrier format.

### W3C (World Wide Web Consortium)

**Relationship type:** Standards consumer (building on W3C specifications).

UM builds directly on three W3C Recommendations: JSON-LD 1.1, Decentralized Identifiers v1.0, and Verifiable Credentials Data Model v2.0. These are foundational dependencies, not experimental choices. UM's technical architecture assumes these W3C standards are stable and broadly implemented.

**Current organizational relationship:** There is no formal relationship between the UM project and any W3C working group. UM consumes W3C standards as published specifications; it does not participate in W3C standardization processes.

**Future plans:** Engaging with W3C working groups is a possibility if UM reaches maturity levels where formal standardization is appropriate. The most relevant W3C groups would be:

- **W3C Credentials Community Group** — given UM's relationship to VCs and DIDs
- **W3C Verifiable Credentials Working Group** — if UM's shard/claim composition model intersects with VC envelope discussions
- **W3C Decentralized Identifier Working Group** — for DID method interoperability

No timeline or concrete plans exist for W3C engagement. This is a decision that will be revisited after the project achieves broader external adoption and multiple independent implementations.

### IETF (Internet Engineering Task Force)

**Relationship type:** Standards consumer (building on IETF RFCs).

UM uses three IETF specifications: RFC 8785 (JCS) for canonicalization, RFC 8032 (Ed25519) for signatures, and RFC 8615 (`.well-known` URIs) for service discovery. These are mature, widely implemented RFCs.

**Current organizational relationship:** There is no formal relationship between the UM project and the IETF. UM references IETF RFCs as foundational building blocks.

**Future plans:** There are no plans to submit UM as an IETF Internet-Draft or RFC. The IETF's process is oriented toward transport protocols and data formats with very broad internet applicability. UM may be more appropriate for standards bodies focused on identity, credentials, or interoperability.

### Linux Foundation

**Relationship type:** Documentation quality benchmark and organizational model influence.

The Linux Foundation's hosted project documentation standards were studied and benchmarked during the design of UM's documentation site ([`research/linux-foundation-projects/2026-02/INDEX.md`](../research/linux-foundation-projects/2026-02/INDEX.md)). The domain architecture decision (separating `universalmanifest.net` for spec governance from `myum.net` for runtime resolution) explicitly references the Linux Foundation model: "Makes Linux Foundation style adoption paths cleaner (spec governance != app/runtime service)" ([`docs/DOMAIN-ARCHITECTURE.md`](DOMAIN-ARCHITECTURE.md)).

**Current organizational relationship:** There is no formal relationship between the UM project and the Linux Foundation.

**Future plans:** The Linux Foundation (including Linux Foundation Europe) hosts specifications for identity, interoperability, and decentralized systems (e.g., Decentralized Identity Foundation projects, OpenWallet Foundation). If UM pursues a foundation-hosted governance model, the Linux Foundation ecosystem would be a natural fit. This is not currently planned or in progress.

---

## 4. Standardization Intent

### Current position

Universal Manifest is an **independent open-source specification** developed in a public GitHub repository under the Apache-2.0 license. It is not currently submitted to, hosted by, or governed by any formal standards body.

The project's governance document ([`docs/governance/GOVERNANCE.md`](governance/GOVERNANCE.md)) describes UM as "a standards-track specification," which refers to the project's internal maturity model (done-done framework with maturity gates from "production-candidate" through "world-ready"), not to an external standards body's track.

### Decision status

The decision on whether, when, and how to pursue formal standardization has **not been made**. The gap analysis report ([`docs/reports/2026-02-23-remaining-work-to-final-vision.md`](reports/2026-02-23-remaining-work-to-final-vision.md)) lists "Formal standards body submission (if desired)" as a future-vision item. The parenthetical "(if desired)" reflects the deliberate choice to defer this decision until the project has more adoption evidence.

### Prerequisites for formal standardization

Before formal standardization would be appropriate, the project needs:

1. **Multiple independent implementations** — Gate G4 in the done-done framework requires 3+ independent implementations from 3+ organizations. This is a prerequisite for any credible standards body submission.
2. **Stable v0.2 signature profile** — The v0.2 signature profile (JCS + Ed25519) is currently in draft. A stable, interoperability-tested signature profile is required before the spec can be considered for formal standardization.
3. **Conformance test suite** — A standalone conformance test suite that can be used by any implementation to verify compliance (tracked as WO-0053).
4. **External adoption evidence** — Real-world deployment evidence beyond the project's own reference implementation.

### What this means for adopters

UM is designed so that adopters do not need to wait for formal standardization. The specification is public, the schemas are published at stable URLs, the conformance requirements are documented, and the license (Apache-2.0) permits unrestricted use. Progressive adoption (parse, validate, consume shards, issue, sign/verify) is available today.

Formal standardization, if pursued, would provide additional governance guarantees (multi-stakeholder stewardship, formal change processes, patent commitments) but is not a prerequisite for technical adoption.

---

## 5. Summary Table

| Standards Body / Org | Relationship Type | Current Status | Future Plans |
|---|---|---|---|
| MSF | Historical lineage | No active formal relationship; MUM origin acknowledged | Open to contributing back if mutual interest arises |
| OMA3 / OMATrust | Active integration lane | Assessed, documented, fixtures and journey complete | Deepen as OMATrust matures |
| W3C | Standards consumer | Building on JSON-LD, DIDs, VCs; no organizational engagement | Possible future engagement after broader adoption |
| IETF | Standards consumer | Building on RFC 8785, RFC 8032, RFC 8615; no organizational engagement | No plans for RFC submission |
| Linux Foundation | Documentation/model influence | Benchmarked for docs quality; no organizational relationship | Natural fit if foundation-hosted governance is pursued |

---

## References

- [`docs/PROJECT-VISION.md`](PROJECT-VISION.md) — Project vision including MUM lineage
- [`docs/DECISIONS.md`](DECISIONS.md) — Decision records including v0.2 signature profile, DID method selection
- [`docs/governance/GOVERNANCE.md`](governance/GOVERNANCE.md) — Project governance structure
- [`docs/DOMAIN-ARCHITECTURE.md`](DOMAIN-ARCHITECTURE.md) — Domain split rationale
- [`docs/reports/2026-02-22-omatrust-integration-assessment.md`](reports/2026-02-22-omatrust-integration-assessment.md) — OMATrust integration assessment
- [`integrations/oma-trust.md`](../integrations/oma-trust.md) — OMATrust integration lane
- [`integrations/metaverse.md`](../integrations/metaverse.md) — Metaverse integration lane with MSF lineage
- [`docs/MSF-RELATIONSHIP.md`](MSF-RELATIONSHIP.md) — MSF relationship document
- [`docs/explainers/full-briefing.md`](explainers/full-briefing.md) — Full briefing with competitive positioning
- [`spec/v0.2/SIGNATURE-PROFILE.md`](../spec/v0.2/SIGNATURE-PROFILE.md) — v0.2 signature profile design
- [`research/linux-foundation-projects/2026-02/INDEX.md`](../research/linux-foundation-projects/2026-02/INDEX.md) — Linux Foundation documentation benchmark
