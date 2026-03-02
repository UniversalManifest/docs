# Universal Manifest -- Project Completeness and Vision Audit

**Date:** 2026-03-01
**Auditor:** Claude Opus 4.6 (comprehensive project audit agent)
**Scope:** Full assessment of how well the Universal Manifest project documents and communicates its purpose, methodology, public presence, integration strategy, adoption plan, and standards body positioning.

---

## 1. Executive Summary

The Universal Manifest project has built an unusually thorough internal documentation corpus. The "what UM is" story is told exceptionally well in `docs/explainers/` -- the one-pager, full briefing, agent briefing, and paragraph explainer are among the strongest assets in the repo. The development methodology (done-done framework, journey-driven proof, work-order discipline) is documented to a degree rarely seen in open-source standards projects. The website (`universalmanifest.net`) has a professional Starlight-based site with organized navigation, animated SVG explainers, and interactive tooling (workbench, harness).

However, the project has significant gaps in three critical external-facing areas: (1) there is no standalone "how to adopt UM" guide for third parties separate from the internal development docs; (2) there is no documented outreach, launch, or adoption strategy for getting UM into the hands of external adopters; and (3) the standards body positioning is implicit and reactive rather than explicit and strategic -- references to OMA3, W3C, IETF, and the Metaverse Standards Forum exist, but there is no positioning document that explains UM's relationship to formal standardization processes or whether/when/how the project intends to engage with them.

The strongest areas are: problem articulation, core concept explanation, proof methodology, integration lane breadth, and production infrastructure. The weakest areas are: external adoption packaging, outreach strategy, and standards body engagement documentation.

---

## 2. What UM Solves -- Coverage Assessment

### What IS documented

The problem statement and value proposition are documented thoroughly and at multiple altitudes:

- **One paragraph:** `docs/explainers/paragraph.md` -- crisp, metaphor-driven summary ("Swiss Army Knife for personal data").
- **One-pager:** `docs/explainers/one-pager.md` -- covers the problem, the solution, who it's for, what it enables, and where to start. Six concrete scenarios. Well-written.
- **Full briefing:** `docs/explainers/full-briefing.md` -- the most comprehensive external-facing document. 184 lines covering the fragmentation problem, the solution, core concepts (each with an analogy), end-to-end lifecycle, real-world scenarios, technical foundation, adoption path (5 levels), competitive positioning (W3C VCs, DIDComm, Solid, OIDC), FAQ, and resource links.
- **Agent briefing:** `docs/explainers/agent-briefing.md` -- structured for AI agent consumption with key facts table, positioning statements for four audiences (developers, business, privacy advocates, standards bodies), pitch templates (30-second, 2-minute, partnership opening), and differentiation bullets.
- **AI full briefing:** `docs/UNIVERSAL-MANIFEST-BRIEFING.md` -- the deepest explainer at 537 lines, covering core contract, v0.2 signatures, resolution, nine real-world integration scenarios with concrete manifest examples, architecture summary, and design principles.
- **Animation briefing:** `docs/explainers/animation-briefing.md` -- visual language guide for producing explainer animations, with character descriptions, color palette, and five suggested animation sequences.

The "why" is clearly separated from the "how" in the explainer documents. The fragmentation problem is stated concretely:

> "Today, every pair of systems that needs to exchange information about a user invents its own format. Your social profile, your login credentials, your device registrations, your privacy preferences -- they all live in different shapes, in different places, with no common structure." (`docs/explainers/one-pager.md`, line 9)

### Where a newcomer learns what UM is for

A newcomer arriving at `universalmanifest.net` would land on the site index (`site/src/content/docs/index.md`), which provides a clear, technical overview. They would then be directed to "Getting Started -> What Is Universal Manifest?" (`getting-started/universal-manifest-overview.md`), which covers the problem, the solution, who it is for, current integration targets, a high-level flow diagram, and a minimum adoption path.

The `docs/explainers/` directory is an internal resource, not directly linked from the public site. This is a missed opportunity -- the one-pager and full briefing are the project's strongest external-facing documents but are not surfaced on `universalmanifest.net`.

### What's missing or incomplete

| Gap | Status |
|-----|--------|
| The explainer documents (`docs/explainers/`) are not published on `universalmanifest.net` | MISSING |
| No single "elevator pitch" page on the public site for non-technical evaluators | MISSING |
| The site overview page is technically competent but does not lead with the human problem ("your data is trapped in silos") -- it leads with the format description | INCOMPLETE |
| No "Why UM?" comparison page on the public site (the competitive positioning in `full-briefing.md` is excellent but repo-only) | MISSING |
| Commercial journeys exist (`docs/journeys/commercial/`) but are not published on the site | MISSING |

---

## 3. How It's Being Built -- Coverage Assessment

### Development methodology

The development methodology is documented to an exceptional degree:

- **Done-done definition:** `docs/DONE-DONE-DEFINITION.md` -- 303 lines defining maturity targets (A: early-adopter, B: production-candidate, C: world-ready), seven acceptance gates (G1-G7), evidence requirements, prohibited completion claims, and sign-off protocol. This is unusually rigorous for an open-source standards project.
- **Done-done checklist:** `docs/DONE-DONE-CHECKLIST.md` -- actionable gate-by-gate checklist with evidence path requirements.
- **Critical path:** `docs/CRITICAL-PATH.md` -- nine phases from "define done" through "drift governance and closure-regression checks." Each phase has a clear goal, must-haves, and verification commands.
- **Work order system:** 68 work orders (`WO-0001` through `WO-0068`), 52 completed, with two new waves defined. Work orders are tracked in `docs/workorders/` and indexed.
- **State-of-the-project:** `docs/STATE-OF-THE-PROJECT.md` -- comprehensive snapshot with current status, work-order status, milestone progress, and verification outputs.

### Proof model (journeys, fixtures, smoke tests)

The proof model is one of the project's strongest differentiators:

- **Journey definitions:** 11 canonical journeys (`J01` through `J11`) documented in `docs/journeys/`, covering parse-and-ignore, TTL, signature verification, UMID resolution, edge-to-display smoke, public profile projection, RP1 spatial fabric, smart-glasses consent, metaverse cross-world, multi-provider personhood, and OMATrust attestation.
- **Executable proof suite:** `packages/universal-manifest/scripts/run-journeys.mjs` -- writes a JSON report to `docs/journeys/_artifacts/`.
- **Journey README:** `docs/journeys/README.md` -- documents the philosophy:

> "The Universal Manifest project does not consider 'docs exist' as proof. Maturity claims require runnable evidence." (line 85-86)

- **Fixture suite:** 46 committed fixtures (31 v0.1 + 15 v0.2) covering valid, invalid, and domain-specific stubs across all integration lanes. [CORRECTION 2026-03-01: Original report stated "40 v0.1 + 6 expanded" -- actual committed breakdown is 31 v0.1 (4 valid + 16 stubs + 11 invalid) and 15 v0.2 (4 valid + 11 invalid). One additional uncommitted stub exists.]
- **Production smoke:** `packages/universal-manifest/scripts/smoke-endpoints.mjs` -- endpoint verification for both dev and prod environments.

### Connection to deliverables

The done-done framework is well-connected to deliverables through the gate structure and evidence-pack template. The critical path phases map directly to work orders and milestones. The journey system maps directly to executable tests. This is a well-integrated methodology.

### What's missing

| Gap | Status |
|-----|--------|
| The development methodology is not explained on the public site -- a newcomer would not discover the done-done framework unless they browse governance docs | SCATTERED |
| No "how we build this" page that explains the journey-driven approach to a potential contributor | MISSING |
| The teaching scripts system (`docs/teaching-scripts/`) is at Stage 3 (script ideas) -- no actual scripts or animations have been produced for it yet | INCOMPLETE |
| The interactive sandbox (WO-0060 through WO-0068) is defined and mandated but not yet implemented | INCOMPLETE |

---

## 4. What the Website Does -- Coverage Assessment

### Current site content

The site (`universalmanifest.net`) is built with Astro/Starlight and has the following navigation structure:

1. **Overview** -- landing page with core model explanation, animated flow diagram, adoption paths
2. **Getting Started** -- What Is UM?, Quick Start, Concepts, Stub Manifests, Critical Path, TypeScript Helper, Manifest Workbench
3. **Specification** -- v0.1, v0.2
4. **Conformance** -- v0.1, v0.2, Resolver
5. **Integrations** -- 7 published lanes (Social, Proof-of-Personhood, OMATrust, RP1, Smart Glasses, Metaverse, Chia DID/VC) plus 3 new lanes (Healthcare, Education, Smart Home), plus a comprehensive catalog index
6. **Publishing** -- Versioning, Releasing, Deploy Checklist, Domain Split, Production Smoke, Deploy
7. **Verification & Proof** -- Journeys, Smoke, Harness
8. **Governance** -- Decisions, Done-Done
9. **Tools** -- Manifest Workbench, Verification Harness, Implementation Sandbox

### Site map / IA document

The site has a documented IA at `docs/site/INFORMATION-ARCHITECTURE.md`, which defines primary audiences (implementers, evaluators, maintainers), the top-level navigation, a canonical "read first" path, and a source-of-truth mapping between site pages and repo docs. There is also an editorial style guide at `docs/site/EDITORIAL-STYLE-GUIDE.md`.

### Does the site tell the "what UM is" story effectively?

The site is competent at telling the story to a technically oriented audience. The overview page leads with a format description and technical model, then provides "choose a starting path" guidance for implementers, evaluators, and deployers. The "What Is Universal Manifest?" page covers the problem, the solution, who it's for, and a minimum adoption path.

However, the site does NOT tell the story effectively for:
- Non-technical evaluators (no business-focused landing page)
- First-time visitors who need the "why" before the "how" (the site leads with structure, not problem)
- Standards body reviewers (no positioning page explaining UM's relationship to formal standards)

### Interactive sandbox

The sandbox is mandated (`docs/MANDATE-interactive-implementation-sandbox.md`) and work orders are defined (WO-0060 through WO-0068), but implementation has not started. The sandbox is envisioned as a three-panel, step-through interactive experience with real validation logic, scenario selection modal, and approximately 25+ scenarios covering the full breadth of UM capabilities.

### Workbench and harness

- **Workbench:** Published at `/getting-started/workbench/` -- browser-based tool for import, edit, validate, and export of manifests. Supports v0.1 and v0.2 templates.
- **Harness:** Published at `/proof/harness/` -- lightweight verification surface for browsing fixtures and running quick resolver checks. Has autorun mode for screenshot evidence capture.

Both are marked `hidden: true` in sidebar and accessed via the Tools section.

### Gap between what the site IS and what it SHOULD be

| Gap | Status |
|-----|--------|
| No non-technical landing page or "why UM" page for evaluators | MISSING |
| No published version of the explainer documents (one-pager, full briefing) on the site | MISSING |
| Commercial journeys not published on the site (creator, venue operator, app developer, privacy, enterprise) | MISSING |
| The workbench and harness are `hidden: true` in their sidebar entries -- discoverable only via Tools section | INCOMPLETE |
| Interactive sandbox not yet built | INCOMPLETE |
| No "Examples" or "Demos" section on the site for quick visual understanding | MISSING |
| The integration catalog (`integrations/index.md`) is comprehensive but many lanes are "Planned" with no fixture or proof coverage | INCOMPLETE |
| No changelog or release notes page on the public site | MISSING |
| 16 animated SVGs are live but not organized into a browsable gallery or tutorial sequence | SCATTERED |

---

## 5. Integration Strategy -- Coverage Assessment

### Integration lane documentation

Integration lanes are documented at two levels:

**Repo-level (`integrations/`):** 13 files covering reference-runtime, social, metaverse, RP1 spatial fabric, smart-glasses AR, proof-of-personhood, Chia DID/VC, OMATrust, healthcare, education, smart-home, runtime-profile, and a TEMPLATE.md for new lanes.

**Site-level (`site/src/content/docs/integrations/`):** 12 pages including a comprehensive catalog index organizing lanes by category (Identity & Social, Trust & Verification, Spatial & Immersive, IoT & Devices, Blockchain & Web3, Healthcare & Wellbeing, Commerce & Finance, Government & Civic, Education, Media & Entertainment). The catalog includes both published and planned lanes.

The integration catalog is genuinely impressive in scope, with 42 lanes listed across 10 categories, though only 11 are published or new. [CORRECTION 2026-03-01: Original report stated "50+ lanes" and "only 10 published" -- actual count is 42 total lanes across 10 categories. Published/New lanes number 11, not 10 (Social/Profile, Proof of Personhood, OMATrust, Metaverse, RP1, Smart Glasses, Reference Runtime, Chia DID/VC, Healthcare, Education, Smart Home).] Each published lane includes suggested claim/pointer/consent keys, fixture references, implementation checklists, and boundary statements (normative vs non-normative).

### "How to adopt UM" guide for third parties

There is no standalone adoption guide for third parties. The closest equivalent is the Quick Start page on the site, which is implementer-focused ("implement the minimum viable consumer"). The `DEPTH-AND-SCOPE.md` contains an adoption tier model (Tier 0-4) and the `full-briefing.md` contains an adoption path (Level 1-5), but neither is published as a dedicated adoption guide on the site.

The `DEPTH-AND-SCOPE.md` adoption tiers are well-designed:

> "1. Tier 0 -- Parse-only: validate `@type`, TTL, and treat unknown fields as opaque
> 2. Tier 1 -- Pointers consumer: use `pointers` to fetch canonical content
> 3. Tier 2 -- Projection renderer: render known `shards`
> 4. Tier 3 -- Verified consumer: enforce signature verification + TTL
> 5. Tier 4 -- Issuer: produce signed manifests" (lines 150-161)

But this is in an internal docs file, not on the public site.

### Resolver documentation for external use

The resolver (`myum.net`) has documentation across several files:
- `docs/DOMAIN-ARCHITECTURE.md` -- domain split rationale and resolver behavior
- `services/myum-resolver/CONTRACT.md` -- resolver contract (exists per directory listing)
- `site/src/content/docs/conformance/resolver.md` -- site page for resolver conformance
- `docs/DEPLOY-CHECKLIST.md` -- deployment instructions

The resolver has a deterministic lookup contract, error semantics, and health endpoint. However, there is no public-facing "Resolver API Reference" page on the site. The resolver documentation is split across internal and site docs without a single authoritative external reference.

### What's missing

| Gap | Status |
|-----|--------|
| No standalone "How to Adopt UM" guide for third parties | MISSING |
| The adoption tier model (from DEPTH-AND-SCOPE) is not published on the site | MISSING |
| No "Resolver API Reference" page on the public site | MISSING |
| No write/publish API for the resolver (manifests can only be added via direct KV operations) | MISSING |
| Most integration lanes in the catalog are "Planned" with no content | INCOMPLETE |
| No adoption success stories or case studies (the commercial journeys are fictional but would serve this purpose if published) | MISSING |
| The TEMPLATE.md for new integration lanes exists. The authoring guide referenced in the catalog index (`/docs/guides/integration-authoring-guide`) exists in the repo at `docs/guides/integration-authoring-guide.md` (186 lines) but is NOT published on the docs site -- there is no `site/src/content/docs/guides/` directory, making the catalog link a dead URL. | BROKEN LINK | [CORRECTION 2026-03-01: Original report said the authoring guide "does not appear to exist" -- it exists as a repo file but is not published on the site, so the site link is broken.]

---

## 6. External Exposure Plan -- Coverage Assessment

### Documented plan for getting UM into others' hands

There is **no documented outreach strategy, launch plan, or adoption roadmap** in the repo. The closest references are:

- The External Adopter Wave (WO-0053 through WO-0059) defines work orders for standalone conformance test suite, reference implementation repository, adopter onboarding document package, adopter feedback loop, spec vs implementation documentation, v0.1-to-v0.2 migration guide, and governance completion. This is a technical preparation checklist, not an outreach strategy.
- The agent briefing (`docs/explainers/agent-briefing.md`) contains a "Partnership Proposal Opening" template but no documented plan for where/when/how to use it.
- The teaching scripts system and interactive sandbox are the closest things to an "exposure strategy" -- they are designed to make UM understandable to newcomers -- but they are internal development artifacts, not a distribution plan.

### Publishing model documentation

The publishing model is well-documented:

- `docs/PUBLISHING-AND-VERSIONING.md` -- stable URLs, immutability policy, HTTP headers, caching, versioning rules, release checklist.
- `docs/RELEASING.md` -- step-by-step release process for repo and for `universalmanifest.net`.
- `docs/DEPLOY-CHECKLIST.md` -- deployment checklist for both domains.
- `docs/DOMAIN-ARCHITECTURE.md` -- domain split rationale.

These are thorough and would serve an adopter well, but they are "how we publish" docs for maintainers, not "how you consume published artifacts" docs for adopters.

### What's missing

| Gap | Status |
|-----|--------|
| No outreach strategy or adoption plan document | MISSING |
| No "launch checklist" for presenting UM publicly (beyond deploy checklists) | MISSING |
| No documented plan for conference presentations, blog posts, or community engagement | MISSING |
| No documented target adopter list or ecosystem map | MISSING |
| No plan for when/how to publish the npm package publicly | INCOMPLETE |
| No plan for soliciting early adopter feedback (WO-0056 defines a feedback system but it is NOT_STARTED) | INCOMPLETE |
| No "adopter onboarding package" (WO-0055 is defined but NOT_STARTED) | INCOMPLETE |
| The GitHub repository URL is inconsistent -- at least 4 different GitHub URLs exist across the project: `github.com/LocalArtistNetwork/universalmanifest` (site config), `github.com/WebOfTrustInfo/universal-manifest` (governance docs, CONTRIBUTING.md), `github.com/nicholasgrigoriadis/universalmanifest` (agent briefing, full briefing), and `github.com/universalmanifest/universalmanifest` (code examples) | INCONSISTENT | [CORRECTION 2026-03-01: Original report identified only 2 conflicting URLs. At least 4 distinct GitHub URLs exist across the project.]

---

## 7. Standards Body Positioning -- Coverage Assessment

### Standards bodies referenced and in what context

**OMA3 / OMATrust:**
- Most extensively referenced standards body in the project. The OMATrust integration lane is fully documented with an assessment report (`docs/reports/2026-02-22-omatrust-integration-assessment.md`), a link-coverage evidence document, integration lane docs (both repo and site), fixtures, and a journey (J11). The assessment recommends "GO, but as a staged integration lane first."
- OMA3 is referenced as the "consortium/standards-body context" while OMATrust is the "product/lane" reference. This distinction is explicitly documented.
- The assessment acknowledges maturity risks: OMATrust portals are preview/pre-alpha/testnet, some docs pages are placeholders, and the domain structure (`docs.omatrust.org` vs `docs.oma3.org`) is in transition.

**Metaverse Standards Forum (MSF):**
- Referenced exclusively in the lineage context. UM is "explicitly descended from the earlier Metaverse Universal Manifest (MUM) concept document" which was created in the MSF repo (`/Users/grig/work/MSF - Metaverse Standards Forum/repo/msf-wg-tool/geopose-talk/INBOX/`). This is documented in `docs/PROJECT-VISION.md`, `docs/DECISIONS.md`, `integrations/metaverse.md`, and `docs/PROJECT-KNOWLEDGE-INDEX.md`.
- There is no documentation about UM's current or future relationship with the MSF as an organization.

**W3C:**
- Referenced in the context of standards that UM builds on: W3C DIDs (Decentralized Identifiers), W3C Verifiable Credentials, W3C JSON-LD. The `full-briefing.md` positions UM relative to W3C VCs: "VCs are individual claims. UM is a container that can carry VCs alongside other data."
- The agent briefing contains a "For Standards Bodies" positioning statement that references JSON-LD, DIDs, JCS (RFC 8785), and Ed25519.
- No documentation exists about engaging with W3C working groups or submitting UM through a W3C process.

**IETF:**
- Referenced only indirectly through RFC citations (RFC 8785 for JCS, RFC 8615 for `.well-known`). No documentation about IETF engagement.

**Linux Foundation:**
- Referenced in the context of documentation quality benchmarking. The `research/linux-foundation-projects/2026-02/` directory contains a 10-project benchmark study used to model documentation standards for `universalmanifest.net`. The `SYNTHESIS.md` provides actionable patterns.
- `docs/DOMAIN-ARCHITECTURE.md` notes: "Makes Linux Foundation style adoption paths cleaner (spec governance != app/runtime service)."
- No documentation about submitting UM to the Linux Foundation.

### Is there a clear positioning document?

**No.** There is no dedicated document explaining UM's relationship to formal standards processes. The positioning is scattered across multiple files:
- The agent briefing has a "For Standards Bodies" paragraph (4 sentences).
- The full briefing has a "Competitive Positioning" section comparing UM to W3C VCs, DIDComm, Solid Pods, and OIDC.
- The governance document (`docs/governance/GOVERNANCE.md`) describes UM as "a standards-track specification" but does not explain which standards track or body.
- The done-done definition references "World-ready" maturity (Maturity C) but does not tie it to any formal standards process.

### Is the OMA3/OMATrust integration documented? Maturity?

Yes, this is the most mature standards-adjacent integration. The OMATrust assessment is a 260-line document covering: platform positioning, protocol model, proof and schema model, API surfaces, fit assessment (strong/medium/low areas), recommended integration architecture, and a phased implementation plan. The integration is described as high conceptual compatibility with manageable maturity risk. The lane has fixtures, a journey (J11), and live site documentation.

### Is there a strategy for standards body submission?

**No explicit strategy exists.** The only reference is in the gap analysis report (`docs/reports/2026-02-23-remaining-work-to-final-vision.md`), which lists "D.8 Formal standards body submission (if desired)" as a future-vision item requiring "months" of effort. The parenthetical "(if desired)" indicates this decision has not been made.

### What's missing

| Gap | Status |
|-----|--------|
| No "Standards Positioning" document explaining UM's relationship to formal standards processes | MISSING |
| No explicit strategy for whether/when/how to engage with W3C, IETF, or other standards bodies | MISSING |
| No documentation about current or future relationship with the Metaverse Standards Forum as an organization | MISSING |
| No documentation about potential Linux Foundation submission pathway | MISSING |
| The positioning relative to W3C VCs, DIDComm, and Solid is in an internal doc (`full-briefing.md`), not on the public site | SCATTERED |
| No "Standards Landscape" page on the site showing where UM fits relative to existing standards | MISSING |
| The agent briefing "For Standards Bodies" statement exists but is 4 sentences -- not a credible positioning document | INCOMPLETE |
| The governance document describes UM as "standards-track" without defining which track | INCOMPLETE |

---

## 8. Gap Analysis Summary

| # | Gap Description | Category | Area |
|---|----------------|----------|------|
| 1 | Explainer documents (`docs/explainers/`) not published on `universalmanifest.net` | MISSING | Vision |
| 2 | No non-technical landing page or "Why UM?" page on the public site | MISSING | Vision |
| 3 | No published competitive positioning page on the site | MISSING | Vision |
| 4 | Commercial journeys not published on the site | MISSING | Vision |
| 5 | No standalone "How to Adopt UM" guide for third parties | MISSING | Integration |
| 6 | Adoption tier model (Tier 0-4) not published on the site | MISSING | Integration |
| 7 | No "Resolver API Reference" page on the public site | MISSING | Integration |
| 8 | No outreach strategy or adoption plan document | MISSING | Exposure |
| 9 | No launch checklist for public presentation | MISSING | Exposure |
| 10 | No "Standards Positioning" document | MISSING | Standards |
| 11 | No strategy for engagement with W3C, IETF, MSF, or other standards bodies | MISSING | Standards |
| 12 | No "Standards Landscape" comparison page on the site | MISSING | Standards |
| 13 | No documentation about current/future MSF organizational relationship | MISSING | Standards |
| 14 | Interactive sandbox defined but not yet built | INCOMPLETE | Website |
| 15 | Teaching scripts system at Stage 3 (ideas only, no produced scripts) | INCOMPLETE | Website |
| 16 | Most integration lanes in catalog are "Planned" with no content | INCOMPLETE | Integration |
| 17 | Adopter onboarding package (WO-0055) not started | INCOMPLETE | Exposure |
| 18 | Adopter feedback loop (WO-0056) not started | INCOMPLETE | Exposure |
| 19 | npm package not yet published publicly | INCOMPLETE | Exposure |
| 20 | Governance doc says "standards-track" without defining which track | INCOMPLETE | Standards |
| 21 | Agent briefing "For Standards Bodies" is 4 sentences, not a positioning document | INCOMPLETE | Standards |
| 22 | Competitive positioning (UM vs VCs, DIDComm, Solid, OIDC) exists only in internal docs | SCATTERED | Vision |
| 23 | Resolver documentation split across multiple internal and site files with no single reference | SCATTERED | Integration |
| 24 | Adoption path guidance scattered across DEPTH-AND-SCOPE, full-briefing, and site quick start | SCATTERED | Integration |
| 25 | Development methodology (done-done, journeys) not explained in a contributor-facing page | SCATTERED | Methodology |
| 26 | 16 animated SVGs live but not organized into browsable gallery or tutorial sequence | SCATTERED | Website |
| 27 | GitHub repository URL inconsistent across different files (LocalArtistNetwork vs WebOfTrustInfo) | OUTDATED | Exposure |
| 28 | Site overview page leads with format description rather than human problem statement | INCOMPLETE | Vision |
| 29 | No changelog or release notes page on the public site | MISSING | Website |
| 30 | Integration authoring guide exists in repo (`docs/guides/integration-authoring-guide.md`, 186 lines) but is not published on the site; catalog index link is broken | BROKEN LINK | Integration | [CORRECTION 2026-03-01: File exists as repo doc but not as site page.]
| 31 | No write/publish API for the resolver | MISSING | Integration |
| 32 | No documented target adopter list or ecosystem map | MISSING | Exposure |

---

## 9. Recommended Priority Actions

### P0 (Critical) -- Must exist for UM to be presentable to external audiences

1. **Publish explainer documents on the site.** The one-pager and full briefing are the project's strongest external assets. Add them to the site under a top-level "About" or "Learn" section. This is the single highest-impact action for external communication.

2. **Create a standalone Adoption Guide.** Consolidate the adoption tier model (from DEPTH-AND-SCOPE), the adoption path (from full-briefing), and the quick start into a single "How to Adopt Universal Manifest" document on the public site. Target audience: a developer or architect evaluating whether to adopt UM, who needs to understand what level of commitment is required and what they get at each tier.

3. **Create a Standards Positioning document.** Document UM's relationship to formal standards processes: what standards UM builds on (JSON-LD, DIDs, VCs, JCS, Ed25519), how UM relates to adjacent efforts (W3C VCs, DIDComm, Solid), whether/when UM might be submitted to a standards body, and what the relationship is with the MSF (given the MUM lineage) and OMA3 (given the active integration lane). This should be both a repo document and a published site page.

4. **Create a "Why UM?" page on the public site.** This should be the non-technical entry point for evaluators and decision-makers. Lead with the fragmentation problem, not the JSON-LD format. Use the "Swiss Army Knife" metaphor. Link to the full briefing for depth.

5. **Fix the GitHub repository URL inconsistency.** At least 4 different GitHub URLs exist: `github.com/LocalArtistNetwork/universalmanifest` (site config), `github.com/WebOfTrustInfo/universal-manifest` (governance, CONTRIBUTING.md), `github.com/nicholasgrigoriadis/universalmanifest` (agent briefing, full briefing), and `github.com/universalmanifest/universalmanifest` (code examples). All must be resolved to a single canonical URL before any public presentation. [CORRECTION 2026-03-01: Original report identified only 2 conflicting URLs; at least 4 exist.]

6. **Build and ship the interactive sandbox.** The CEO mandate is clear: "This is the thing that makes Universal Manifest real to the world. Everything else is paperwork until this exists." Work orders WO-0060 through WO-0068 are defined and are highest priority.

### P1 (Important) -- Should exist for completeness and credibility

7. **Publish the commercial journeys on the site.** The creator journey, venue operator journey, app developer journey, privacy journey, and enterprise journey in `docs/journeys/commercial/` are compelling narrative documents that demonstrate UM's value in concrete terms. They should be on the site under a "Use Cases" or "Stories" section.

8. **Create a Standards Landscape page on the site.** The competitive positioning from `full-briefing.md` is strong content. Publish it on the site so evaluators can see how UM fits in the ecosystem without reading an internal doc.

9. **Create a Resolver API Reference page.** Consolidate resolver documentation from `DOMAIN-ARCHITECTURE.md`, `CONTRACT.md`, and `conformance/resolver.md` into a single, authoritative API reference on the public site.

10. **Publish the adoption tier model on the site.** The Tier 0-4 model from `DEPTH-AND-SCOPE.md` is excellent adoption guidance. Publish it as part of the Adoption Guide (P0 item 2) or as a standalone page.

11. **Create a contributor-facing "How We Build This" page.** Explain the journey-driven proof model, the done-done framework, and the work-order discipline to potential contributors. This would live in the Governance section of the site.

12. **Organize animated SVGs into a browsable sequence.** The 16 production animated SVGs are scattered across content pages. Create an "Animation Gallery" or "Visual Explainer" page that presents them in a logical teaching sequence.

13. **Complete and publish the adopter onboarding package (WO-0055).** This is the external-facing complement to the internal development methodology.

14. **Add a changelog or release notes page to the site.** Essential for credibility with external adopters who need to track what has changed between versions.

### P2 (Nice to have) -- Would strengthen the project but not blocking

15. **Document an outreach strategy.** Even a lightweight document listing target audiences, channels, events, and timeline would be valuable for project coordination.

16. **Create an MSF relationship document.** Given the MUM lineage, document what the current relationship with the Metaverse Standards Forum is and whether there are plans to contribute UM back to MSF working groups.

17. **Produce teaching script animations.** The teaching scripts system has a well-designed framework (iconic representation, script format, 20 script ideas) but no produced scripts or animations. Even 2-3 completed scripts would significantly enhance the project's communication capability.

18. **Expand integration lane content.** Many lanes in the catalog are "Planned." Prioritize creating content for the most strategically important planned lanes (ActivityPub/Fediverse, Ethereum ENS, Gaming Profiles).

19. **Publish an explicit "not a standards body" statement or a "path to standardization" statement.** Either UM intends to pursue formal standardization (in which case, document the plan) or it intends to remain an independent open-source standard (in which case, document that position). The current ambiguity is a gap.

20. **Create an ecosystem map diagram.** A visual showing where UM fits relative to JSON-LD, DIDs, VCs, Solid, DIDComm, OMA3/OMATrust, MSF, and other standards would be a powerful communication tool for both the site and presentations.

---

## Appendix: Key Files Referenced

| File | Description |
|------|-------------|
| `/Users/grig/work/repo/universalmanifest/docs/explainers/one-pager.md` | Strongest external-facing explainer |
| `/Users/grig/work/repo/universalmanifest/docs/explainers/full-briefing.md` | Deepest explainer with competitive positioning |
| `/Users/grig/work/repo/universalmanifest/docs/explainers/agent-briefing.md` | AI-optimized reference with pitch templates |
| `/Users/grig/work/repo/universalmanifest/docs/UNIVERSAL-MANIFEST-BRIEFING.md` | Comprehensive 537-line briefing with examples |
| `/Users/grig/work/repo/universalmanifest/docs/DEPTH-AND-SCOPE.md` | Adoption tier model (Tier 0-4) |
| `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md` | 9-phase development roadmap |
| `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-DEFINITION.md` | Maturity gate framework (G1-G7) |
| `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-CHECKLIST.md` | Release readiness checklist |
| `/Users/grig/work/repo/universalmanifest/docs/journeys/README.md` | Journey proof system documentation |
| `/Users/grig/work/repo/universalmanifest/docs/PUBLISHING-AND-VERSIONING.md` | Publishing model and immutability policy |
| `/Users/grig/work/repo/universalmanifest/docs/DOMAIN-ARCHITECTURE.md` | Domain split rationale |
| `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md` | Current project snapshot |
| `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md` | Vision including MUM lineage |
| `/Users/grig/work/repo/universalmanifest/docs/governance/GOVERNANCE.md` | Governance charter |
| `/Users/grig/work/repo/universalmanifest/docs/site/INFORMATION-ARCHITECTURE.md` | Site IA document |
| `/Users/grig/work/repo/universalmanifest/docs/MANDATE-interactive-implementation-sandbox.md` | CEO sandbox mandate |
| `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-22-omatrust-integration-assessment.md` | OMATrust integration assessment |
| `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-23-remaining-work-to-final-vision.md` | Previous gap analysis |
| `/Users/grig/work/repo/universalmanifest/site/astro.config.mjs` | Site configuration and navigation |
| `/Users/grig/work/repo/universalmanifest/site/src/content/docs/index.md` | Site landing page |
| `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/universal-manifest-overview.md` | "What Is UM?" page |
| `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/index.md` | Integration catalog |
| `/Users/grig/work/repo/universalmanifest/integrations/oma-trust.md` | OMATrust integration lane |
| `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md` | Metaverse integration lane (with MSF lineage) |
| `/Users/grig/work/repo/universalmanifest/research/linux-foundation-projects/2026-02/SYNTHESIS.md` | LF documentation benchmark |
| `/Users/grig/work/repo/universalmanifest/docs/journeys/commercial/enterprise-journey.md` | Enterprise adopter narrative |
| `/Users/grig/work/repo/universalmanifest/docs/teaching-scripts/README.md` | Teaching scripts system overview |
| `/Users/grig/work/repo/universalmanifest/docs/security/THREAT-MODEL.md` | Security threat model |

---

**End of audit.**
