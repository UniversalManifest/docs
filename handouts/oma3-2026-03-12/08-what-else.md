# 08 -- Beyond Metaverse: The Full Application Space

---

## The Analogy

A shipping container was designed for ocean freight. But the standardized format turned out to be useful for trains, trucks, temporary offices, pop-up shops, emergency housing, and art installations. The container did not change -- people discovered new uses for the same standard shape.

Universal Manifest is a standard shape for portable state. The metaverse portaling use case is where it started. But the same architecture -- facets, pointers, consent, signatures, resolution -- applies wherever identity, credentials, or consent need to travel between systems.

---

## Why

Standards bodies sometimes ask: "Is this a metaverse thing?" The answer matters because a standard tied to one domain has a narrow adoption path. UM's architecture is domain-neutral by design. The manifest format, consent model, signature profile, and resolver contract carry no assumptions about metaverse, social media, IoT, or any specific vertical.

## What -- The Concept Hierarchy

The Universal Manifest specification has mapped **163 leaf-level use cases** across **15 top-level categories**. Each use case describes a concrete scenario where portable state solves a real problem.

### The 15 Categories

| # | Category | Use Cases | Example Scenarios |
|---|----------|-----------|-------------------|
| 1 | **Identity & Profile Portability** | 13 | Social profile across platforms, professional credentials, gaming identity |
| 2 | **Consent & Privacy Management** | 14 | Default-deny firewall, cross-platform consent sync, GDPR-portable consent |
| 3 | **Digital Assets & Ownership** | 10 | NFT provenance, cross-chain asset references, digital collectible portability |
| 4 | **Metaverse & Spatial Computing** | 14 | Cross-world portaling, avatar transport, spatial consent, venue policies |
| 5 | **IoT & Device Enrollment** | 10 | Device registration, smart home identity, fleet enrollment |
| 6 | **Commerce & Payments** | 10 | Payment handle portability, loyalty programs, purchase history |
| 7 | **Credentials & Verification** | 12 | Age verification, KYC proofs, professional licenses, academic records |
| 8 | **Creative & Media** | 10 | Artist attribution, content provenance, rights management |
| 9 | **Enterprise & Organization** | 9 | Employee credential portability, B2B trust, supply chain identity |
| 10 | **Governance & Standards** | 10 | Spec versioning, conformance profiles, cross-standard alignment |
| 11 | **Healthcare & Wellbeing** | 10 | Patient identity portability, consent for health data, emergency access |
| 12 | **Education & Research** | 8 | Academic transcript portability, research credential sharing |
| 13 | **Government & Civic** | 8 | Civic identity, voting credential portability, public service access |
| 14 | **Social & Community** | 10 | Reputation portability, social graph references, group membership |
| 15 | **Infrastructure & Protocol** | 15 | Resolver contract, signature profiles, caching, consent architecture |

### Status Breakdown

| Status | Count | What It Means |
|--------|-------|--------------|
| **Proven** | 15 | Fixture-backed, journey-tested, production-verified |
| **Documented** | 28 | Explainer, integration lane, or design document exists |
| **Proposed** | 61 | Concept identified and described; no implementation evidence yet |
| **Unexplored** | 59 | Domain identified as applicable; detailed analysis not yet done |
| **Total** | **163** | |

### Where the depth is

The deepest coverage is in the foundation:

- **Infrastructure & Protocol:** 6 proven, 7 documented (13 of 15 concepts with evidence). This is the core that everything builds on.
- **Consent & Privacy:** 4 proven, 2 documented. The consent model is battle-tested across multiple journey scenarios.
- **Metaverse & Spatial Computing:** 1 proven, 5 documented. The portaling integration with IWPS builds on this foundation.
- **Credentials & Verification:** 2 proven, 2 documented. Age verification and personhood proof journeys exist.

### Where the opportunity is

The 59 unexplored concepts are not gaps -- they are the market. Each represents a domain where UM's architecture applies but detailed work has not yet been done. The largest clusters:

- **Government & Civic:** 7 unexplored (civic identity, voting credentials, public service access)
- **IoT & Device Enrollment:** 7 unexplored (fleet management, smart home, industrial IoT)
- **Commerce & Payments:** 6 unexplored (payment handles, loyalty, purchase history)
- **Creative & Media:** 6 unexplored (attribution, provenance, rights management)

These domains do not require changes to UM's core architecture. They require defining domain-specific facet names, consent keys, and integration guidance -- the same extensibility pattern that already works for metaverse and social.

### How every domain uses the same architecture

Every category uses the same five building blocks:

1. **Facets** carry domain-specific data (medical records, game profiles, employment history)
2. **Pointers** reference external authoritative sources (avatar CDN, credential issuer, data pod)
3. **Consent** controls what receiving systems can do with the data
4. **Signatures** prove the manifest was not tampered with
5. **The resolver** makes the manifest findable by UMID

The architecture does not change across domains. Only the facet names, consent keys, and pointer types change.

---

*Next: [09 -- What's Next](09-whats-next.md) covers current status, roadmap, and collaboration opportunities.*
