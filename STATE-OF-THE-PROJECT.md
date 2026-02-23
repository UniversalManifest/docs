# State of the Project — Universal Manifest

**Date:** 2026-02-23  
**Status:** Core implementation wave (`WO-0001` through `WO-0034`) is delivered in-repo (`universalmanifest.net` + `myum.net`). Follow-on hardening/governance work (`WO-0036` through `WO-0038`) and the v0.2 signature verification investigation (`WO-0040`) are complete. Final closure-grade posture remains gated by two open items: mandatory human onboarding evidence (`WO-0035`, BLOCKED on human-participant reader test) and onboarding plain-language rewrite (`WO-0039`, NOT_STARTED). `WO-0015` is also BLOCKED pending resolution of both `WO-0035` and `WO-0039`.
**Canonical repository path:** `/Users/grig/work/repo/universalmanifest`
**Legacy path:** archived (historical only)

This repo is a **spec + fixtures + minimal tooling** project. It is not a running service.

For the “what has to happen next” sequence, see: `docs/CRITICAL-PATH.md`.
For the latest condensed status summary, see: `docs/reports/2026-02-18-live-status-and-next-critical-path.md`.

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
  - reference implementation + Shield caching + transport: `integrations/reference-runtime.md`
  - Social/profile adoption: `integrations/social.md`
  - Metaverse lane + lineage context: `integrations/metaverse.md`
  - RP1 spatial-fabric lane: `integrations/rp1-spatial-fabric.md`
  - Smart-glasses AR social layer lane: `integrations/smart-glasses-ar.md`
  - Proof-of-personhood multi-provider lane: `integrations/proof-of-personhood.md`
  - Chia DID/VC credential lane: `integrations/chia-vc.md`
- **Publishing + versioning plan**
  - Stable URLs + headers + immutability policy: `docs/PUBLISHING-AND-VERSIONING.md`
  - Domain split architecture (`universalmanifest.net` + `myum.net`): `docs/DOMAIN-ARCHITECTURE.md`
- **Official completion framework**
  - Done-done definition: `docs/DONE-DONE-DEFINITION.md`
  - Release checklist: `docs/DONE-DONE-CHECKLIST.md`
  - Evidence pack template: `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`
- **Tooling**
  - TypeScript types + runtime assertion for v0.1: `packages/universal-manifest/`
  - Fixture validation run via `npm test` (build + validate valid + invalid fixtures)
- **Proof surfaces (executable + visual)**
  - Journeys → executable proof suite: `docs/journeys/` (run via `packages/universal-manifest` → `npm run journeys`)
  - Harness → visual endpoint/fixture debugger: `site/public/harness/index.html` (served at `/harness/index.html`)
  - Endpoint smoke (dev/prod) for docs + resolver contract: `packages/universal-manifest/scripts/smoke-endpoints.mjs`
- **Visual onboarding assets (new)**
  - Excalidraw source-of-truth scaffold: `docs/diagrams/`
  - Published diagram assets path: `site/public/diagrams/`
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

- v0.1 signature is still a permissive envelope; v0.2 defines an interop profile but remains draft until publishing and broader adopter verification
- Additional integrity profiles (e.g., Data Integrity / RDF canonicalization) beyond the v0.2 baseline
- Revocation cursor/events as a normative part of the contract
- A complete conformance suite (we have baseline valid/invalid fixtures; TTL/replay/security cases remain)
- Advanced hardening of the interactive manifest workbench beyond first public release (`WO-0014`)
- First-time onboarding validation with human external reader testing is required for closure-grade onboarding claims (CLI-agent pass exists but is not sufficient under current policy gate; `WO-0035` BLOCKED, `WO-0039` NOT_STARTED)

## Work-order status (2026-02-23)

- Completed: `WO-0001` through `WO-0013` (including `WO-0003` publishing/deploy)
- Completed: `WO-0014` interactive workbench (first usable implementation + verification evidence)
- BLOCKED: `WO-0015` first-time overview and visual onboarding — policy-gated pending human participant evidence (`WO-0035`) and onboarding rewrite (`WO-0039`)
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
- BLOCKED: `WO-0035` human-reader policy and onboarding evidence alignment — awaiting dated human-participant result artifact (Policy A, 2026-02-22)
- Completed: `WO-0036` v0.2 publication and verification edge-case expansion (2026-02-22)
- Completed: `WO-0037` integrity profile, revocation, and adversarial conformance hardening (2026-02-22)
- Completed: `WO-0038` corpus drift governance and follow-on WO cycle (2026-02-22)
- NOT_STARTED: `WO-0039` onboarding plain-language rewrite and source-propagation hardening
- Completed: `WO-0040` v0.2 signature verification investigation — confirmed working (2026-02-23)
- Completed: `WO-0041` status document drift reconciliation (2026-02-23)

## Critical-path execution update (2026-02-20)

Completed in this run:
- fixed local resolver E2E instability (`J03`) by seeding preview KV in journey setup and waiting for status transitions before assertions.
- deployed latest Pages artifact for `universalmanifest.net`; workbench routes are live.
- bound resolver worker to both apex and `www` host variants for `myum.net`.
- re-ran production smoke and strict K2B validator with explicit artifact root.

Evidence:
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs`
- `/Users/grig/work/repo/universalmanifest/docs/journeys/_artifacts/2026-02-20T05-25-51-070Z-journey-report.json`
- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/wrangler.toml`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0019-resolver-j03-reliability-and-routing-hardening.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/2026-02-20-k2b-integration-completeness-report.md`

Production route verification:
- `https://universalmanifest.net/getting-started/workbench/` -> `200`
- `https://universalmanifest.net/getting-started/workbench/` -> `308` redirect to `/workbench/` (live target)
- `https://universalmanifest.net/workbench/` -> `200`
- `https://www.myum.net/health` -> `200`

## Lineage and integration codification update (2026-02-20)

Completed this run:
- codified MUM origin lineage in source-of-truth vision and decision records
- added explicit integration lanes for metaverse, RP1 spatial fabric, and smart-glasses AR social-layer controls
- added corresponding docs-site integration pages and updated first-time overview context

Evidence:
- `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md`
- `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
- `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`
- `/Users/grig/work/repo/universalmanifest/integrations/rp1-spatial-fabric.md`
- `/Users/grig/work/repo/universalmanifest/integrations/smart-glasses-ar.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/metaverse.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/rp1-spatial-fabric.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/smart-glasses-ar.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/universal-manifest-overview.md`

## WO-0017 execution pass update (2026-02-19)

Concrete deltas completed this run:
- IA delta artifact created:
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/specs/2026-02-19-ia-delta-from-full-corpus.md`
- Journey planning materialization updated:
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/README.md`
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0012-user-journeys-and-e2e-test-suite.md`
- Workbench requirement hardening updated:
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0014-interactive-manifest-workbench.md`
- WO progress/evidence updates:
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0017-corpus-to-ia-and-journey-synthesis.md`
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md`

Gap movement from latest provenance audit:
- `GAP-K2B-001`: closed.
- `GAP-K2B-002`: closed for planning-materialization scope.
- `GAP-K2B-003`: closed (workbench requirements materialized and implemented).
- `GAP-K2B-004`: unchanged.
- `GAP-K2B-005`: unchanged.

## Local verification status (2026-02-23)

- `site` build (`npm run build:clean`): PASS (0 warnings, exit code 0)
- `packages/universal-manifest` tests (`npm test`): PASS (40/40 fixtures, exit code 0)
- Journeys proof (`npm run journeys`): PASS (11/11, exit code 0)
- Endpoint smoke prod (`npm run smoke:endpoints:prod`): PASS (9/9 endpoints)
- Endpoint smoke dev (`npm run smoke:endpoints:dev`): N/A (dev servers not running; expected, not a failure)
- v0.2 signature verification: WORKING

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
- Required gate: run and log at least one human participant reader-test before closure-grade onboarding completion claims (`WO-0035`, Policy A)
  - Protocol: `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-19-first-time-reader-testing-protocol.md`
  - Results: `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-20-first-time-reader-test-results.md`

### Milestone E — Full-corpus IA and journey execution

- Deferred-source reconciliation is complete for the current batch (`WO-0016` completed)
- Conflict decisions are recorded with action targets:
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/ingestion/records/2026-02-18-cross-source-conflicts.md`
- ✅ Corpus-derived IA/journey/workbench deltas were executed and closed in:
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0017-corpus-to-ia-and-journey-synthesis.md`
- Next: run drift checks for newly ingested sources and open follow-on WOs when corpus deltas affect adopter-facing IA or proof flows

### Milestone F — Metaverse lineage and emerging integration lanes

- ✅ MUM origin and strategic lineage are codified in source-of-truth docs.
- ✅ Metaverse integration lane is documented.
- ✅ Metaverse fixture + journey execution evidence is completed (`WO-0022`).
- ✅ RP1 spatial-fabric integration lane is documented.
- ✅ Smart-glasses AR social-layer integration lane is documented.
- ✅ Smart-glasses consent fixture + journey execution evidence is completed (`WO-0021`).
- ✅ RP1 intake, fixture/journey materialization, and conflict reconciliation are completed (`WO-0020`).
- ✅ Multi-provider proof-of-personhood (World ID, Gitcoin Passport, BrightID), social DID method coverage, and Chia DID/VC credential lane completed (`WO-0024` closed 2026-02-20).
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
