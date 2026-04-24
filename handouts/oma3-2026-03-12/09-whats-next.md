# 09 -- Current Status and Roadmap

---

## What Exists Today

### Specification

- **v0.1** is the adoption-focused core contract. Published JSON-LD context and JSON Schema at stable URLs. Conformance fixtures (valid and invalid) are published.
- **v0.2** is a draft that adds a production-grade signature profile (Ed25519 + JCS). Schema, context, and conformance fixtures are available for implementer validation.
- Both versions share the same structural topology: header, facets, claims, consents, devices, pointers, signature.

### Resolver

- **myum.net** is the reference deployment of the resolver specification. It resolves UMIDs to manifests via HTTP GET. The contract is documented with a machine-readable well-known descriptor.
- The resolver returns 307 redirects to canonical sources, 200 payloads for inline manifests, 404 for unknown UMIDs, and 410 for revoked ones.
- Any organization can run a conformant resolver using the published contract specification.

### Proof and Evidence

- **25 journey proofs** demonstrate end-to-end scenarios: public profile projection, smart glasses consent, metaverse cross-world portaling, device enrollment, tampered manifest detection, and more.
- **An interactive sandbox** on universalmanifest.net lets users step through scenarios and inspect manifest state at each stage.
- **A hackathon proof-of-concept** validated UM concepts in a live spatial environment with portal-based manifest resolution, avatar loading from pointers, and runtime consent enforcement.
- **16 integration lanes** document how UM applies to specific domains: metaverse, social, IoT, smart glasses, spatial computing, credentials, and others.

### Concept Coverage

- **163 leaf-level use cases** across 15 categories have been identified and cataloged.
- 15 are proven with fixture evidence. 28 are documented. 61 are proposed. 59 are unexplored.

---

## What Is Being Worked On

### Active Items

| Item | Status | What It Does |
|------|--------|-------------|
| IWPS alignment and OMA3 positioning | Active | Maps UM as the cargo layer for IWPS transport. Proposes UM as the payload for the `assets` parameter. |
| Facet encryption architectural decision | Accepted | Uses an additive privacy model: projection remains the normative path, while encrypted inline facets are optional guidance for confidentiality at rest. |
| Payment handle integration | Not started | Creating standard pointers for fiat and crypto payment gateways. A natural collaboration area with OMA3. |

### Deferred Items (tracked, not forgotten)

The project maintains a comprehensive audit of 62+ deferred items across 10 categories. These include:

**Specification gaps** -- encrypted facets, batch revocation protocol, content integrity for pointer targets, audience-scoped consent.

**Research tracks** -- selective disclosure (BBS+, SD-JWT), wallet protocol bindings, avatar translation profiles, synchronization conflict resolution.

**Standards alignment** -- IWPS `assets` parameter formal binding, joint IWPS+UM conformance profile, proximity credential presentation profile, OpenID Federation trust mapping.

**Proposed extensions** -- CBOR-LD binary encoding for constrained transports, Merkle history for audit trails, content-addressed identifiers for immutable snapshots.

Each item is tracked with a priority (P0 through P3), a blocking assessment, and a link to where it is documented.

---

## Where OMA3 Collaboration Fits

### The primary integration point

IWPS v0.3's `assets` parameter is marked "Reserved for Future Use." UM fills this gap. The proposal: `assets` carries a UMID (a resolvable reference to a manifest) or, for low-latency scenarios, an inline manifest. No changes to the IWPS API structure are required -- this fills an existing extension point.

### Joint areas of interest

| Area | Current Status | Collaboration Opportunity |
|------|---------------|--------------------------|
| **IWPS `assets` binding** | Alignment analysis complete; proposal drafted | Define the formal binding specification together |
| **Payments** | TBD in both IWPS and UM | Co-develop the payment portability model |
| **Joint conformance profile** | Proposed | Define "IWPS + UM" conformance tiers alongside OMA3 Security Certification |
| **Avatar translation** | Research track | Co-develop cross-engine avatar portability metadata |
| **Compliance proofs** | UM has consent; IWPS has security tiers | Map consent rules to certification requirements |

### What we would like from OMA3

We would like to understand which areas of the concept space are most relevant to your work, so we can prioritize detailed documentation and integration guidance for those domains.

---

## Reference Materials

| Material | Location |
|----------|----------|
| Specification (v0.2) | `spec/v0.2/README.md` |
| Live documentation site | https://universalmanifest.net |
| Resolver | https://myum.net |
| IWPS alignment analysis | `docs/reports/2026-03-11-iwps-um-alignment-analysis.md` |
| Deferred items audit | `docs/reports/2026-03-12-deferred-concepts-and-loose-ends-comprehensive-audit.md` |
| Concept explorer (interactive) | https://universalmanifest.net/tools/concept-explorer/ |
| OMA3 presentation script | `docs/presentations/2026-03-12-oma3-architectural-overview.md` |

---

*This concludes the OMA3 handout collection. Return to the [Reading Guide](00-reading-guide.md) for the full table of contents.*
