# IWPS–Universal Manifest Alignment Analysis and Integration Strategy

**Date:** 2026-03-11
**Work order:** WO-0147
**Prepared for:** OMA3 presentation (2026-03-12)

---

## 1. Executive Summary

The **Inter-World Portaling Standard (IWPS)** v0.3 and the **Universal Manifest (UM)** specification occupy complementary layers in the metaverse interoperability stack. They are not competing standards; they are designed to work together.

**IWPS is the plumbing.** It defines *how* a user moves between virtual worlds: a two-call transport protocol (Query + Teleport) that handles capability negotiation, session binding, and communication path selection between a Source World and a Destination World.

**UM is the cargo.** It defines *what* travels with the user: a portable, cryptographically verifiable JSON-LD envelope carrying identity, asset pointers, consent rules, compliance proofs, social graph references, preferences, and reputation — all organized into modular facets with default-deny privacy.

IWPS has explicit TBD sections for asset transfer, look-and-feel portability, payments, and portable state. UM fills precisely these gaps. Together, they provide a complete portaling solution: IWPS moves the user; UM carries the user's portable state.

This document maps the complementary relationship, identifies integration points, and recommends that OMA3 publish UM as the portable state standard that completes the IWPS portaling picture.

---

## 2. Layer Mapping

| Layer | IWPS v0.3 | Universal Manifest |
|-------|-----------|-------------------|
| **Transport** | Query + Teleport APIs (two HTTP calls with session binding) | Not addressed — UM is transport-agnostic by design |
| **Identity** | `userId` string; four authentication models (self-attested, source-verified, third-party, decentralized) | Rich identity via DID-based `subject` field; cryptographic signatures; facet-scoped identity projections |
| **Assets** | TBD — "Reserved for Future Use" in both Query and Teleport payloads | Asset pointers (`metaverse.avatar`, `metaverse.inventory`); projection rules; graceful degradation guidance |
| **Look-and-Feel** | TBD — acknowledged as needed but undefined | Avatar pointers, preference bundles (`prefs.language.*`, `prefs.financial.*`), facet-based profile projection |
| **Consent / Privacy** | Not addressed | Default-deny consent propagation per facet; granular consent keys (`metaverse.voiceCapture`, `metaverse.recording.faceVisible`, etc.) |
| **Portable State** | Not addressed | JSON-LD envelope with TTL-based freshness; pointer-first architecture; offline-tolerant caching |
| **Compliance** | Not addressed | Compliance proofs via claims and pointers (`metaverse.complianceProof`); age-gate and KYC without exposing raw PII |
| **Social** | Not addressed | Social graph pointers (`metaverse.socialGraph`); reputation references (`metaverse.reputation`); consent-gated disclosure |
| **Payments** | TBD | Payment handle integration (planned, tracked as WO-0142) |
| **Integrity / Trust** | OMA3 Security Certification tiers (Bronze/Silver/Gold) | JCS + Ed25519 cryptographic signatures (v0.2 profile); deterministic canonicalization; signature profile extensibility |
| **Capability Negotiation** | `portalLimitations` + `approvedAssets` in Query response | Graceful degradation rules — consumers project what they support, ignore what they do not |

---

## 3. Integration Points

### 3.1 IWPS `assets` parameter maps to UM manifest

The IWPS Query and Teleport API payloads both include an `assets` field marked "Reserved for Future Use." This is exactly where a Universal Manifest Identifier (UMID) or an inline UM manifest belongs. The UM specification defines the structure, semantics, and validation rules for the portable state that `assets` is intended to carry.

**Proposed mapping:** `assets` carries a UMID (a resolvable reference to a manifest hosted at `myum.net/{UMID}`) or, for low-latency scenarios, an inline UM manifest envelope.

### 3.2 IWPS `portalLimitations` + `approvedAssets` maps to UM graceful degradation and projection rules

When a Destination World responds to a Query call, it returns `portalLimitations` describing what it cannot support and `approvedAssets` listing what it can accept. UM's graceful degradation model aligns directly: UM consumers are already required to project only what they support and ignore unknown fields safely. The Destination World can use the UM manifest's asset pointers and facets to determine which items to approve and which limitations to declare.

### 3.3 IWPS User Agent communication path maps to UM privacy-preserving carrier

IWPS defines multiple communication paths: Device-to-Device, Cloud-to-Cloud, Hybrid, and User Agent. The User Agent path, where the user's client mediates the transfer, is the most natural carrier for a UM manifest. This aligns with UM's subject-controlled runtime model, where the subject's wallet or client holds the authoritative manifest and selectively discloses facets based on consent rules.

### 3.4 IWPS Identity Framework Model 3 (Source-verified) maps to UM cryptographic signatures

IWPS Identity Framework Model 3 describes source-verified identity, where the Source World vouches for the user's identity to the Destination World. UM's v0.2 signature profile (JCS + Ed25519) provides the cryptographic mechanism for this: the issuer signs the manifest, and the Destination World can verify the signature without trusting a central authority.

### 3.5 IWPS `userId` maps to UM `subject` DID

IWPS carries a `userId` string with the portal request. UM uses a DID-based `subject` field as the canonical identity anchor. The `userId` in an IWPS request can reference the same DID that appears in the UM manifest's `subject` field, binding the transport-level identity to the rich portable state.

---

## 4. What UM Adds to IWPS

UM fills the gaps that IWPS explicitly marks as TBD or does not address:

1. **Structured portable state that fills the `assets` TBD.** UM provides a defined JSON-LD envelope with a published schema, validation rules, and conformance tests. IWPS no longer needs to define its own asset format from scratch — it can reference UM as the payload standard.

2. **Consent propagation so destination worlds know what they are allowed to do.** UM's default-deny consent model means every facet of the user's portable state carries explicit permission boundaries. The Destination World does not have to guess what it can disclose, render, or record.

3. **Facet-based modularity so different contexts read different data.** A gaming world reads gaming-relevant facets; a social platform reads social facets; a commerce platform reads payment-relevant facets. The same manifest serves all contexts without exposing irrelevant data.

4. **Pointer-first architecture so manifests stay lightweight.** Instead of copying megabytes of avatar geometry or inventory data into the transport payload, UM carries URI pointers to authoritative sources. This keeps the manifest at 1–3 KB, well within the payload limits of any transport protocol.

5. **TTL and freshness so state does not go stale.** Every UM manifest carries `issuedAt` and `expiresAt` timestamps. The Destination World knows exactly when to stop trusting cached state and request a fresh manifest, without needing a separate revocation check protocol.

6. **Cryptographic integrity so state cannot be tampered with in transit.** The v0.2 signature profile ensures that the manifest the Destination World receives is exactly what the issuer produced. Combined with IWPS's transport-level session binding (`teleportId` + `teleportPin`), this provides defense in depth.

---

## 5. What IWPS Adds to UM

UM is deliberately transport-agnostic. IWPS provides the concrete transport layer that UM does not define:

1. **Concrete transport protocol for the portaling use case.** IWPS's two-call pattern (Query to negotiate, Teleport to execute) gives UM a well-defined delivery mechanism for the metaverse portaling lane. UM does not need to invent its own portal API.

2. **Platform capability negotiation.** IWPS's Query response includes ISA (Instruction Set Architecture), OS, and client type information. This lets the Source World (or the user's client) tailor the UM manifest's asset pointers to formats the Destination World can actually render.

3. **Communication path selection.** IWPS defines four communication models (Device, Cloud, Hybrid, User Agent). This gives UM carriers deployment flexibility: a privacy-sensitive deployment can use the User Agent path; a low-latency deployment can use Cloud-to-Cloud.

4. **Session binding via TeleportId + TeleportPin.** IWPS's session binding mechanism ensures that the UM manifest delivered during Teleport corresponds to the negotiation that happened during Query. This prevents replay and misdirection attacks at the transport level.

5. **OMA3 Security Certification tiers.** IWPS defines Bronze, Silver, and Gold certification levels for world operators. This provides an external trust signal that UM consumers can factor into their trust posture evaluation alongside UM's own signature verification.

---

## 6. Proposed Integration Architecture

The following sequence shows how a portal flow works when IWPS and UM operate together.

### Step-by-step portal flow

```
┌──────────────┐                                    ┌──────────────┐
│ Source World  │                                    │  Dest World  │
│  (Platform A) │                                    │  (Platform B) │
└──────┬───────┘                                    └──────┬───────┘
       │                                                   │
       │  1. User encounters portal to Platform B          │
       │                                                   │
       │  2. Source calls IWPS Query API:                   │
       │     - portalURI = "platformb://lobby"              │
       │     - userId = "did:key:z6Mk..."                  │
       │     - assets = { umid: "urn:uuid:abc-123" }       │
       │  ─────────────────────────────────────────────►   │
       │                                                   │
       │                  3. Destination receives UMID,     │
       │                     fetches manifest from          │
       │                     myum.net/urn:uuid:abc-123      │
       │                                                   │
       │                  4. Destination inspects manifest: │
       │                     - Verifies signature (v0.2)    │
       │                     - Checks TTL / freshness       │
       │                     - Reads consent rules          │
       │                     - Resolves supported facets    │
       │                     - Resolves asset pointers      │
       │                                                   │
       │  5. Destination returns Query response:            │
       │     - approved = true                              │
       │     - approvedAssets = [avatar, profile]           │
       │     - portalLimitations = [inventory:partial]      │
       │     - teleportId = "tport-xyz-789"                │
       │  ◄─────────────────────────────────────────────   │
       │                                                   │
       │  6. Source calls IWPS Teleport API:                │
       │     - teleportId = "tport-xyz-789"                │
       │     - teleportPin = "pin-456"                     │
       │     - assets = { umid: "urn:uuid:abc-123" }       │
       │  ─────────────────────────────────────────────►   │
       │                                                   │
       │                  7. Destination loads user with:   │
       │                     - Identity from manifest       │
       │                       subject DID                  │
       │                     - Avatar from metaverse.avatar │
       │                       pointer                      │
       │                     - Profile from publicProfile   │
       │                       facet                        │
       │                     - Preferences from prefs.*     │
       │                       keys                         │
       │                     - Consent rules enforced       │
       │                       (default-deny)               │
       │                                                   │
       │  8. Destination calls sourceAckUrl:                │
       │     - status = "arrived"                           │
       │     - teleportId = "tport-xyz-789"                │
       │  ─────────────────────────────────────────────►   │
       │                                                   │
       │  (Source confirms departure and cleans up          │
       │   local session state)                             │
       │                                                   │
```

### Key architectural properties of this flow

- **Separation of concerns:** IWPS handles transport negotiation and session management. UM handles portable state definition and consent enforcement. Neither standard needs to know the internal implementation details of the other.
- **Resolver-mediated state retrieval:** The Destination World fetches the manifest from the UM resolver (`myum.net`) rather than receiving a potentially large payload inline. This keeps the IWPS API calls lightweight.
- **Consent enforcement at arrival:** The Destination World applies UM consent rules before activating any features. Portaling does not grant implicit permission.
- **Graceful degradation:** If the Destination World cannot render certain assets, it declares `portalLimitations` in the Query response. The Source World can inform the user. The UM manifest's pointer-first design means partial support is handled cleanly.

---

## 7. Gap Analysis

### 7.1 IWPS gaps that UM fills

| IWPS Gap | UM Capability |
|----------|--------------|
| Asset transfer format (TBD) | UM manifest envelope with typed asset pointers and facets |
| Look-and-feel portability (TBD) | Avatar pointers, preference bundles, facet-based profile projection |
| Privacy and consent | Default-deny consent propagation; granular consent keys per facet |
| Compliance and age verification | Compliance proofs via claims and pointers; decision-grade status without PII exposure |
| Social graph portability | Social graph and reputation pointers with consent-gated disclosure |
| Portable state freshness | TTL-based validity with `issuedAt` / `expiresAt` timestamps |
| Cryptographic state integrity | JCS + Ed25519 signature profile (v0.2); extensible to additional profiles |

### 7.2 UM gaps that IWPS fills

| UM Gap | IWPS Capability |
|--------|----------------|
| Transport protocol for portaling | Query + Teleport two-call API with session binding |
| Platform capability negotiation | ISA, OS, client type metadata in Query handshake |
| Communication path selection | Device, Cloud, Hybrid, User Agent models |
| Session binding and anti-replay | TeleportId + TeleportPin mechanism |
| Operator trust certification | OMA3 Security Certification tiers (Bronze/Silver/Gold) |

### 7.3 Remaining gaps in both standards

| Gap | Status |
|-----|--------|
| **Payments framework** | TBD in IWPS; planned in UM (WO-0142, payment handle integration). Neither standard currently defines a complete payment portability model. This is a natural area for joint development. |
| **Real-time asset streaming** | Neither standard addresses continuous synchronization of live world state. Both are designed for discrete transfer events, not real-time replication. |
| **Multi-party portaling** | IWPS defines single-user portal flows. UM manifests are per-subject. Group portaling (moving a party of users together) is not currently addressed by either standard. |
| **Cross-chain asset ownership verification** | Both standards can reference blockchain-based assets, but neither defines a normative on-chain verification protocol. This may be addressed through OMATrust's attestation layer. |

---

## 8. Recommendations for OMA3

### 8.1 Publish UM as the portable state standard that complements IWPS

IWPS and UM together provide a complete portaling solution. OMA3 should position UM as the specification that defines what the `assets` parameter carries — the structured, consent-aware, cryptographically verifiable portable state envelope that IWPS transports.

### 8.2 Position UM as the payload for IWPS's `assets` parameter

The IWPS specification's `assets` field (currently "Reserved for Future Use") should reference the Universal Manifest specification as the recommended payload format. This does not require changes to the IWPS API structure — it fills an existing extension point.

### 8.3 Collaborate on the Asset Transfer Framework with UM as the reference model

Rather than designing a new asset transfer format from scratch, OMA3 can use UM's pointer-first, facet-based, consent-aware architecture as the reference model for the Asset Transfer Framework that IWPS anticipates. This accelerates delivery and ensures consistency with a specification that already has:

- Published JSON-LD schemas at stable URLs
- A deterministic resolver contract (`myum.net/{UMID}`)
- Conformance test fixtures (valid and invalid)
- Multiple integration lanes (metaverse, social, IoT/edge, smart glasses, spatial computing)
- A v0.2 signature profile for cryptographic integrity
- MUM lineage directly from the Metaverse Standards Forum working group concept

### 8.4 Align identity models

IWPS Identity Framework Model 4 (Decentralized) aligns most naturally with UM's DID-based `subject` field. OMA3 should consider recommending DID-based identity as the preferred model when IWPS and UM operate together, while preserving backward compatibility with IWPS Models 1–3 for deployments that do not yet support DIDs.

### 8.5 Define a joint conformance profile

A joint "IWPS + UM" conformance profile would give world operators a clear integration target: implement the IWPS transport protocol, accept UM manifests as the `assets` payload, enforce UM consent rules at arrival, and support graceful degradation for unsupported asset types. This profile could be tiered alongside OMA3's existing Security Certification levels.

---

## References

- [IWPS v0.3 specification](https://github.com/nicktjhia/Inter-World-Portaling-System) — OMA3 Inter-World Portaling Standard
- [Universal Manifest specification](https://universalmanifest.net) — UM standards and documentation site
- [UM resolver](https://myum.net) — Deterministic manifest resolution service
- [`integrations/metaverse.md`](../../integrations/metaverse.md) — UM metaverse integration lane
- [`docs/explainers/metaverse-portaling.md`](../explainers/metaverse-portaling.md) — MUM portaling explainer
- [`docs/STANDARDS-POSITIONING.md`](../STANDARDS-POSITIONING.md) — UM standards positioning (all bodies)
- [`docs/MSF-RELATIONSHIP.md`](../MSF-RELATIONSHIP.md) — MSF relationship document
- [`docs/reports/2026-03-06-metaverse-portaling-integration-note.md`](2026-03-06-metaverse-portaling-integration-note.md) — Portaling integration note
- [`docs/journeys/journey-09-metaverse-crossworld-projection.md`](../journeys/journey-09-metaverse-crossworld-projection.md) — Metaverse portaling journey
