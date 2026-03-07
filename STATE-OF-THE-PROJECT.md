# State of the Project — Universal Manifest

**Date:** 2026-03-06
**Status:** 135 formal work orders defined in `docs/workorders/`. WO-0001 through WO-0052 complete. Interactive Sandbox Wave (WO-0060 through WO-0068) COMPLETED. Sandbox V2 Redesign (WO-0069 through WO-0080) COMPLETED. Audit-driven waves (WO-0081 through WO-0112) COMPLETED. External Adopter Wave (WO-0053 through WO-0059) COMPLETED (all seven work orders delivered with evidence on 2026-03-02). Deployment/Ops hardening follow-on (WO-0113 through WO-0118) COMPLETED. Runtime reality + credential durability waves (WO-0119 through WO-0124) COMPLETED. Go-Now Program Execution Wave (WO-0125 through WO-0126) COMPLETED. Privacy Signal Standards Review + Execution (WO-0127 through WO-0128) COMPLETED. Inbox Corpus Hygiene Wave (WO-0129) COMPLETED. Localized Source Follow-on Wave (WO-0130 through WO-0136) COMPLETED. Runtime Guidance and Spatial-Fabric Refresh Wave (WO-0137 through WO-0138) COMPLETED. RP1/MSF Adversarial Hardening Wave (WO-0139) COMPLETED. K2B Concept Integration Traceability (WO-0140) COMPLETED. Metaverse Portaling Integration (WO-0141) COMPLETED.
**Canonical repository path:** `<repo-root>`
**Legacy path:** archived (historical only)

This repo remains a **spec-first project with fixtures and tooling**, and it now also includes active production operations for the docs surface (`universalmanifest.net`) and resolver surface (`myum.net`) via Cloudflare Pages/Workers.

For the “what has to happen next” sequence, see: `docs/CRITICAL-PATH.md`.
For recent audit reports, see the [`docs/reports/`](reports/) directory (includes freshness audits, completeness audits, and status summaries).

## Current snapshot

### What exists now

- **v0.1 draft spec artifacts**
  - JSON-LD context: `spec/v0.1/schema.jsonld`
  - Structural schema: `spec/v0.1/schema.json`
  - Spec overview: `spec/v0.1/README.md`
  - Well-known name registry (draft): `spec/v0.1/REGISTRY.md`
  - Conformance checklist + fixtures list (draft): `spec/v0.1/CONFORMANCE.md`
- **Fixtures**
  - Baseline examples: `examples/v0.1/`
  - Near-real stubs: `examples/v0.1/stubs/`
  - Invalid fixtures (conformance): `examples/v0.1/invalid/`
  - Human index for fixtures + “vision drivers”: `docs/STUB-MANIFESTS.md`
- **Integration notes**
  - reference implementation + device caching + transport: `integrations/reference-runtime.md`
  - Social/profile adoption: `integrations/social.md`
  - Metaverse lane + lineage context: `integrations/metaverse.md`
  - RP1 spatial-fabric lane: `integrations/rp1-spatial-fabric.md`
  - Smart-glasses social layer lane: `integrations/smart-glasses.md`
  - Proof-of-personhood multi-provider lane: `integrations/proof-of-personhood.md`
  - DID + VC credential lane: `integrations/did-vc.md`
  - Global Privacy Control (GPC) lane: `integrations/gpc-global-privacy-control.md`
- **Publishing + versioning plan**
  - Stable URLs + headers + immutability policy: `docs/PUBLISHING-AND-VERSIONING.md`
  - Domain split architecture (`universalmanifest.net` + `myum.net`): `docs/DOMAIN-ARCHITECTURE.md`
- **Official completion framework**
  - Done-done definition: `docs/DONE-DONE-DEFINITION.md`
  - Release checklist: `docs/DONE-DONE-CHECKLIST.md`
  - Evidence pack template: `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`
- **Tooling**
  - TypeScript types + runtime assertion in spec repo: `packages/universal-manifest/`
  - Standalone TypeScript reference implementation repository: `https://github.com/grigb/um-typescript`
  - Fixture validation run via `npm test` (build + validate valid + invalid fixtures + GPC proof pack)
- **Proof surfaces (executable + visual)**
  - Journeys → executable proof suite: `docs/journeys/` (run via `packages/universal-manifest` → `npm run journeys`; 22 executable journeys passing)
  - Harness → visual endpoint/fixture debugger: `site/public/harness/index.html` (served at `/harness/index.html`)
  - Endpoint smoke (dev/prod) for docs + resolver contract: `packages/universal-manifest/scripts/smoke-endpoints.mjs`
- **Animated SVG explainer pipeline (established, proven)**
  - 29 production animated SVGs live on universalmanifest.net (plus 2 test files and 2 pilot iterations; 33 total) (WO-0042, WO-0043)
  - Prompt pack system: `.dev/ai/prompts/animation/`
  - Workflow documentation: `docs/design/ANIMATED-SVG-WORKFLOW.md`
  - QA checklist: `docs/design/ANIMATION-QA-CHECKLIST.md`
  - Production assets: `site/public/animations/`
  - Overview diagram: `site/public/diagrams/universal-manifest-overview-template.svg`
- **Teaching scripts system**
  - Staged explanation scripts for 30-second, 3-minute, and 15-minute audiences: `docs/teaching-scripts/`
  - Capsule-Pod iconic representation (approved): `docs/teaching-scripts/01-ICONIC-REPRESENTATION.md`
- **Interactive sandbox (COMPLETED, WO-0060 through WO-0068)**
  - CEO mandate: `docs/MANDATE-interactive-implementation-sandbox.md`
  - Proposal and scenario list: `.dev/ai/proposals/PROPOSAL-interactive-implementation-sandbox.md`
  - 25 interactive scenarios across 5 categories (Getting Started, Trust and Verification, Integration Lanes, Edge Cases, Advanced)
  - Browser-based Ed25519 validator with 54/54 Node parity
  - Three-panel layout with step engine, scenario modal with search and filters
  - 25 SVG illustrations, CI parity testing (54/54), scenario smoke testing (183/183)
- **Sandbox V2 Redesign (COMPLETED, WO-0069 through WO-0080)**
  - HierarchyExplorer, DetailsCard, EntityColumn, ProtocolLens, SubjectPanel components
  - SandboxLayoutV2 (CSS Grid), SandboxEngineV2 (two-entity state management)
  - Scenario detail page rewrite, full scenario migration (GS, TV, IL, EC, AD)
  - Responsive polish, animations, accessibility audit
  - Build and browser verification completed.
- **Public docs IA + editorial polish**
  - Explicit sidebar labels/order and adopter-first navigation in the docs site
  - “Critical Path” reframed as adopter-facing “Adoption Roadmap”
  - Integration pages now include clear implementation checklists + fixture links + boundaries
- **v0.2 draft signature profile (artifacts exist)**
  - Signature profile: `spec/v0.2/SIGNATURE-PROFILE.md`
  - Draft schema + context: `spec/v0.2/schema.json` + `spec/v0.2/schema.jsonld`
  - Draft conformance: `spec/v0.2/CONFORMANCE.md`
  - Fixtures: `examples/v0.2/`
- **Background research**
  - Imported docs under `research/` with an index at `research/README.md`

### What is *not* finalized yet (by design)

- v0.1 signature is still a permissive placeholder; v0.2 defines an interop profile but remains draft until publishing and broader adopter verification
- Additional integrity profiles (e.g., Data Integrity / RDF canonicalization) beyond the v0.2 baseline
- Revocation cursor/events as a normative part of the contract
- A complete conformance suite (we have baseline valid/invalid fixtures plus non-normative GPC proof coverage; broader TTL/replay/security cases remain)
- Advanced hardening of the interactive manifest workbench beyond first public release (`WO-0014`)
- First-time onboarding validation with human external reader testing is recommended as optional quality evidence (not a closure gate).

## Work-order status (2026-03-05)

- Completed: `WO-0001` through `WO-0013` (including `WO-0003` publishing/deploy)
- Completed: `WO-0014` interactive workbench (first usable implementation + verification evidence)
- Completed: `WO-0015` first-time overview and visual onboarding
- Completed: `WO-0016` GAS index scan and knowledge integration ledger (including deferred-corpus reconciliation)
- Completed: `WO-0017` full-corpus to IA/journey synthesis execution (implementation pass completed 2026-02-19)
- Completed: `WO-0018` MUM lineage + metaverse/RP1/smart-glasses integration codification (2026-02-20)
- Completed: `WO-0019` resolver `J03` reliability + production routing hardening (2026-02-20)
- Completed: `WO-0020` RP1 source ingestion + synthesis materialization (2026-02-20)
- Completed: `WO-0021` smart-glasses consent fixtures + proof journeys (2026-02-20)
- Completed: `WO-0022` metaverse lane fixtures + proof hardening (2026-02-20)
- Completed: `WO-0023` deployment drift prevention automation (2026-02-20)
- Completed: `WO-0024` multi-provider proof-of-personhood, social identity, DID, and Chia integration (2026-02-20)
- Completed: `WO-0025` documentation readability and links polish (2026-02-21)
- Completed: `WO-0026` workbench and harness redesign (2026-02-21)
- Completed: `WO-0027` OMATrust integration lane execution (2026-02-21)
- Completed: `WO-0028` Astro content-cache clean-build hardening (2026-02-21)
- Completed: `WO-0029` docs nav order + overview clarity pass (2026-02-22)
- Completed: `WO-0030` animated SVG explainer prompt pack + production pipeline (2026-02-22)
- Completed: `WO-0031` journey proof parity + decoupling hardening (2026-02-22)
- Completed: `WO-0032` published docs stale-status scan and fixes (2026-02-22)
- Completed: `WO-0033` published docs label-first link normalization (2026-02-22)
- Completed: `WO-0034` documentation status coherence and stale-reference reconciliation (2026-02-22)
- Completed: `WO-0035` human-reader policy and onboarding evidence alignment (mandatory gate removed, 2026-02-23)
- Completed: `WO-0036` v0.2 publication and verification edge-case expansion (2026-02-22)
- Completed: `WO-0037` integrity profile, revocation, and adversarial conformance hardening (2026-02-22)
- Completed: `WO-0038` corpus drift governance and follow-on WO cycle (2026-02-22)
- Completed: `WO-0039` onboarding plain-language rewrite and source-propagation hardening
- Completed: `WO-0040` v0.2 signature verification investigation — confirmed working (2026-02-23)
- Completed: `WO-0041` status document drift reconciliation (2026-02-23)
- Completed: `WO-0042` animation upgrade phase 1 -- 7 SVGs (replaced pilots, upgraded overview, 4 new scenarios) (2026-02-27)
- Completed: `WO-0043` animation upgrade phase 2 -- 9 SVGs (2 tool explainers, 7 integration lane explainers) (2026-02-27)
- Completed: `WO-0044` public open-source examples and demos work stream (2026-02-27)
- Completed: `WO-0045` commercial explainer ecosystem and integration expansion (2026-02-27)
- Completed: `WO-0046` infographic styles inventory viewer (2026-02-26)
- Completed: `WO-0047` security documentation and threat model (`docs/security/THREAT-MODEL.md`) (2026-02-27)
- Completed: `WO-0048` conformance suite expansion: 6 new fixtures (3 valid, 3 invalid) (2026-02-27)
- Completed: `WO-0049` CI/CD hardening: 5-job GitHub Actions pipeline (`.github/workflows/ci.yml`) (2026-02-27)
- Completed: `WO-0050` API reference, JSDoc, Lan→Um rename, package.json update (2026-02-27)
- Completed: `WO-0051` governance framework, RFC template, GitHub issue templates (`docs/governance/`) (2026-02-27)
- Completed: `WO-0052` JSON audit: docs already clean, no changes needed (2026-02-27)

### New work order waves

#### Interactive Sandbox Wave (WO-0060 through WO-0068) — COMPLETED

Per CEO mandate ([`docs/MANDATE-interactive-implementation-sandbox.md`](MANDATE-interactive-implementation-sandbox.md)), this wave superseded the External Adopter Wave in execution order. All 9 work orders completed and verified (2026-02-28).

- Completed: `WO-0060` sandbox foundation and browser validator (2026-02-28)
- Completed: `WO-0061` three-panel layout and step engine (2026-02-28)
- Completed: `WO-0062` scenario modal and navigation (2026-02-28)
- Completed: `WO-0063` Getting Started scenarios GS-01 through GS-04 (2026-02-28)
- Completed: `WO-0064` Trust and Verification scenarios TV-01 through TV-05 (2026-02-28)
- Completed: `WO-0065` Integration Lane scenarios IL-01 through IL-08 (2026-02-28)
- Completed: `WO-0066` Edge Case and Advanced scenarios (2026-02-28)
- Completed: `WO-0067` visual polish and SVG illustrations (2026-02-28)
- Completed: `WO-0068` CI parity testing and QA (2026-02-28)

#### Sandbox V2 Redesign (WO-0069 through WO-0080) — COMPLETED

All 12 work orders completed (2026-03-01). Build and browser verification completed.

- Completed: `WO-0069` HierarchyExplorer (reusable collapsible JSON tree-view) (2026-03-01)
- Completed: `WO-0070` DetailsCard (dual-mode hierarchy/JSON toggle) (2026-03-01)
- Completed: `WO-0071` SessionStateIndicator + V2 types (2026-03-01)
- Completed: `WO-0072` EntityColumn (symmetrical entity panel) (2026-03-01)
- Completed: `WO-0073` ProtocolLens (step-by-step interaction viewer) (2026-03-01)
- Completed: `WO-0074` SubjectPanel (exchanged object display) (2026-03-01)
- Completed: `WO-0075` SandboxLayoutV2 (new CSS Grid layout) (2026-03-01)
- Completed: `WO-0076` SandboxEngineV2 (two-entity state management) (2026-03-01)
- Completed: `WO-0077` Scenario detail page rewrite (2026-03-01)
- Completed: `WO-0078` Getting Started scenario migration GS-01 through GS-04 (2026-03-01)
- Completed: `WO-0079` Remaining scenario migration: TV, IL, EC, AD (2026-03-01)
- Completed: `WO-0080` Responsive polish, animations, accessibility audit (2026-03-01)

#### External Adopter Wave (WO-0053 through WO-0059) — COMPLETED

- Completed: `WO-0053` standalone conformance test suite (2026-03-02)
- Completed: `WO-0054` reference implementation repository (2026-03-02)
- Completed: `WO-0055` adopter onboarding document package (2026-03-02)
- Completed: `WO-0056` adopter feedback loop and contract system (2026-03-02)
- Completed: `WO-0057` spec vs. implementation documentation clarity (2026-03-02)
- Completed: `WO-0058` v0.1-to-v0.2 migration guide (2026-03-02)
- Completed: `WO-0059` governance completion: breaking-change, deprecation, incident policies + simulation evidence (2026-03-02)

#### Audit-Driven Content and Documentation Waves (WO-0081 through WO-0111) — COMPLETED

- Completed: `WO-0081` through `WO-0090` (spec-vs-implementation boundary fixes)
- Completed: `WO-0091` through `WO-0102` (external-facing content and site publishing)
- Completed: `WO-0103` through `WO-0111` (documentation freshness, change records, and animated SVG gallery organization)

#### myum Resolver Consumer Frontend + Runtime Reality (WO-0112) — COMPLETED

- `WO-0112` implementation, deployment alignment, and production verification are complete (`/sandbox/`, `/resolver/`, and `/reference/resolver-api/` are live and production smoke passes)

#### Deployment and Operations Hardening (WO-0113 through WO-0118) — COMPLETED

- Completed: `WO-0113` staging environments and promotion model (custom staging domains active with fallback resilience and staging KV split)
- Completed: `WO-0114` gated staged-to-production deployment workflow
- Completed: `WO-0115` toolchain/runtime baseline pinning
- Completed: `WO-0116` resolver contract coverage expansion in CI
- Completed: `WO-0117` synthetic monitoring + SLO policy
- Completed: `WO-0118` automated staging target selection (explicit override -> custom-domain auto -> fallback auto) across deploy gates and synthetic monitoring

#### Runtime Reality and Credential Durability Follow-on (WO-0119 through WO-0124) — COMPLETED

- Completed: `WO-0119` resolver route canonicalization and fixture freshness lock
- Completed: `WO-0120` harness 307 contract parity and trust matrix
- Completed: `WO-0121` synthetic alert delivery and escalation drill
- Completed: `WO-0122` runtime status messaging reconciliation
- Completed: `WO-0123` Cloudflare credential stabilization for gated production promotions
- Completed: `WO-0124` CI Cloudflare secret rotation to long-lived API tokens with enforcement and remediation closeout

#### Go-Now Program Execution Wave (WO-0125 through WO-0126) — COMPLETED

- Completed: `WO-0125` Portable Identity Profile Go-Now execution and integration pages (`PIP-GN-01` through `PIP-GN-06`)
- Completed: `WO-0126` Metaverse Universal Manifest Go-Now execution and integration pages (`MUM-GN-01` through `MUM-GN-06`)

#### Privacy Signal Standards Review and Execution (WO-0127 through WO-0128) — COMPLETED

- Completed: `WO-0127` GPC standards integration review and gap analysis
- Completed: `WO-0128` GPC Go-Now runtime mapping, fixtures, and proof

#### Inbox Corpus Hygiene Wave (WO-0129) — COMPLETED

- Completed: `WO-0129` Universal Manifest inbox dedupe, import, and archive

#### Localized Source Follow-on Wave (WO-0130 through WO-0136) — COMPLETED

- Completed: `WO-0130` Composite architecture and active runtime alignment
- Completed: `WO-0131` DID + VC and metaverse lane refresh from localized corpus
- Completed: `WO-0132` Research-First protocol volatility, proximity, and federation gaps
- Completed: `WO-0133` Protocol recommendation governance and standards currency matrix
- Completed: `WO-0134` Proximity credential and presentation profile assessment
- Completed: `WO-0136` OMB Wiki spatial-fabric source refresh and primary-source crosscheck
- Completed: `WO-0135` Federation and bridge strategy decision package

#### Runtime Guidance and Spatial-Fabric Refresh Wave (WO-0137 through WO-0138) — COMPLETED

- Completed: `WO-0137` Role-based runtime, federation, and bridge guidance refresh
- Completed: `WO-0138` RP1/MSF primary-source refresh and integration-depth pass

#### RP1/MSF Adversarial Hardening Wave (WO-0139) — COMPLETED

- Completed: `WO-0139` RP1/MSF adversarial attachment and session hardening

#### K2B Concept Integration Traceability (WO-0140) — COMPLETED

- Completed: `WO-0140` K2B concept integration transfer map and traceability closeout
- Delivered one consolidated report explaining what the deep research gaps were filled with, where each major concept landed downstream, and where K2B already exists in the repo as the knowledge-to-build transition system.
- Key artifact:
  - `docs/reports/2026-03-06-k2b-concept-integration-transfer-map.md`

#### Metaverse Portaling Integration (WO-0141) — COMPLETED

- Completed: `WO-0141` metaverse portaling integration and guidance refresh
- Made portaling explicit as the metaverse-lane user experience: jumping between different platforms with UM carrying portable content pointers and policy state.
- Synchronized the metaverse lane, journey language, sandbox scenario language, MSF lineage framing, and internal explainer surface around that concept.
- Key artifact:
  - `docs/reports/2026-03-06-metaverse-portaling-integration-note.md`

## Priority context (2026-03-06)

The Interactive Sandbox Wave (WO-0060 through WO-0068), Sandbox V2 Redesign (WO-0069 through WO-0080), audit-driven waves (WO-0081 through WO-0112), External Adopter Wave (WO-0053 through WO-0059), runtime durability follow-on (WO-0119 through WO-0124), Go-Now execution wave (WO-0125 through WO-0126), GPC execution wave (WO-0127 through WO-0128), inbox corpus hygiene wave (WO-0129), WO-0130 through WO-0136, the Runtime Guidance and Spatial-Fabric Refresh Wave (WO-0137 through WO-0138), the RP1/MSF Adversarial Hardening Wave (WO-0139), the K2B Concept Integration Traceability pass (WO-0140), and the Metaverse Portaling Integration pass (WO-0141) are completed. There are no queued follow-on work orders in `docs/workorders/WO-INDEX.md`.

No work order may be executed outside the explicitly approved sequence without user confirmation.

## Critical-path execution update (2026-02-20)

Completed in this run:
- fixed local resolver E2E instability (`J03`) by seeding preview KV in journey setup and waiting for status transitions before assertions.
- deployed latest Pages artifact for `universalmanifest.net`; workbench routes are live.
- bound resolver worker to both apex and `www` host variants for `myum.net`.
- re-ran production smoke and strict K2B validator with explicit artifact root.

Evidence:
- `packages/universal-manifest/scripts/run-journeys.mjs`
- `docs/journeys/_artifacts/2026-02-20T05-25-51-070Z-journey-report.json`
- `services/myum-resolver/wrangler.toml`
- `docs/workorders/WO-0019-resolver-j03-reliability-and-routing-hardening.md`
- `.dev/ai/reports/2026-02-20-k2b-integration-completeness-report.md`

Production route verification:
- `https://universalmanifest.net/getting-started/workbench/` -> `200`
- `https://universalmanifest.net/getting-started/workbench/` -> `308` redirect to `/workbench/` (live target)
- `https://universalmanifest.net/workbench/` -> `200`
- `https://www.myum.net/health` -> `200`

## Lineage and integration codification update (2026-02-20)

Completed this run:
- codified MUM origin lineage in source-of-truth vision and decision records
- added explicit integration lanes for metaverse, RP1 spatial fabric, and smart-glasses social-layer controls
- added corresponding docs-site integration pages and updated first-time overview context

Evidence:
- `docs/PROJECT-VISION.md`
- `docs/DECISIONS.md`
- `integrations/metaverse.md`
- `integrations/rp1-spatial-fabric.md`
- `integrations/smart-glasses.md`
- `site/src/content/docs/integrations/metaverse.md`
- `site/src/content/docs/integrations/rp1-spatial-fabric.md`
- `site/src/content/docs/integrations/smart-glasses.md`
- `site/src/content/docs/getting-started/universal-manifest-overview.md`

## WO-0017 execution pass update (2026-02-19)

Concrete deltas completed this run:
- IA delta artifact created:
  - `.dev/ai/specs/2026-02-19-ia-delta-from-full-corpus.md`
- Journey planning materialization updated:
  - `docs/journeys/README.md`
  - `docs/workorders/WO-0012-user-journeys-and-e2e-test-suite.md`
- Workbench requirement hardening updated:
  - `docs/workorders/WO-0014-interactive-manifest-workbench.md`
- WO progress/evidence updates:
  - `docs/workorders/WO-0017-corpus-to-ia-and-journey-synthesis.md`
  - `docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md`

Gap movement from latest provenance audit:
- `GAP-K2B-001`: closed.
- `GAP-K2B-002`: closed for planning-materialization scope.
- `GAP-K2B-003`: closed (workbench requirements materialized and implemented).
- `GAP-K2B-004`: unchanged.
- `GAP-K2B-005`: unchanged.

## Local verification status (2026-02-28)

- `site` build (`npm run build:clean`): PASS (0 warnings, exit code 0)
- `packages/universal-manifest` tests (`npm test`): PASS (46/46 fixtures, exit code 0)
- Journeys proof (`npm run journeys`): PASS (11/11, exit code 0)
- Endpoint smoke prod (`npm run smoke:endpoints:prod`): PASS (9/9 endpoints)
- Endpoint smoke dev (`npm run smoke:endpoints:dev`): N/A (dev servers not running; expected, not a failure)
- v0.2 signature verification: WORKING
- Nomenclature cleanup: 31 files updated (50 changes), "signature envelope" → "signature" throughout

Note: 46 committed fixtures (31 v0.1 + 15 v0.2) after WO-0048 conformance suite expansion. 1 additional uncommitted stub (`cross-system-projection-manifest.jsonld`) exists on disk, totaling 47.

## What we consider “done” for v0.1

v0.1 is “done enough” when:

1. A third-party system can parse manifests and safely ignore unknown fields.
2. Fixtures cover the baseline subject types (venue, device, creator) + one cross-system profile projection.
3. The spec clearly documents TTL + caching + ID guidance and why it exists.

The project satisfies (1) and (2) with runnable evidence and now has production deployment proof. Remaining work is primarily interoperability hardening plus first-time adopter experience/tooling.

For formal gate-level completion criteria and evidence requirements, use:

- `docs/DONE-DONE-DEFINITION.md`
- `docs/DONE-DONE-CHECKLIST.md`

## Next milestones (recommended)

### Milestone A — Conformance scaffolding (still v0.1.x)

- ✅ Added `spec/v0.1/CONFORMANCE.md` checklist (“what a consumer MUST do to claim v0.1 support”)
- ✅ Added initial invalid fixtures (missing required fields, wrong `@type`, bad shards)
- ✅ Updated `packages/universal-manifest` validator to assert invalid fixtures fail
- Next: add deeper TTL and misuse/adversarial fixtures for v0.1.x and v0.2.x as the suite hardens

### Milestone B — Signature profile (v0.2)

- ✅ Chose a v0.2 baseline profile (JCS + Ed25519) and added draft artifacts + fixtures:
  - `spec/v0.2/SIGNATURE-PROFILE.md`
  - `spec/v0.2/schema.json` + `spec/v0.2/schema.jsonld`
  - `spec/v0.2/CONFORMANCE.md`
  - `examples/v0.2/`
- Next: publish v0.2 artifacts at stable URLs and expand fixtures for verification edge-cases

### Milestone C — Distribution + stability (v0.2+)

- Documented publishing + versioning plan: `docs/PUBLISHING-AND-VERSIONING.md`
- Production deployment is live:
  - `https://universalmanifest.net` (Cloudflare Pages)
  - `https://myum.net` (Cloudflare Worker + KV)
- Next: harden v0.2 migration policy and resolver edge-case semantics
  - Cloudflare Pages runbook: `deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`
  - Resolver contract: `services/myum-resolver/CONTRACT.md`

### Milestone D — Adopter onboarding + interactive tooling

- ✅ First-time overview content and visual onboarding are shipped
- ✅ Interactive manifest workbench is shipped and verified (`WO-0014` completed)
- ✅ CLI-agent reader test evidence logged
- Optional quality step: run and log a human participant reader-test for additional onboarding confidence.
  - Protocol: `docs/reports/2026-02-19-first-time-reader-testing-protocol.md`
  - Results: `docs/reports/2026-02-20-first-time-reader-test-results.md`

### Milestone E — Full-corpus IA and journey execution

- Deferred-source reconciliation is complete for the current batch (`WO-0016` completed)
- Conflict decisions are recorded with action targets:
  - `.dev/ai/ingestion/records/2026-02-18-cross-source-conflicts.md`
- ✅ Corpus-derived IA/journey/workbench deltas were executed and closed in:
  - `docs/workorders/WO-0017-corpus-to-ia-and-journey-synthesis.md`
- Next: run drift checks for newly ingested sources and open follow-on WOs when corpus deltas affect adopter-facing IA or proof flows

### Milestone F — Metaverse lineage and emerging integration lanes

- ✅ MUM origin and strategic lineage are codified in source-of-truth docs.
- ✅ Metaverse integration lane is documented.
- ✅ Metaverse fixture + journey execution evidence is completed (`WO-0022`).
- ✅ RP1 spatial-fabric integration lane is documented.
- ✅ Smart-glasses social-layer integration lane is documented.
- ✅ Smart-glasses consent fixture + journey execution evidence is completed (`WO-0021`).
- ✅ RP1 intake, fixture/journey materialization, and conflict reconciliation are completed (`WO-0020`).
- ✅ Multi-provider proof-of-personhood (World ID, Gitcoin Passport, BrightID), social DID method coverage, and DID + VC credential lane completed (`WO-0024` closed 2026-02-20).
- Next: maintain conformance/security hardening milestones and consider deeper adversarial fixture coverage.

## How other systems should adopt it today (v0.1)

Recommended adoption tier for external systems *right now*:

- Validate required fields (`@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`)
- Enforce TTL for caching decisions
- Use `pointers` and known `shards` for projection
- Treat `signature` as optional and/or “best effort” until the signature profile is finalized
- For v0.2 drafts: verify signatures when present and required by that profile

## Notes on origin-runtime relationship

the reference implementation is a primary design driver, but the project goal is broader:

- a reference implementation uses the manifest as a local-first capsule (edge ↔ display ↔ admin).
- Future “social profile” surfaces should treat the manifest as an envelope that drives projections (web profile pages, ActivityPub actor pointers, etc.).

This is why “reference implementation specifics” live in `integrations/` and `research/`, not in `spec/`.

## Historical priority note

Priority sections in older handoffs/audits are historical snapshots and must be revalidated against the current repository state before execution.

## Agent onboarding status

Universal Manifest has been aligned to the GAS split model for onboarding consistency:

- `AGENTS.md` contains the global immutable rules copy.
- `PROJECT-RULES.md` contains Universal Manifest-specific instructions and operational context.
- `.dev` now includes GAS-style directory scaffolding for handoffs, workorders, reports, and inbox capture.
