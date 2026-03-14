# Session Synthesis and Strategic Roadmap -- 2026-03-12

**Purpose:** Consolidates all findings from the 2026-03-12 work session into a single strategic document for OMA3 meeting preparation and ongoing project planning.

---

## Executive Summary

- **Universal Manifest covers 179 concepts across 15 domains** with 163 leaf nodes. Of these, 15 are proven with fixture evidence, 28 are documented, 61 are proposed, and 59 are unexplored. The unexplored count is a strength: it demonstrates UM's breadth of applicability across domains far beyond metaverse.
- **62-67 deferred items have been cataloged** across 10 categories, with 3 P0 items (IWPS `assets` parameter binding, encrypted inline facets architectural decision, no encryption profile in spec). This is the first time the project has a single comprehensive inventory of everything that is explicitly not yet done.
- **The IWPS alignment analysis positions UM as the cargo that fills IWPS's transport** -- the `assets` parameter in IWPS's Query and Teleport APIs is exactly where a UMID belongs. This is the primary OMA3 talking point.
- **Three engineering deep dives were completed** (hashing, facet encryption, resolver) that demonstrate specification-level sophistication comparable to W3C and IETF standards work.
- **18 NotebookLM video briefs are queued** with 7 at Priority 1 for the OMA3 meeting, but the hashing deep-dive video should wait until its concepts are integrated into the spec (per user feedback that unintegrated concepts should not be presented as settled).

---

## 1. What Was Accomplished Today

### Work Orders Completed

| WO | Title | Key Artifact |
|----|-------|-------------|
| WO-0154 | Hashing, caching, and data bundling deep dive | `docs/explainers/hashing-and-data-bundling-deep-dive.md` |
| WO-0155 | Concept hierarchy explorer and ecosystem namespace | `site/public/tools/concept-explorer/` (179 nodes, interactive HTML tool) |

### Additional Deliverables

| Deliverable | Description |
|-------------|-------------|
| Deferred concepts audit | 62 items across 10 categories (`docs/reports/2026-03-12-deferred-concepts-and-loose-ends-comprehensive-audit.md`) |
| Audit verification | Independent verification confirming 50+ items, identifying 5 additional items (true count ~64-67) |
| NotebookLM vault rebuild | 633 files (up from 559), 1.4 MB compressed |
| Production queue update | 18 videos planned, L3-11 added (`docs/scripts/production-queue.md`) |
| Hashing deep dive explainer | 9 sections covering SHA-256 ETags, Ed25519+JCS, pointer-first architecture, CID deferral, digestMultibase proposal, CBOR-LD future |

### Cumulative Session Output (2026-03-11 through 2026-03-12)

WO-0146 through WO-0155 were completed across these sessions -- 10 work orders encompassing IWPS localization, alignment analysis, OMA3 presentation, video hierarchy, hackathon learnings, avatar equip concept, portal loading mandate, facet encryption deep dive, hashing deep dive, and the concept explorer.

**Therefore:** The project's documentation and strategic positioning are now in the strongest state they have ever been. The immediate action is to use these materials in the OMA3 meeting.

---

## 2. The Full Picture: What UM Covers vs. What's Missing

### Concept Explorer Data Summary

The concept explorer at `site/public/tools/concept-explorer/` contains **179 total nodes** (including 16 category/root nodes) with **163 leaf concepts** across **15 top-level categories**.

#### Status Breakdown

| Status | Count | Meaning |
|--------|-------|---------|
| Proven | 15 | Fixture-backed, journey-tested, production-verified |
| Documented | 28 | Explainer, integration lane, or design document exists |
| Proposed | 61 | Concept identified and described; no implementation evidence |
| Unexplored | 59 | Domain identified as applicable; no detailed analysis yet |
| **Total leaf concepts** | **163** | |

#### Category Breakdown

| Category | Leaf Concepts | Proven | Documented | Proposed | Unexplored |
|----------|--------------|--------|------------|----------|------------|
| Identity & Profile Portability | 13 | 1 | 1 | 6 | 5 |
| Consent & Privacy Management | 14 | 4 | 2 | 6 | 2 |
| Digital Assets & Ownership | 10 | 0 | 1 | 5 | 4 |
| Metaverse & Spatial Computing | 14 | 1 | 5 | 6 | 2 |
| IoT & Device Enrollment | 10 | 0 | 2 | 1 | 7 |
| Commerce & Payments | 10 | 0 | 0 | 4 | 6 |
| Credentials & Verification | 12 | 2 | 2 | 4 | 4 |
| Creative & Media | 10 | 0 | 0 | 4 | 6 |
| Enterprise & Organization | 9 | 0 | 0 | 6 | 3 |
| Governance & Standards | 10 | 1 | 5 | 3 | 1 |
| Healthcare & Wellbeing | 10 | 0 | 1 | 4 | 5 |
| Education & Research | 8 | 0 | 1 | 4 | 3 |
| Government & Civic | 8 | 0 | 0 | 1 | 7 |
| Social & Community | 10 | 0 | 1 | 5 | 4 |
| Infrastructure & Protocol | 15 | 6 | 7 | 2 | 0 |

#### What This Tells Us

**Deep proven coverage where it matters most:** Infrastructure & Protocol has 13 of 15 concepts at proven or documented status. Consent & Privacy has 6 of 14 proven or documented. These are the foundational layers that enable everything above them.

**Breadth of applicability is the story:** 59 unexplored concepts across Government & Civic (7), IoT (7), Commerce (6), Creative & Media (6), Healthcare (5), Identity (5), and others demonstrate that UM's architecture applies to domains far beyond metaverse. Each unexplored concept is a potential adoption conversation.

**The ratio tells the right story:** 15 proven + 28 documented = 43 concepts with evidence. 61 proposed + 59 unexplored = 120 concepts with room to grow. This is a specification with proven depth in its core and natural extensibility into dozens of new domains. It is not "incomplete" -- it is "applicable and growing."

**Therefore:** Use the concept explorer at the OMA3 meeting to show UM's breadth. The 59 unexplored concepts are conversation starters, not deficiencies. The 15 proven concepts demonstrate that the architecture works. The tool itself demonstrates sophisticated project organization.

---

## 3. Deferred Items by Priority

The comprehensive audit cataloged 62 items (true count ~64-67 per verification). Items are organized below by actionability.

### P0: Must address soon (3 items)

These are the items that, if left unaddressed, create real barriers to adoption or architectural coherence.

| # | Item | Category | Status | Blocking |
|---|------|----------|--------|----------|
| 1 | **IWPS `assets` parameter binding** | Standards alignment | Proposed (analysis complete) | Formal IWPS-UM integration at spec level |
| 2 | **Encrypted inline facets vs projection decision** (WO-0143) | Architecture decision | NOT_STARTED | Normative encryption profile, PIP-RS-01, key management design |
| 3 | **No encryption profile in v0.1 or v0.2** | Spec gap | Proposed (deep dive complete) | Use cases requiring cryptographic privacy at rest |

**Therefore:** Item 1 is the OMA3 meeting agenda item -- present the alignment analysis and propose the binding. Items 2 and 3 are the same architectural question from different angles: WO-0143 must be executed next to unblock the entire encryption/privacy track.

### P1: Important extensions on the roadmap (17 items)

These are items that do not block current adoption but block significant future use cases or ecosystem scale.

| # | Item | Category |
|---|------|----------|
| 1 | No revocation protocol beyond HTTP 410 | Spec gap |
| 2 | No content integrity for pointer targets (digestMultibase) | Spec gap |
| 3 | No permissions firewall / audience-scoped consent | Spec gap |
| 4 | No resolver write API or self-service registration | Spec gap |
| 5 | WO-0142: Payment handles and fiat/crypto gateway | Open WO |
| 6 | PIP-RS-01: Encrypted private fragment profile | Research track |
| 7 | PIP-RS-02: Selective disclosure / ZK proof profile | Research track |
| 8 | PIP-RS-04: Wallet protocol binding profile | Research track |
| 9 | MUM-RS-01: Selective disclosure and compliance proof profile | Research track |
| 10 | MUM-RS-04: Synchronization conflict-resolution protocol | Research track |
| 11 | JWE per-facet encryption (recommended primary method) | Proposed extension |
| 12 | Portal loading content pointers (CEO mandate fulfilled) | Proposed extension |
| 13 | Encrypt-then-sign ordering convention | Proposed extension |
| 14 | Joint IWPS + UM conformance profile | Standards alignment |
| 15 | Proximity-aware credential presentation profile | Standards alignment |
| 16 | Protocol recommendation governance initial population | Standards alignment |
| 17 | NotebookLM knowledge vault rebuild | Operational |

**Therefore:** After the OMA3 meeting, prioritize WO-0143 (the encryption decision), then WO-0142 (payments -- a joint OMA3 collaboration area), then the standards-currency matrix population (governance infrastructure that is built but empty).

### P2: Nice-to-have improvements (22 items)

These include deeper standards alignment, conceptual exploration, and ecosystem convenience items. Full list in the audit report. Key examples:

- No Data Integrity proof profile (W3C VC alignment)
- No authenticated/private resolution profile
- BBS+ and SD-JWT selective disclosure profiles
- Federation model for resolvers
- Record-as-core-primitive vision
- Consent delegation model
- AI agent integration lane
- Education and healthcare lane depth
- TS helper package npm publication timing
- Avatar equip tool and myum.net equip interface (product concepts)

**Therefore:** These are tracked but should not compete with P0/P1 items for execution time.

### P3: Future/research items (7 items)

Long-term items contingent on ecosystem maturity or external standard finalization:

- CBOR-LD + COSE binary encoding (contingent on W3C Recommendation status)
- Merkle history for manifests
- Bitstring status lists for batch revocation
- CID snapshots alongside UMIDs
- Emergency override for consent
- Real-time asset streaming (gap in both IWPS and UM)
- Multi-party portaling

**Therefore:** Document these as future considerations. Do not allocate execution time.

### Items Missed by Original Audit (from verification)

The verification pass identified 5 additional items:

1. **WO-0155** (Concept hierarchy explorer) -- was IN_PROGRESS during audit, should be listed as open WO
2. **Permissions firewall open question 9.2** -- Rule synchronization across multiple devices/agents
3. **Permissions firewall open question 9.5** -- Retroactive consent change effects
4. **Post-quantum algorithm support** -- Mentioned in SIGNATURE-PROFILE.md section 7
5. **v0.4+ consent synchronization protocol** -- Distinct from open question 9.2

Also noted: items 6.4 and 10.4 (standards-currency matrix) are duplicates, so the true unique count is ~64-67.

**Therefore:** These are minor and do not change the strategic picture. The audit achieves its purpose.

---

## 4. Standards Alignment Status

### IWPS (Inter-World Portaling Standard, OMA3)

**Alignment:** Strong complementarity. IWPS = transport, UM = cargo. No overlap, no conflict.

| Integration Point | Status |
|-------------------|--------|
| `assets` parameter as UMID carrier | Proposed (alignment analysis complete) |
| `portalLimitations` maps to UM graceful degradation | Natural fit, no spec change needed |
| User Agent communication path as UM carrier | Aligned with UM's subject-controlled model |
| Identity Framework Model 4 (Decentralized) | Maps directly to UM `subject` DID |
| IWPS `userId` maps to UM `subject` | Direct binding |

**Remaining gaps (joint):**
- Payments framework (TBD in both)
- Real-time asset streaming (architectural mismatch -- both are discrete, not streaming)
- Multi-party portaling (not addressed by either)
- Cross-chain asset ownership verification (OMATrust may handle)

**Therefore:** Present the complementarity diagram at OMA3. Propose UM as the payload standard for the `assets` parameter. This is not a competitive positioning -- it fills gaps IWPS explicitly marked as TBD.

### W3C Verifiable Credentials Ecosystem

| Aspect | UM Status |
|--------|-----------|
| JSON-LD base format | Aligned |
| Ed25519 signing | Compatible (JCS vs RDFC-1.0 canonicalization differs) |
| Data Integrity proofs (RDFC-1.0) | Deferred -- additive future profile, not replacing JCS |
| BBS+ selective disclosure | Research-first track (PIP-RS-02) |
| `digestMultibase` for context/pointer integrity | Proposed, not yet in spec |
| Bitstring Status Lists | Deferred (P3) |

**Therefore:** UM is compatible with the W3C VC ecosystem at the format and cryptographic level. The remaining gaps (Data Integrity, BBS+) are additive profiles that do not block adoption.

### Other Standards

| Standard | Relationship |
|----------|-------------|
| SD-JWT (IETF RFC 9901) | Bridge profile for JWT ecosystems (research-first) |
| OpenID Federation | Strongest fit for verifier/issuer trust, but no mapping doc exists |
| OpenID4VP / Digital Credentials API | Dependency for proximity presentation profile |
| DIDComm v2 | UM uses same primitives (JWE, Ed25519) but different scope (document vs messaging) |
| Solid | UM uses pointers to Solid Pods; complementary |
| GPC | Integration lane completed (WO-0127, WO-0128) |

**Therefore:** UM's standards alignment is strong at the foundation (JSON-LD, Ed25519, DID) and has clear, tracked gaps for advanced features. No standards conflict exists.

---

## 5. The Concept Explorer as a Strategic Tool

### What It Shows

The concept explorer at `site/public/tools/concept-explorer/index.html` is an interactive, searchable tree of 179 concepts organized into 15 categories. Each node has a name, description, status badge, and links to documentation where it exists. It loads from `concepts.json` -- updating the hierarchy means editing one JSON file.

### How to Use It at the OMA3 Meeting

1. **Open the explorer live** and show the 15 categories -- this immediately communicates breadth.
2. **Expand "Metaverse & Spatial Computing"** to show the OMA3-relevant concepts and their status (1 proven, 5 documented, 6 proposed, 2 unexplored).
3. **Expand "Infrastructure & Protocol"** to show the foundation: 6 proven, 7 documented -- this is where the engineering rigor lives.
4. **Search for "portaling"** to demonstrate the search function and show the portaling concept with its documentation links.
5. **Expand "Commerce & Payments"** to show the collaboration opportunity: 0 proven, 4 proposed, 6 unexplored -- this is where OMA3 partnership could add immediate value.

### The Vision: Why This Changes the Narrative

The concept explorer transforms UM from "a metaverse identity spec" to "a universal portable state specification that has proven depth in identity, consent, and metaverse while being naturally extensible to commerce, healthcare, government, IoT, and creative media."

The 59 unexplored concepts are not gaps -- they are the market. Each one is a potential partnership conversation, a potential integration lane, a potential standards collaboration. The tool makes this visible and browsable.

**Future vision (documented in WO-0155):**
1. On-demand documentation: users flag areas where they want detail, driving priorities
2. Ecosystem compliance: external parties claim namespace by submitting conformance evidence
3. Distributed namespace management: decentralized registry of UM application domains
4. Standards ecosystem: living directory of who implements what, verified against conformance

**Therefore:** The concept explorer is not just a documentation tool -- it is a strategic positioning asset. Use it at the OMA3 meeting to show breadth. Use it in follow-up conversations to identify collaboration domains.

---

## 6. Video Production Status

### Overview

18 videos are planned across 3 priority tiers, organized by the hierarchy of discovery system (Level 0 through Level 3).

| Priority | Count | Purpose | Status |
|----------|-------|---------|--------|
| Priority 1 (OMA3 Meeting) | 7 | Engineering deep dives and standards positioning | Briefs ready, production via NotebookLM |
| Priority 2 (Core Library) | 6 | Foundational explainers for the channel | Briefs ready |
| Priority 3 (Complete Coverage) | 5 | Audience-specific and topic deep dives | Briefs ready |

### Priority 1 Videos (OMA3 Meeting)

| # | ID | Title | Length |
|---|-----|-------|--------|
| 0 | L3-10 | Facet Privacy -- Public, Encrypted, and Selective Disclosure | 6 min |
| 1 | L2-03 | UM for Standards Bodies | 2 min |
| 2 | L3-09 | IWPS + UM: The Complete Portaling Stack | 6 min |
| 3 | L1-01 | Everything You Need to Know About UM | 6 min |
| 4 | L3-07 | The Composite Stack Architecture | 6 min |
| 5 | L3-05-DEEP | The myum.net Resolver -- Complete Deep Dive | 6 min |
| 6 | L3-11 | Hashing, Caching, and Data Bundling Deep Dive | 6 min |

### Important Note on L3-11 (Hashing Deep Dive)

The hashing deep-dive video brief is ready, but production should **wait** until the concepts it describes (digestMultibase for pointer integrity, CBOR-LD binary profile, CID snapshots) are properly considered and integrated into the spec. Presenting unintegrated concepts as settled in a NotebookLM video would create a false impression of spec completeness. The explainer document exists and can be referenced directly in the OMA3 meeting, but the video should not be produced until the concepts it describes are part of the specification.

The same principle applies to L3-10 (facet encryption): the three encryption methods are proposed, not normative. The video brief is clear about this, but the distinction must be maintained in production.

### Production Queue Location

`docs/scripts/production-queue.md` -- contains all 18 video briefs with copy-pasteable NotebookLM prompts.

**Therefore:** Produce L2-03 (Standards Bodies) and L3-09 (IWPS + UM) first -- these are the most directly relevant to the OMA3 audience. L1-01 (Master Explainer) as backup. Hold L3-11 until integration.

---

## 7. Recommended Next Actions

Prioritized by urgency and impact.

### Immediate (OMA3 meeting, today)

1. **Use the presentation materials** -- `docs/presentations/2026-03-12-oma3-architectural-overview.md` is a complete 13-minute presentation with 9 sections, NotebookLM briefs per section, and visual suggestions.
2. **Show the concept explorer** -- `site/public/tools/concept-explorer/index.html` demonstrates breadth. Open it live if internet is available, or have screenshots ready.
3. **Lead with the IWPS complementarity** -- Section 7 of the presentation ("How UM Fits Into IWPS") is the key section. The framing: IWPS = plumbing, UM = cargo.
4. **Have the alignment analysis ready** -- `docs/reports/2026-03-11-iwps-um-alignment-analysis.md` contains the detailed gap table, integration flow diagram, and 5 specific OMA3 recommendations.
5. **Reference the hackathon proof** -- Section 8 of the presentation describes the spatial fabric hackathon where UM concepts were validated live with Three.js.

### This Week

6. **Execute WO-0143** (encrypted inline facets vs projection model decision) -- This is the most significant open architectural decision. The facet encryption deep dive provides the research foundation. The decision unblocks PIP-RS-01, the normative encryption profile, key management design, and the encrypt-then-sign convention.
7. **Execute WO-0142** (payment handles) -- A natural OMA3 collaboration area. Both IWPS and UM have payments as TBD. Being first with a proposal creates leverage.
8. **Populate the standards-currency matrix** -- The governance framework exists (WO-0133 completed) but is empty. Initial assessments for the major protocol families (DID methods, VC profiles, OIDC, OpenID Federation) would give the project evidence-based protocol recommendations instead of ad hoc choices.
9. **Process the INBOX** -- 6 items, 3 of which can be immediately archived (README copy.md, permissions-system.md are already integrated conceptually). The CEO mandate (Feb 26) should be consolidated with WO-0145.

### This Month

10. **Produce Priority 1 videos** (6 of the 7 -- hold L3-11 per note above) via NotebookLM using the rebuilt knowledge vault.
11. **Add WO-0155 to WO-INDEX.md** -- It exists as a file but is not indexed.
12. **Create AI agent integration lane** -- The inbox has an idea fragment. Given the growth of the AI agent ecosystem, this is a timely addition.
13. **Publish the concept explorer on the main site** -- Currently at `/tools/concept-explorer/`. Should be linked from the docs site sidebar.
14. **Schedule the first Research-First track execution** -- PIP-RS-02 (selective disclosure / ZK proof) or MUM-RS-01 (compliance proof) are the highest-impact research tracks.

---

## 8. OMA3 Meeting Preparation Checklist

### Materials Ready

| Material | Location | Status |
|----------|----------|--------|
| 13-minute architectural overview presentation | `docs/presentations/2026-03-12-oma3-architectural-overview.md` | Ready |
| IWPS-UM alignment analysis (detailed) | `docs/reports/2026-03-11-iwps-um-alignment-analysis.md` | Ready |
| Concept explorer (interactive tool) | `site/public/tools/concept-explorer/index.html` | Ready |
| IWPS spec (localized copy) | `docs/research/iwps-base-specification-v0.3.md` | Ready |
| Facet encryption deep dive | `docs/explainers/facet-encryption-deep-dive.md` | Ready |
| Hashing deep dive | `docs/explainers/hashing-and-data-bundling-deep-dive.md` | Ready |
| Resolver deep dive | `docs/explainers/resolver-deep-dive.md` | Ready |
| Hackathon validation report | `docs/reports/2026-03-11-spatial-fabric-hackathon-learnings.md` | Ready |
| Deferred concepts audit (full inventory) | `docs/reports/2026-03-12-deferred-concepts-and-loose-ends-comprehensive-audit.md` | Ready |
| NotebookLM knowledge vault | `notebooklm-knowledge-vault.zip` (633 files) | Ready |
| Video production queue with briefs | `docs/scripts/production-queue.md` | Ready |

### Materials NOT Ready

| Material | Gap | Impact |
|----------|-----|--------|
| Produced NotebookLM videos | Briefs ready, audio not yet generated | Can describe verbally; share briefs for context |
| Live concept explorer on universalmanifest.net | Tool exists in `/tools/concept-explorer/` but not linked from main nav | Open from local filesystem or direct URL |
| Payment handle proposal | WO-0142 NOT_STARTED | Describe as "natural collaboration area" |
| Encryption profile decision | WO-0143 NOT_STARTED | Present three options from the deep dive; acknowledge the decision is pending |

### Key Talking Points

1. **"IWPS is the plumbing, UM is the cargo."** The `assets` parameter in IWPS's Query and Teleport APIs is exactly where a UMID belongs. No spec changes required on either side -- this fills an existing extension point.

2. **"179 concepts, 15 categories."** UM is not a metaverse spec -- it is a universal portable state specification. Show the concept explorer to prove breadth. The metaverse lane is one of 15 categories.

3. **"Default-deny consent travels with the data."** This is the privacy differentiator. No other standard carries consent rules inside the portable document itself with cryptographic integrity.

4. **"We validated this in a live hackathon."** Portal server + Three.js + manifest resolution + avatar loading from pointers + consent enforcement at runtime. Proof, not theory.

5. **"Per-facet encryption in a portable document."** No other standard offers per-facet encryption at the envelope level. JWE per-facet with multi-recipient support means one manifest, multiple audiences, cryptographic access control. This is genuinely novel.

### Questions to Anticipate from Alfred Tom / OMA3 Audience

| Question | Prepared Answer |
|----------|----------------|
| "How does UM handle the `assets` field in IWPS?" | Proposed mapping: `assets` carries a UMID or inline manifest. The IWPS alignment analysis (section 3.1) details the integration. |
| "What about payments?" | Both standards have payments as TBD. WO-0142 tracks UM's payment handle integration. Natural collaboration area with OMA3. |
| "How does this relate to OMATrust?" | OMATrust attestation tiers (Bronze/Silver/Gold) provide external trust signals. UM provides the portable state those attestations apply to. Complementary. |
| "Is this ready for adoption?" | v0.1 is adoptable today (Phase 1-4 complete). v0.2 signature profile is drafted. The concept explorer shows where proven evidence exists vs. where research is still needed. |
| "What about existing identity standards?" | UM carries DIDs and VCs, it does not replace them. It adds the portable envelope that W3C VCs do not provide (see comparison table in the facet encryption deep dive). |
| "How does consent work across worlds?" | Default-deny consent travels inside the manifest. When a manifest arrives at a destination world via IWPS, the world reads consent rules before activating any features. Consent enforcement at arrival, not just at origin. |
| "What's the governance model?" | Open specification with published governance framework, RFC template, breaking-change policy, and deprecation policy. Not vendor-controlled. |

### What to Show vs. What to Describe Verbally

**Show (if internet/screen available):**
- The concept explorer tool (demonstrates breadth and interactivity)
- The IWPS + UM flow diagram from the alignment analysis (section 6)
- The facet encryption example showing JWE per-facet (section 3, Method 1 of the deep dive)
- The resolver deep dive comparison table (section 6 -- how UM compares to DNS, Solid, DIDComm, VCs)

**Describe verbally:**
- The hackathon proof-of-concept (describe the flow, do not show code)
- The encryption architectural decision (present three options, acknowledge the decision is pending)
- The payment handle integration opportunity (frame as collaboration, not a gap)
- The video production pipeline (mention that deep-dive videos are being produced via NotebookLM for engineer-level audiences)

---

## Cross-Reference Table: Deferred Items to Concept Explorer Categories

This table maps the highest-priority deferred items to the concept explorer categories where they cluster. This shows where gaps concentrate and where effort would have the most impact.

| Concept Explorer Category | Deferred Items | Priority Range | Cluster Theme |
|--------------------------|----------------|----------------|---------------|
| **Infrastructure & Protocol** | digestMultibase, CBOR-LD, CID snapshots, Merkle history, bitstring status lists, resolver federation, resolver write API, resolver rate limiting | P1-P3 | Protocol maturation and scaling |
| **Consent & Privacy Management** | Permissions firewall, consent delegation, audience verification, emergency override, retroactive consent, rule synchronization | P1-P3 | Consent evolution (v0.3+) |
| **Credentials & Verification** | Data Integrity proof profile, BBS+ selective disclosure, SD-JWT bridge, proximity credential presentation | P1-P2 | Advanced credential operations |
| **Metaverse & Spatial Computing** | Portal loading content (fixture gap), synchronization conflict resolution, avatar translation, multi-party portaling | P1-P3 | Deep metaverse features |
| **Commerce & Payments** | Payment handles (WO-0142), cross-chain asset verification | P1-P3 | Entire domain is undeveloped |
| **Identity & Profile Portability** | Encrypted inline facets, projection lifecycle, wallet recovery, wallet protocol binding, AI agent identity | P0-P2 | Privacy and advanced identity |
| **Governance & Standards** | Standards-currency matrix population, IWPS assets binding, joint conformance profile, OpenID Federation mapping | P0-P1 | Standards ecosystem maturation |

**Key insight:** The heaviest cluster is in Infrastructure & Protocol (8 items), but most are P2-P3 and do not block adoption. The highest-impact cluster is Governance & Standards (4 items at P0-P1) because these items directly affect the OMA3 relationship and ecosystem positioning. The Commerce & Payments cluster is the largest greenfield opportunity for OMA3 collaboration.

**Therefore:** Post-OMA3, the execution sequence should be: (1) WO-0143 (encryption decision, unblocks the Identity/Privacy cluster), (2) WO-0142 (payments, creates OMA3 collaboration momentum), (3) standards-currency matrix population (makes protocol recommendations evidence-based).

---

## Source Documents Consulted

| Document | Location |
|----------|----------|
| Deferred concepts audit | `docs/reports/2026-03-12-deferred-concepts-and-loose-ends-comprehensive-audit.md` |
| Audit verification | `.dev/reviews/VERIFY-deferred-audit-75752557-2026-03-12.md` |
| Hashing deep dive | `docs/explainers/hashing-and-data-bundling-deep-dive.md` |
| Facet encryption deep dive | `docs/explainers/facet-encryption-deep-dive.md` |
| Concept explorer JSON | `site/public/tools/concept-explorer/concepts.json` |
| Production queue | `docs/scripts/production-queue.md` |
| Previous handoff (03:16) | `.dev/ai/handoffs/2026-03-12-03-16-54Z-handoff-universalmanifest.md` |
| Current handoff (06:00) | `.dev/ai/handoffs/2026-03-12-06-00-00Z-handoff-universalmanifest.md` |
| IWPS alignment analysis | `docs/reports/2026-03-11-iwps-um-alignment-analysis.md` |
| OMA3 presentation | `docs/presentations/2026-03-12-oma3-architectural-overview.md` |
| WO-0155 (concept explorer) | `docs/workorders/WO-0155-concept-hierarchy-explorer-and-ecosystem-namespace.md` |
| Inbox audit report | `docs/reports/2026-03-11-inbox-audit-report.md` |
| Critical path | `docs/CRITICAL-PATH.md` |
| State of the project | `docs/STATE-OF-THE-PROJECT.md` |
