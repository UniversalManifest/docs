# Universal Manifest — Critical Path

This document captures the minimal execution sequence to make Universal Manifest broadly adoptable and eventually “world-ready”.

“World-ready” is not a vibe. It requires passing the gates in `docs/DONE-DONE-DEFINITION.md` with evidence.

## Phase 0 — Define “done” (gates + evidence) -- COMPLETE

- Read: `docs/DONE-DONE-DEFINITION.md`
- Use: `docs/DONE-DONE-CHECKLIST.md`
- Capture: `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`

Status: Done-done framework established and in active use across all phases.

## Phase 1 — Make v0.1 adoptable (minimal contract) -- COMPLETE

Goal: third parties can adopt UM without choosing your identity provider, storage, or framework.

Must-have:

- clear v0.1 contract (required fields + TTL semantics)
- unknown-field tolerance (forward compatibility)
- fixtures: valid + invalid + near-real stubs
- conformance checklist + basic validator tooling

Status: v0.1 contract is adoptable. 32 v0.1 fixtures (valid, invalid, stubs) committed. Conformance checklist and validator tooling shipped.

## Phase 2 — Harden interoperability (v0.2 signature profile) -- COMPLETE

Goal: two independent implementations can sign/verify the same payload the same way.

Must-have:

- signature profile (canonicalization + signing + verification rules)
- signed fixtures and invalid-signature fixtures
- a reference verifier (small, testable, not a framework)

Status: v0.2 signature profile (JCS + Ed25519) is drafted with 15 fixtures. Ed25519 signature verification confirmed working (WO-0040). Conformance suite expanded with adversarial cases (WO-0048).

## Phase 3 — Publish like a real standard (`universalmanifest.net`) -- COMPLETE

Goal: newcomers can understand and adopt the spec quickly, and the URLs are stable.

Must-have:

- spec/docs site with clear navigation and a first-time reader path
- stable URLs for schema/context artifacts
- versioning + immutability policy

Status: `universalmanifest.net` is live on Cloudflare Pages with stable URLs, adopter-first sidebar navigation, and first-time reader overview.

## Phase 4 — Make UMIDs resolvable (`myum.net/{UMID}`) -- COMPLETE

Goal: a consumer can resolve a manifest by UMID with a deterministic contract (headers, caching, errors, privacy posture).

Must-have:

- resolver endpoint contract + examples
- minimum privacy posture (what is public vs not, and why)
- tests that exercise resolution end-to-end

Status: `myum.net` resolver is live on Cloudflare Workers + KV. J03 reliability hardened (WO-0019). Production smoke passes 9/9 endpoints.

## Phase 5 — Prove it across surfaces (reference implementation + cross-runtime) -- COMPLETE

Goal: demonstrate the spec is not “just for reference implementation” while still letting reference implementation be a primary design driver.

Must-have:

- reference implementation integration recipe
- at least one cross-runtime adopter journey (e.g., profile projection)
- journeys act as proof, not marketing

Status: 21 executable journeys passing. Multiple integration lanes documented with fixture-backed proof, including GPC runtime-signal handling as a non-normative proof lane.

## Phase 6 — Full-corpus synthesis before IA and journey expansion -- COMPLETE

Goal: ensure IA, onboarding, and journey planning are derived from the full source corpus with explicit conflict decisions.

Must-have:

- no deferred sources in active corpus batch (all selected sources dispositioned)
- explicit cross-source conflict register with decisions and action targets
- synthesis output that maps source signals into IA/journey/workbench directives
- follow-on implementation WO for corpus-to-artifact execution

Status: Corpus-derived IA/journey/workbench deltas executed and closed (WO-0016, WO-0017).

## Phase 7 — Onboarding clarity + interactive adopter tooling -- COMPLETE

Goal: first-time adopters can understand UM quickly and validate real manifests without writing custom tooling first.

Must-have:

- clear “What is Universal Manifest?” overview for first-contact readers
- visual onboarding diagrams maintained with source assets
- interactive manifest workbench (import, create, validate, export)
- explicit boundaries between reference tooling and normative spec contract

Status: First-time overview shipped. Interactive manifest workbench shipped and verified (WO-0014). Teaching scripts and explainer ecosystem established.

## Phase 8 — Lineage-grounded expansion lanes -- COMPLETE

Goal: scale beyond baseline adoption while preserving origin context and integration boundaries.

Must-have:

- explicit lineage reference to the MUM origin document in source-of-truth docs
- metaverse integration lane documentation
- RP1 spatial-fabric integration lane documentation with source-ingestion plan
- smart-glasses social-layer integration lane documentation with consent-first behavior
- clear rule that normative contract changes still require versioned spec/conformance updates

Status: All integration lanes documented with fixtures and proof journeys (WO-0018 through WO-0024, WO-0027). 13 integration lanes total including OMATrust, proof-of-personhood, DID + VC, education, healthcare, and smart home.

## Phase 9 — Drift governance and closure-regression checks -- ACTIVE

Goal: keep completion claims true over time by running recurring drift and regression checks with explicit WO trigger thresholds.

Cadence and owner:

- weekly drift/governance run by active maintainer or delegated agent
- required before new completion claims or milestone closure statements

Mandatory command set:

1. strict K2B gate validation:
   - `bash ~/.agents/scripts/validate-k2b-gates.sh <repo-root> --artifact-root .dev/ai --strict`
2. journey parity check:
   - `cd packages/universal-manifest && npm run journeys`
3. production route checks:
   - `curl -I https://universalmanifest.net/`
   - `curl -I https://universalmanifest.net/getting-started/workbench/`
   - `curl -I https://universalmanifest.net/proof/harness/`
4. docs link-hygiene scan:
   - `rg -n '/harness/|/proof/|/getting-started/|/spec/|/conformance/|/workbench/|/integrations/' site/src/content/docs --glob '*.md' | rg -v '\\]\\([^)]+'`

Follow-on WO trigger thresholds:

- open a new WO immediately if any mandatory command fails
- open a new WO if status docs contradict active WO status or production reality
- open a new WO if newly ingested corpus signals require IA/spec/proof deltas beyond trivial wording edits

## Phase 10 — Interactive Sandbox (WO-0060-0068) -- COMPLETED, HIGHEST PRIORITY

Per CEO mandate ([`docs/MANDATE-interactive-implementation-sandbox.md`](MANDATE-interactive-implementation-sandbox.md)), this phase superseded all other execution priorities.

Goal: provide a hands-on interactive sandbox where adopters can explore real manifests, see validation in action, and understand the spec through guided scenarios.

Delivered:

- sandbox foundation with browser-based Ed25519 validator (54/54 parity with Node)
- three-panel layout (entity | consumer | protocol) with step engine
- scenario modal with card grid, search, filters, and keyboard navigation
- 25 interactive scenarios across 5 categories:
  - Getting Started (GS-01 through GS-04): first-time user onboarding
  - Trust and Verification (TV-01 through TV-05): real Ed25519, tamper detection
  - Integration Lanes (IL-01 through IL-08): social, smart glasses, metaverse, spatial, and more
  - Edge Cases (EC-01 through EC-04): failure mode demonstrations
  - Advanced (AD-01 through AD-04): cross-system projection, revocation, full v0.2
- 25 SVG illustrations (self-contained, accessible, dark theme)
- CI parity testing (54/54) and scenario smoke testing (183/183)

Status: All 9 work orders (WO-0060 through WO-0068) completed and verified.

## Phase 11 — Sandbox V2 Redesign (WO-0069-0080) -- COMPLETED

Goal: redesign the sandbox UI with a two-entity interaction model, hierarchy explorer, protocol lens, and enhanced visual design.

Delivered:

- HierarchyExplorer: reusable collapsible JSON tree-view (WO-0069)
- DetailsCard: dual-mode hierarchy/JSON toggle (WO-0070)
- SessionStateIndicator + V2 types (WO-0071)
- EntityColumn: symmetrical entity panel (WO-0072)
- ProtocolLens: step-by-step interaction viewer (WO-0073)
- SubjectPanel: exchanged object display (WO-0074)
- SandboxLayoutV2: new CSS Grid layout (WO-0075)
- SandboxEngineV2: two-entity state management (WO-0076)
- Scenario detail page rewrite (WO-0077)
- Getting Started scenario migration (WO-0078)
- Remaining scenario migration: TV, IL, EC, AD (WO-0079)
- Responsive polish, animations, accessibility audit (WO-0080)

Status: All 12 work orders completed. Build and browser verification completed, and the redesign is live on production routes.

## Phase 12 — External Adopter Verification Wave (WO-0053-0059) -- COMPLETED

Goal: enable third-party adoption by providing standalone conformance tools, reference implementations, onboarding materials, and clear spec-vs-implementation boundaries. Blocks Gates G4 and G6.

Must-have:

- standalone conformance test suite (WO-0053, CRITICAL, blocks Gate G4)
- reference implementation repository (WO-0054, CRITICAL, blocks Gate G4)
- adopter onboarding document package (WO-0055, CRITICAL, blocks Gate G4)
- adopter feedback loop and contract system (WO-0056, HIGH, blocks Gate G4 + G6)
- spec-vs-implementation documentation clarity (WO-0057, HIGH, blocks Gate G4)
- v0.1-to-v0.2 migration guide (WO-0058, HIGH, blocks Gate G6)
- governance completion: breaking-change, deprecation, incident policies (WO-0059, CRITICAL, blocks Gate G6 + World-ready)

Status: Completed. WO-0053 through WO-0059 were delivered and verified with evidence on 2026-03-02, including standalone conformance tooling, reference implementation publication, adopter onboarding package, migration guide, and governance completion.

## Phase 13 — Teaching Scripts and Visual Identity System -- IN_PROGRESS

Goal: create a comprehensive teaching and communication ecosystem with staged explanation scripts and a consistent visual identity.

Delivered so far:

- teaching scripts system with staged explanations for 30-second, 3-minute, and 15-minute audiences ([`docs/teaching-scripts/`](teaching-scripts/))
- Capsule-Pod iconic representation approved as the UM visual identity ([`docs/teaching-scripts/01-ICONIC-REPRESENTATION.md`](teaching-scripts/01-ICONIC-REPRESENTATION.md))
- 20 script ideas defined ([`docs/teaching-scripts/03-SCRIPT-IDEAS.md`](teaching-scripts/03-SCRIPT-IDEAS.md))
- 5 explainer documents at various depth levels ([`docs/explainers/`](explainers/))
- 4 animation scripts ([`docs/scripts/`](scripts/))
- 29 production animated SVGs plus 2 pilot files on universalmanifest.net

Status: Stage 3 (script ideas and visual identity established). Ongoing refinement.

## Phase 14 — Code Examples Ecosystem -- COMPLETE

Goal: provide runnable code examples and a demo application so adopters can learn by doing.

Delivered:

- 12 runnable code examples covering hello-world, validation, signing, shards, resolution, projection, device registration, consent enforcement, unknown-field tolerance, and multi-manifest aggregation ([`examples/code/`](../examples/code/))
- browser-based and Python validation examples ([`examples/code/browser-validate/`](../examples/code/browser-validate/), [`examples/code/python-validate/`](../examples/code/python-validate/))
- full demo application with server and library ([`examples/demo-app/`](../examples/demo-app/))

Status: Completed (WO-0044).

## Phase 15 — Portable Identity Profile + Metaverse Go-Now Program Execution -- COMPLETE

Goal: close both immediate execution tracks with adopter-ready guidance, synchronized evidence, and publication-ready docs/site updates without changing UM normative contract boundaries.

Delivered:

- Portable Identity Profile Go-Now completion (`PIP-GN-01` through `PIP-GN-06`):
  - integration lane + site mirror,
  - fixture and journey evidence packs,
  - registry key-family expansion,
  - implementation-path guide and site publication,
  - governance synchronization updates.
- Metaverse Universal Manifest Go-Now completion (`MUM-GN-01` through `MUM-GN-06`):
  - integration hardening and scenario coverage,
  - registry + fixtures + journey suite evidence,
  - synchronization-profile guide and site publication,
  - governance synchronization updates.

Primary evidence:

- `docs/workorders/WO-0125-portable-identity-profile-go-now-execution-and-integration-pages.md`
- `docs/workorders/WO-0126-metaverse-universal-manifest-go-now-execution-and-integration-pages.md`
- `docs/reports/2026-03-05-portable-identity-profile-comprehensive-human-review-report.md`
- `docs/reports/2026-03-05-metaverse-universal-manifest-comprehensive-human-review-report.md`
- `docs/reports/2026-03-05-gn06-conformance-npm-test.txt`
- `docs/reports/2026-03-05-gn06-journeys-run.txt`
- `docs/reports/2026-03-05-gn06-site-build-clean.txt`

Status: Completed (WO-0125, WO-0126). Next path is Research-First execution (`PIP-RS-*`, `MUM-RS-*`) under existing promotion gates.

## Phase 16 — Privacy Signal Standards Alignment (GPC) -- COMPLETE

Goal: execute the GPC integration direction from standards review into reference proof without expanding the core UM contract prematurely.

Delivered:

- standards review and overlap/gap analysis closure (`WO-0127`)
- published GPC integration lane docs for repo + site
- runtime normalization helpers for `Sec-GPC` and `navigator.globalPrivacyControl`
- `/.well-known/gpc.json` support-resource parsing helpers
- optional UM evidence projection helpers for consent/pointer representation
- dedicated GPC fixture pack under `examples/integrations/gpc/`
- GPC evidence-projection manifest fixture
- `J21` executable journey proof for runtime-authoritative behavior and scope-limited supersession

Primary evidence:

- `docs/workorders/WO-0127-gpc-standards-integration-review-and-gap-analysis.md`
- `docs/workorders/WO-0128-gpc-go-now-runtime-mapping-fixtures-and-proof.md`
- `integrations/gpc-global-privacy-control.md`
- `packages/universal-manifest/src/index.ts`
- `docs/reports/2026-03-06-gpc-go-now-npm-test.txt`
- `docs/reports/2026-03-06-gpc-go-now-journeys.txt`
- `docs/journeys/_artifacts/2026-03-06T07-50-34-715Z-journey-report.json`

Status: Completed (WO-0127, WO-0128). Next path is broader privacy-signal research/promotion work only if explicitly approved.
