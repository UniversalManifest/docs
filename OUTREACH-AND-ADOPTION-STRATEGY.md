# Outreach and Adoption Strategy — Universal Manifest

This document defines the strategy for reaching external adopters of Universal Manifest. It covers target audiences, outreach channels, launch readiness, timeline, pitch materials, success metrics, and a conference plan.

This strategy covers **how to reach adopters**. For the onboarding package adopters receive once engaged, see WO-0055 (Adopter Onboarding Document Package). For the feedback loop that sustains adopter relationships, see WO-0056 (Adopter Feedback Loop).

---

## 1. Target Adopter Profiles

### Profile 1: Platform Developer (Identity / Social / Gaming)

**Who:** Developers building platforms where users move between contexts -- social networks, gaming platforms, creator tools, community platforms.

**Pain point:** Every new integration partner requires a custom user data exchange format. Profile sync, credential verification, and consent propagation are each a separate custom build.

**What UM gives them:** A single document format that carries identity, credentials, preferences, and consent between their platform and any UM-aware system. Progressive adoption: start by consuming manifests from other platforms, later issue their own.

**Entry point:** Parse a manifest (Level 1), consume known shards like `publicProfile` (Level 3), then issue manifests for their users (Level 4).

### Profile 2: IoT / Edge / Venue Operator

**Who:** Teams building for constrained devices, public displays, venue management, smart building systems, and offline-first environments.

**Pain point:** Devices at the edge need to know who is authorized and what policies apply, but they cannot phone home for every check. Connectivity is intermittent or absent.

**What UM gives them:** A self-contained, time-bounded permission document that works offline. TTL enforcement means the device knows when to stop trusting a cached manifest without a revocation check. Local-first by design.

**Entry point:** The reference runtime integration lane ([`integrations/reference-runtime.md`](../integrations/reference-runtime.md)) demonstrates the full edge-display-admin flow. Start by consuming manifests on devices, then issue device-scoped manifests from the edge server.

### Profile 3: Standards Body / Specification Author

**Who:** People working in W3C, IETF, MSF, OMA3, Decentralized Identity Foundation, OpenWallet Foundation, or similar organizations.

**Pain point:** Existing standards for identity, credentials, and data exchange are siloed. VCs carry claims but not consent. OIDC carries auth state but not portable preferences. DIDComm handles messaging but not document composition.

**What UM gives them:** A composition layer that carries VCs, consent, device registrations, and data pointers in a single envelope, built on their existing standards (JSON-LD, DIDs, JCS, Ed25519). UM complements, does not replace, existing standards.

**Entry point:** The standards positioning document ([`docs/STANDARDS-POSITIONING.md`](STANDARDS-POSITIONING.md)) and the "For Standards Bodies" positioning statement in the agent briefing ([`docs/explainers/agent-briefing.md`](explainers/agent-briefing.md)).

### Profile 4: Enterprise / Compliance Team

**Who:** Organizations with cross-system data exchange requirements, privacy compliance obligations (GDPR, CCPA), and multi-vendor integration challenges.

**Pain point:** User consent decisions do not travel with user data. Every system-to-system data exchange requires a separate consent verification mechanism. Integration costs multiply with each new partner.

**What UM gives them:** Default-deny consent that travels with the data. Every receiving system knows what it is allowed to do without calling back to the origin. The consent model is structural (built into the manifest), not bolted on.

**Entry point:** The full briefing's "For Business Decision-Makers" positioning statement ([`docs/explainers/full-briefing.md`](explainers/full-briefing.md)). The adoption path (five levels from parse to sign/verify) allows enterprise teams to start with low-risk integration.

### Profile 5: Decentralized Identity / Web3 Developer

**Who:** Developers building with DIDs, Verifiable Credentials, blockchain-based identity, or decentralized trust systems.

**Pain point:** DIDs and VCs provide identity and credential primitives, but there is no standard portable document that composes them with consent, device state, and data pointers into a single handoff-ready envelope.

**What UM gives them:** A manifest that uses their existing DID as the subject, carries their VCs as claims within shards, and adds consent, device registration, and pointer capabilities that DIDs and VCs alone do not provide. The OMATrust integration lane and the DID + VC lane demonstrate concrete examples.

**Entry point:** The DID + VC integration lane ([`integrations/did-vc.md`](../integrations/did-vc.md)), the OMATrust integration lane ([`integrations/oma-trust.md`](../integrations/oma-trust.md)), and the proof-of-personhood integration lane ([`integrations/proof-of-personhood.md`](../integrations/proof-of-personhood.md)).

### Profile 6: Spatial Computing / Smart Glasses Developer

**Who:** Developers building smart glasses applications, spatial computing platforms, and mixed-reality experiences.

**Pain point:** Consent for face recording, voice capture, and location sharing has no portable standard. Each smart-glasses platform implements its own ad-hoc consent mechanism. Users cannot express consent preferences that travel with them across devices and platforms.

**What UM gives them:** Consent keys for smart glasses-specific scenarios (`ar.recording.faceVisible`, `ar.recording.voiceAllowed`, `ar.profile.autoSharePublic`) that are machine-readable and enforceable in real time. The manifest travels with the user and declares their preferences to any UM-aware smart glasses runtime.

**Entry point:** The smart glasses integration lane ([`integrations/smart-glasses.md`](../integrations/smart-glasses.md)) and the RP1 spatial fabric lane ([`integrations/rp1-spatial-fabric.md`](../integrations/rp1-spatial-fabric.md)).

### Profile 7: Open-Source Contributor / Community Developer

**Who:** Individual developers interested in contributing to an open-source standard, building tools around it, or using it for personal projects.

**Pain point:** Want to contribute to a meaningful standards project but most standards processes are inaccessible to individual contributors.

**What UM gives them:** An Apache-2.0 licensed, public GitHub repo with clear governance, an RFC process for spec changes, and progressive contribution paths from filing issues to proposing RFCs.

**Entry point:** The CONTRIBUTING.md guide, the RFC template ([`docs/governance/RFC-TEMPLATE.md`](governance/RFC-TEMPLATE.md)), and the GitHub repository.

---

## 2. Target Ecosystem Map

### Tier 1 — Direct outreach targets (highest alignment)

| Organization / Community | Why | Integration Lane |
|---|---|---|
| OMA3 / OMATrust ecosystem | Active integration lane, assessed compatibility | OMATrust |
| Bluesky / AT Protocol community | AT Protocol DID integration (`did:plc`), social profile portability | Social |
| Mastodon / ActivityPub community | ActivityPub actor pointers, federated profile portability | Social |
| Solid Project community | Solid Pod pointer integration, data sovereignty alignment | Social / General |
| World ID (Tools for Humanity) | Proof-of-personhood integration lane | Personhood |
| Gitcoin Passport | Composite personhood score integration | Personhood |
| BrightID | Social-graph personhood verification | Personhood |
| Chia Network | `did:chia` DID method, on-chain VC integration | DID + VC |

### Tier 2 — Ecosystem alignment targets

| Organization / Community | Why | Integration Lane |
|---|---|---|
| Decentralized Identity Foundation (DIF) | DID interoperability, VC composition | General |
| OpenWallet Foundation | Wallet-based credential portability | General |
| W3C Credentials Community Group | VC + DID intersection | General |
| NVIDIA (edge/display) | Reference runtime uses NVIDIA Shield as exemplar | IoT / Edge |
| Smart glasses manufacturers (Meta, Snap, Xreal) | smart glasses consent model | Smart Glasses |
| Spatial computing platforms | RP1 spatial fabric integration | RP1 |
| Linux Foundation Europe projects | Governance model alignment, potential hosting | General |

### Tier 3 — Broader ecosystem

| Domain | Target Communities |
|---|---|
| Gaming | Game engine communities (Unity, Unreal, Godot), cross-game identity projects |
| Healthcare | FHIR / HL7 community (patient consent portability) |
| Education | Open Badges / CLR community (credential portability) |
| Creative economy | Creator tools, NFT platforms, rights management systems |
| Enterprise identity | SCIM / identity federation communities |

---

## 3. Outreach Channels

### Channel 1: GitHub (primary developer channel)

**Actions:**
- Maintain clear README, CONTRIBUTING.md, and issue templates for contributor onboarding
- Use GitHub Discussions for community Q&A and design discussion
- Publish releases with changelogs and migration guidance
- Cross-link from the repository to the documentation site and integration lanes

**Audience:** Developers, contributors, standards reviewers

### Channel 2: Standards Body Engagement (relationship-building)

**Actions:**
- Share the standards positioning document with contacts at OMA3, W3C CCG, DIF, and OpenWallet Foundation
- Present UM at relevant working group meetings (start with OMA3 given existing integration)
- Submit feedback or liaison statements to relevant W3C working groups when UM's architecture intersects their work
- Attend MSF meetings as an observer or contributor if metaverse lane traction justifies it

**Audience:** Standards body participants, specification authors

### Channel 3: Documentation Site (passive discovery)

**Actions:**
- Maintain [`universalmanifest.net`](https://universalmanifest.net) as the public face of the project
- Ensure the site has clear entry paths for each adopter profile (developer quick-start, business overview, standards positioning)
- Publish integration lane documentation with code examples and fixture references
- Maintain the interactive workbench for hands-on manifest exploration

**Audience:** All profiles (developers, business evaluators, standards reviewers)

### Channel 4: Direct Outreach (targeted partnerships)

**Actions:**
- Prepare a partnership proposal opening (available in [`docs/explainers/agent-briefing.md`](explainers/agent-briefing.md))
- Contact Tier 1 targets with a tailored pitch (use the integration lane that matches their domain)
- Offer to co-develop integration guidance for their specific use case
- Provide early access to conformance test suite and onboarding package

**Audience:** Tier 1 ecosystem targets

### Channel 5: Social Media and Developer Communities

**Actions:**
- Share project updates, integration lane demonstrations, and release announcements
- Post technical content to developer platforms (Dev.to, Hashnode, Medium)
- Engage in relevant Mastodon, Bluesky, and Twitter/X discussions about identity, portability, and consent standards
- Create short-form explainer content (thread-length summaries of what UM does and why)

**Audience:** Developer community, identity/privacy advocates

### Channel 6: Conferences and Events (in-person and virtual)

**Actions:** See Section 8 (Conference and Presentation Plan).

---

## 4. Launch Readiness Checklist

The following items must be ready before presenting UM publicly to external audiences. This is distinct from the deploy checklist (which covers technical deployment) and the done-done framework (which covers spec maturity).

### Must-have for public presentation

- [ ] **Standards positioning document published** — both in repo and on the site
- [ ] **Documentation site stable** — `universalmanifest.net` builds clean, all navigation works, no broken links
- [ ] **At least 3 integration lanes published on site** — with fixture references and suggested claim/pointer keys
- [ ] **One-pager and full briefing available** — [`docs/explainers/one-pager.md`](explainers/one-pager.md) and [`docs/explainers/full-briefing.md`](explainers/full-briefing.md)
- [ ] **Agent briefing with pitch templates available** — [`docs/explainers/agent-briefing.md`](explainers/agent-briefing.md)
- [ ] **Open-source infrastructure complete** — LICENSE, CONTRIBUTING.md, CODE_OF_CONDUCT.md, SECURITY.md
- [ ] **README cleaned of local paths** — No `/Users/<username>/...` references visible to external readers
- [ ] **Resolver operational** — `myum.net` returns healthy responses for known UMIDs
- [ ] **Workbench operational** — Interactive manifest exploration works on the live site
- [ ] **v0.1 JSON Schema `$id` corrected** — Points to `universalmanifest.net`, not legacy domain

### Should-have for credibility

- [ ] **v0.2 signature profile stable** — Draft status clearly communicated, with working verification examples
- [ ] **Conformance test suite available** — External adopters can run tests against their implementations (WO-0053)
- [ ] **Implementation guide published** — Sequential "how to implement" document (WO-0055)
- [ ] **At least one external implementation** — Evidence that someone outside the project has consumed or produced a manifest
- [ ] **CHANGELOG published** — Release history visible on the site

### Nice-to-have for polish

- [ ] **Animated explainer** — Visual walkthrough of the manifest lifecycle
- [ ] **Ecosystem map diagram** — Visual showing where UM fits relative to adjacent standards
- [ ] **Conference slide deck** — Ready-to-present materials

---

## 5. Timeline — From Current State to Public Launch

### Phase 1: Foundation (current — Q1 2026)

**Status:** In progress.

**Objective:** Complete the project infrastructure that makes external engagement credible.

**Key deliverables:**
- Standards positioning document (this strategy's companion, WO-0093)
- Open-source community infrastructure (LICENSE, CONTRIBUTING.md, CODE_OF_CONDUCT.md)
- v0.1 schema `$id` correction
- README cleanup
- Outreach strategy document (this document, WO-0095)

**External visibility:** Private sharing only. Share the project with individual trusted contacts for early feedback.

### Phase 2: Limited Beta (Q2 2026)

**Objective:** Get 3-5 external organizations to evaluate and attempt implementation.

**Key deliverables:**
- Conformance test suite (WO-0053)
- Implementation guide and adopter onboarding package (WO-0055)
- Adopter feedback loop (WO-0056)
- v0.2 signature profile promoted to stable (or clear timeline for stability)

**External visibility:** Targeted outreach to Tier 1 ecosystem targets. Share onboarding package, offer co-development support, and collect structured feedback.

**Success gate:** At least 2 organizations have attempted to parse or produce a manifest, and feedback has been collected and triaged.

### Phase 3: Public Announcement (Q3 2026)

**Objective:** Make the project publicly visible and invite broad participation.

**Key deliverables:**
- Public blog post / announcement
- Conference presentation(s)
- Standards body presentations (start with OMA3, then expand)
- All launch readiness checklist items complete

**External visibility:** Full public visibility. GitHub repo prominently positioned, documentation site polished, social media engagement active.

**Success gate:** At least 3 independent implementations from 3 organizations (Gate G4 from done-done framework).

### Phase 4: Ecosystem Growth (Q4 2026 and beyond)

**Objective:** Grow the adopter base, deepen integration lanes, and evaluate formal standardization.

**Key deliverables:**
- Additional integration lanes based on adopter demand
- Expanded fixture coverage for new use cases
- Formal standardization decision (pursue or explicitly defer)
- Community governance expansion (additional maintainers, TSC members)

**External visibility:** Sustained community engagement. Regular releases, conference presence, standards body participation where appropriate.

---

## 6. Pitch Materials Index

The following existing documents serve as pitch and outreach materials:

| Document | Audience | Location |
|---|---|---|
| One-paragraph description | Anyone (30-second context) | [`docs/explainers/paragraph.md`](explainers/paragraph.md) |
| One-pager | Business and technical evaluators | [`docs/explainers/one-pager.md`](explainers/one-pager.md) |
| Full briefing | Deep technical evaluation | [`docs/explainers/full-briefing.md`](explainers/full-briefing.md) |
| Agent briefing (with pitch templates) | AI agents, sales contexts | [`docs/explainers/agent-briefing.md`](explainers/agent-briefing.md) |
| Animation production briefing | Visual communicators | [`docs/explainers/animation-briefing.md`](explainers/animation-briefing.md) |
| AI full briefing | AI agents (comprehensive) | [`docs/UNIVERSAL-MANIFEST-BRIEFING.md`](UNIVERSAL-MANIFEST-BRIEFING.md) |
| Standards positioning | Standards body evaluators | [`docs/STANDARDS-POSITIONING.md`](STANDARDS-POSITIONING.md) |
| Integration lane docs (9 lanes) | Domain-specific evaluators | [`integrations/`](../integrations/) |

### Pitch templates available

The agent briefing ([`docs/explainers/agent-briefing.md`](explainers/agent-briefing.md)) contains three ready-to-use pitch templates:

1. **30-second elevator pitch** — for casual introductions
2. **2-minute technical pitch** — for developer audiences and technical evaluators
3. **Partnership proposal opening** — for outreach to potential adopter organizations

---

## 7. Success Metrics

### Adoption metrics

| Metric | Phase 2 Target | Phase 3 Target | Phase 4 Target |
|---|---|---|---|
| Organizations that have attempted implementation | 2+ | 5+ | 10+ |
| Independent implementations passing conformance | 0 | 3+ | 5+ |
| GitHub stars | -- | 100+ | 500+ |
| npm package downloads (weekly) | -- | 50+ | 500+ |

### Engagement metrics

| Metric | Phase 2 Target | Phase 3 Target | Phase 4 Target |
|---|---|---|---|
| GitHub issues from external contributors | 5+ | 20+ | 50+ |
| External pull requests | 1+ | 5+ | 15+ |
| Standards body presentations delivered | 0 | 2+ | 4+ |
| Conference talks delivered | 0 | 1+ | 3+ |

### Feedback metrics

| Metric | How Measured |
|---|---|
| Time from first contact to first manifest parse | Track during beta onboarding |
| Adopter-reported friction points | Feedback loop system (WO-0056) |
| Spec change proposals from external adopters | RFC submissions |
| Integration lane requests from adopters | GitHub issues |

---

## 8. Conference and Presentation Plan

### Target events (by domain alignment)

| Event | Domain | Relevance | Typical Submission Deadline |
|---|---|---|---|
| Internet Identity Workshop (IIW) | Identity / DIDs / VCs | Core audience for portable identity standards | ~2 months before event |
| W3C TPAC | Web standards | W3C community engagement, VC/DID working groups | ~3 months before event |
| Rebooting the Web of Trust (RWoT) | Decentralized identity | Design workshop format, deep technical engagement | ~2 months before event |
| Decentralized Web Summit | Decentralized systems | Broad decentralized tech community | ~3 months before event |
| GDC (Game Developers Conference) | Gaming | Cross-game identity portability use case | ~6 months before event |
| AWE (Augmented World Expo) | Smart glasses /  Spatial computing | Smart glasses consent model, spatial fabric | ~4 months before event |
| Metaverse Standards Forum meetings | Metaverse / interoperability | MSF lineage, metaverse integration lane | Ongoing (working group schedule) |
| OMA3 events | Web3 / interoperability | OMATrust integration lane | Varies |
| FOSDEM | Open source | Open-source standards community | ~3 months before event |
| Open Source Summit (Linux Foundation) | Open source | Linux Foundation community, potential hosting path | ~4 months before event |

### Talk abstracts (ready to adapt)

**Title:** "Universal Manifest: One Portable Document for Identity, Credentials, and Consent"

**Abstract (200 words):** Every time two systems need to share information about a user, someone builds a custom integration. Profile sync, credential verification, consent propagation -- each one is a unique data format with its own API, its own auth flow, and its own maintenance burden. Multiply by every pair of systems, and the cost is staggering.

Universal Manifest is an open-source JSON-LD document format that replaces this proliferation with one portable state capsule. A single manifest carries identity references, verified claims, privacy consents, device registrations, and pointers to authoritative data sources. It works offline (every manifest expires automatically). It works at the edge (no phone-home required). It works with existing standards (JSON-LD, DIDs, Verifiable Credentials, Ed25519). And it carries consent natively -- nothing is shared without explicit permission.

This talk introduces UM's architecture, demonstrates real-world integration scenarios (social profile portability, smart glasses consent enforcement, IoT device enrollment), and shows how to go from parsing your first manifest to issuing signed documents in minutes. The specification is open source (Apache-2.0), production infrastructure is live, and adoption is progressive -- start by parsing JSON, add capabilities at your own pace.

---

## References

- [`docs/explainers/one-pager.md`](explainers/one-pager.md) — One-pager explainer
- [`docs/explainers/full-briefing.md`](explainers/full-briefing.md) — Full briefing with competitive positioning
- [`docs/explainers/agent-briefing.md`](explainers/agent-briefing.md) — Agent briefing with pitch templates
- [`docs/STANDARDS-POSITIONING.md`](STANDARDS-POSITIONING.md) — Standards positioning
- [`docs/governance/GOVERNANCE.md`](governance/GOVERNANCE.md) — Governance structure
- [`docs/DONE-DONE-DEFINITION.md`](DONE-DONE-DEFINITION.md) — Done-done framework (maturity gates)
- [`integrations/`](../integrations/) — All integration lane documents
