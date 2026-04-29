# State of the Project — Universal Manifest

**Date:** 2026-04-29
**Status:** Formal work now extends through `WO-0242`. The Home-cluster wave (`WO-0195` through `WO-0205`) is complete, `WO-0206` through `WO-0209` closed the first late-April drift-governance follow-up, `WO-0219` plus follow-ons `WO-0241` and `WO-0242` completed the integration-lane reference/route/journey consolidation, and v0.2 publication prep (`WO-0220`) is complete but still operator-gated. After revert commit `e493b3e` removed the unauthorized CI/workflow layer on 2026-04-28, Phase 9 is back to a manual-only posture, several infrastructure WOs are audit-only `OBSOLETE`, and the publication wave (`WO-0221` through `WO-0231`, excluding obsolete items) remains pending.
**Canonical repository path:** `<repo-root>`
**Legacy path:** archived (historical only)

This repo remains a **spec-first project with fixtures and tooling**, but it is no longer only a spec/docs repo. It now operates a multi-surface public program: a consumer-first public homepage plus standards/docs site on `universalmanifest.net`, executable proof and interactive tooling surfaces, and the resolver/runtime contract surface on `myum.net` via Cloudflare Pages/Workers.

The most important change in this refresh is that the public front door has now been rebalanced. `/` is once again a consumer-facing homepage, the latest W3C-style draft specification now lives at `/spec/latest/`, and the specification shell has site-level navigation instead of behaving like an isolated homepage.

The current public MVP is in place, publication continuity has been verified, and the first internal `UM UI` component layer now exists. The first reader reintegration wave is complete, and the first tool/proof reintegration wave is also complete: `/docs/`, `/about/why-um/`, `/about/one-pager/`, `/use-cases/`, `/learning/`, `/sandbox/`, and `/workbench/` now sit under the shared public/tool-shell family without widening the calm public MVP menu. `WO-0184` has now extended that route/shell alignment to `/404.html`, `/proof/harness/`, `/resolver/`, `/resolver/ops/`, `/resolver/result/`, and `/tools/concept-explorer/` while preserving subordinate raw payloads such as `/resolver/app/` and `/tools/concept-explorer/app/`. `WO-0185` has now given `/spec/latest/` a durable route model: Astro owns the outer shell and calm nav, while the checked-in W3C-style document remains the source of truth for the spec body and standards-reader behavior. `WO-0187` has now normalized the canonical diagram naming path to `/diagrams/universal-manifest-system-overview.svg` while preserving `/diagrams/universal-manifest-overview-template.svg` as a compatibility alias. `WO-0188` has now defined explicit retirement-readiness criteria for compatibility-only routes, deploy layers, and asset aliases, including the sequencing that keeps `deploy/localartist.network/` as the highest-risk and latest retirement candidate. `WO-0190` then deferred additional integrity-profile guidance beyond the current v0.2 JCS + Ed25519 baseline, `WO-0191` kept revocation/status signaling as an optional extension lane, `WO-0192` expanded bounded TTL/security invalid-fixture coverage and propagated those fixtures into the published mirrors, and `WO-0193` hardened workbench draft safety with autosave, discard guards, extracted core logic, and tests. `WO-0189` then defined the explicit v0.2 publication-readiness criteria and blocker list, and `WO-0194` packaged the available first-time-reader validation method and evidence without turning it into a release gate. `WO-0195` then defined the next homepage architecture as a content-first `Home` cluster with local sub-navigation, a domain-of-thought audit, a depth model, and a metaverse-first interactive explorer strategy. `WO-0196` through `WO-0205` then delivered the page architecture, audience landings, explorer content model, lead content packs, route implementation, and publication-readiness pass for that cluster. `WO-0206` then restored the K2B artifact contract and `WO-0207` through `WO-0209` extended that closeout across metadata, internal audit traceability, and the now-reverted first automation pass. `WO-0219`, `WO-0241`, and `WO-0242` have now consolidated integration-lane implementation notes, public route coverage, and dedicated journey coverage through `J27`. The current late-April reality is narrower than the old automation plan: the Home cluster and integration-lane consolidation are complete, v0.2 is still unpublished, publication prep is ready but blocked on the operator-run `WO-0220` tag/release step, and the 2026-04-28 revert moved Phase 9 back to manual governance while marking several workflow-era WOs as historical `OBSOLETE`.

For the “what has to happen next” sequence, see: `docs/CRITICAL-PATH.md`.
For the deepest single-file structural map, see: `docs/COMPREHENSIVE-PROJECT-PROPERTIES-AND-SURFACES-MAP.md`.
For the post-map structural strategy and keep/merge/alias/retire decisions, see: `docs/reports/2026-04-13-post-wo-0179-surface-disposition-and-unification-strategy.md`.
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
- **Public landing/docs/discovery surfaces**
  - Consumer-first root homepage: `site/src/pages/index.astro`
  - `Home`-cluster local-tab family: `site/src/pages/index.astro`, `site/src/pages/use-cases/index.astro`, `site/src/pages/explorer/index.astro`, `site/src/pages/how-it-works/index.astro`, `site/src/pages/standards-fit/index.astro`
  - Audience landing-page family: `site/src/pages/audiences/[audience].astro`
  - Shared content model for the public home-cluster rollout: `site/src/data/home-cluster.ts`
  - Curated docs entry: `site/src/pages/docs/index.astro`
  - Stable latest-draft spec route: `site/src/pages/spec/latest.astro`
  - Reintegrated reader routes under the shared shell: `site/src/pages/about/why-um.astro`, `site/src/pages/about/one-pager.astro`, `site/src/pages/use-cases/index.astro`
  - Long-form docs overview now published at `/docs/overview/`: `site/src/content/docs/index.md`
  - Public agent path: `site/src/content/docs/for-agents.md` and `site/src/content/docs/external-agent-onboarding.md`
  - Machine-readable discovery files: `site/public/llms.txt`, `site/public/.well-known/universal-manifest.json`, `site/public/.well-known/security.txt`
  - Public catalogs for agent/browser consumption: `site/public/agent/fixture-catalog.json`, `site/public/agent/sandbox-scenarios.json`
  - Resolver/runtime contract docs and descriptors: `site/src/content/docs/reference/resolver-api.md`, `services/myum-resolver/CONTRACT.md`
  - Shared-shell static tool entry routes: `site/src/pages/404.astro`, `site/src/pages/proof/harness/index.astro`, `site/src/pages/resolver/index.astro`, `site/src/pages/resolver/ops/index.astro`, `site/src/pages/resolver/result/index.astro`, `site/src/pages/tools/concept-explorer/index.astro`
  - Subordinate raw payload entrypoints preserved behind the aligned routes: `site/public/resolver/app/index.html`, `site/public/tools/concept-explorer/app/index.html`
  - Verified warning-free site build baseline documented in `docs/reports/2026-03-19-docs-root-relocation-warning-free-build-baseline.md`
  - Homepage/spec rebalance implementation report: `docs/reports/2026-04-12-consumer-homepage-and-spec-subpage-rebalance.md`
- **Official completion framework**
  - Done-done definition: `docs/DONE-DONE-DEFINITION.md`
  - Release checklist: `docs/DONE-DONE-CHECKLIST.md`
  - Evidence pack template: `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`
- **Tooling**
  - TypeScript types + runtime assertion in spec repo: `packages/universal-manifest/`
  - Standalone TypeScript reference implementation repository: `https://github.com/grigb/um-typescript`
  - Fixture validation run via `npm test` (build + validate valid + invalid fixtures + GPC proof pack)
- **Proof surfaces (executable + visual)**
  - Shared tool/proof hub: `site/src/pages/learning/index.astro`
  - Sandbox chooser under shared shell: `site/src/pages/sandbox/index.astro`
  - Workbench under shared shell with subordinate raw payload: `site/src/pages/workbench/index.astro`, `site/public/workbench/app/index.html`
  - Journeys → executable proof suite: `docs/journeys/` (run via `packages/universal-manifest` → `npm run journeys`; 27 executable journeys passing)
  - Harness → visual endpoint/fixture debugger under the shared shell: `site/src/pages/proof/harness/index.astro`
  - Published raw harness payload remains available at `site/public/harness/index.html`
  - Endpoint smoke (dev/prod) for docs + resolver contract: `packages/universal-manifest/scripts/smoke-endpoints.mjs`
- **Animated SVG explainer pipeline (established, proven)**
  - 29 production animated SVGs live on universalmanifest.net (plus 2 test files and 2 pilot iterations; 33 total) (WO-0042, WO-0043)
  - Prompt-pack workflow and surviving implementation notes: `docs/design/ANIMATED-SVG-WORKFLOW.md`
  - Workflow documentation: `docs/design/ANIMATED-SVG-WORKFLOW.md`
  - QA checklist: `docs/design/ANIMATION-QA-CHECKLIST.md`
  - Production assets: `site/public/animations/`
  - Overview diagram: `site/public/diagrams/universal-manifest-system-overview.svg` (compatibility alias retained at `site/public/diagrams/universal-manifest-overview-template.svg`)
- **Teaching scripts system**
  - Staged explanation scripts for 30-second, 3-minute, and 15-minute audiences: `docs/teaching-scripts/`
  - Capsule-Pod iconic representation (approved): `docs/teaching-scripts/01-ICONIC-REPRESENTATION.md`
- **Interactive sandbox (COMPLETED, WO-0060 through WO-0068)**
  - CEO mandate: `docs/MANDATE-interactive-implementation-sandbox.md`
  - Surviving scenario catalog: `site/public/agent/sandbox-scenarios.json`
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
  - Landing/docs/discovery/runtime boundaries are now reconciled across the site and authority docs
- **v0.2 draft signature profile (artifacts exist)**
  - Signature profile: `spec/v0.2/SIGNATURE-PROFILE.md`
  - Draft schema + context: `spec/v0.2/schema.json` + `spec/v0.2/schema.jsonld`
  - Draft conformance: `spec/v0.2/CONFORMANCE.md`
  - Fixtures: `examples/v0.2/`
- **Background research**
  - Imported docs under `research/` with an index at `research/README.md`

### What is *not* finalized yet (by design)

- v0.1 signature is still a permissive placeholder; v0.2 defines an interop profile but remains draft until publishing and broader adopter verification
- v0.2 publication prep is complete, but `WO-0220` still requires operator-run tag/release commands before the downstream publication wave can start
- The late-April publication wave remains unfinished: `WO-0221` through `WO-0226`, `WO-0229`, `WO-0230`, and `WO-0231` are still pending; `WO-0214` remains deferred until after publication
- Phase 9 is currently manual-only after the 2026-04-28 revert removed workflow automation; any future automation must be re-scoped rather than assumed live
- Additional integrity profiles (e.g., Data Integrity / RDF canonicalization) beyond the v0.2 baseline
- Revocation cursor/events as a normative part of the contract
- A complete conformance suite (we have baseline valid/invalid fixtures plus non-normative GPC proof coverage; broader TTL/replay/security cases remain)
- Advanced hardening of the interactive manifest workbench beyond first public release (`WO-0014`)
- First-time onboarding validation with human external reader testing is recommended as optional quality evidence (not a closure gate).

## Late-April queue reality (2026-04-28)

- Home-cluster execution remains complete: `WO-0195` through `WO-0205` are still the closed architecture/content/publication-readiness wave for the public front door.
- First late-April follow-up is complete: `WO-0206` through `WO-0209` restored the K2B artifact contract, synchronized metadata, and reconciled closeout traceability.
- Phase 9 is currently manual-only. `WO-0208` briefly introduced workflow automation, but revert commit `e493b3e` removed that layer on 2026-04-28 along with the related workflow-era infrastructure.
- Publication prep is ready but not executed. `WO-0220` finished the hash verification, changelog, and release-command prep, but the actual `git tag`, `git push`, and `gh release create` actions remain operator-gated.
- The active publication queue is still ahead of the repo: `WO-0221` through `WO-0226`, `WO-0229`, `WO-0230`, and `WO-0231` remain `NOT_STARTED`; `WO-0214` remains deferred until after publication.
- Integration-lane follow-up is complete: `WO-0219` standardized implementation notes and the catalog baseline, `WO-0241` added the missing public routes for `runtime-profile` and `data-firewall-ux`, and `WO-0242` added dedicated executable journey coverage for `data-firewall-ux`, `smart-home`, `healthcare-patient-consent`, and `education-credentials`.
- Obsolete WOs are retained for audit only and must not be executed: `WO-0210`, `WO-0211`, `WO-0227`, `WO-0228`, `WO-0233`, `WO-0238`, and `WO-0240`.
- Revert-sensitive deployment-pipeline work needs careful reading: `WO-0232`, `WO-0234`, and `WO-0237` were completed on 2026-04-26, but their workflow changes were later removed by the 2026-04-28 revert, so those WO records describe historical work rather than the live workflow state.

## Work-order status (2026-04-22)

#### MVP-first site publication and staged reintegration wave (WO-0172 through WO-0177) — COMPLETED

- Completed: `WO-0172` two-page MVP site, minimal navigation, and publication preparation
- Completed: `WO-0173` homepage noise reduction and one-click spec prominence
- Completed: `WO-0174` MVP publication safeguards and spec continuity verification
- Completed: `WO-0175` internal `UM UI` component-library extraction
- Completed: `WO-0176` staged reading-surface reintegration under the shared public shell
- Completed: `WO-0177` staged tool/proof-surface reintegration under the shared shell

#### Public spec surface bugfixes (WO-0178) — COMPLETED

- Completed: `WO-0178` spec-latest inline TOC layout and GAS visual verification

#### Remaining site architecture execution wave (WO-0183 through WO-0188) — COMPLETED

- Completed: `WO-0183` canonical route and compatibility alias policy
- Completed: `WO-0184` static tool surface shell alignment
- Completed: `WO-0185` latest spec surface strategy and shell implementation
- Completed: `WO-0186` fixture mirror source-of-truth consolidation
- Completed: `WO-0187` animation and diagram asset naming normalization
- Completed: `WO-0188` compatibility surface retirement readiness

#### Remaining standards and proof hardening wave (WO-0189 through WO-0194) — COMPLETED

- Completed: `WO-0189` v0.2 publication readiness and adopter verification
- Completed: `WO-0190` additional integrity profile decision package
- Completed: `WO-0191` revocation cursor and status contract
- Completed: `WO-0192` conformance suite TTL, replay, and security expansion
- Completed: `WO-0193` interactive manifest workbench hardening wave
- Completed: `WO-0194` first-time reader validation evidence pack

#### Home-cluster IA and explorer strategy (WO-0195) — COMPLETED

- Completed: `WO-0195` home-cluster sitemap, domain audit, and explorer strategy

#### Home-cluster content and audience rollout wave (WO-0196 through WO-0205) — COMPLETED

- Completed: `WO-0196` home-cluster page content architecture and source map
- Completed: `WO-0197` audience landing family architecture and route strategy
- Completed: `WO-0198` explorer lane schema, content template, and hero-asset brief system
- Completed: `WO-0199` metaverse portaling and digital-worlds content pack
- Completed: `WO-0200` EU self-sovereign identity and digital-identity content pack
- Completed: `WO-0201` remaining audience and use-case content packs
- Completed: `WO-0202` home-cluster route shell and local tab navigation implementation
- Completed: `WO-0203` explorer component and first-lane integration
- Completed: `WO-0204` audience landing-page implementation wave
- Completed: `WO-0205` home-cluster migration, harmonization, and publication readiness

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

#### Consumer Resolver UX Hardening (WO-0144) — COMPLETED

- Completed: `WO-0144` myum consumer provenance and example-state hardening (2026-03-10)
- Eliminated live-vs-fallback ambiguity in the consumer resolver UX and added/verified live production example states for contract-visible redirect/revoked behavior.
- Key artifact:
  - `docs/workorders/WO-0144-myum-consumer-provenance-and-example-state-hardening.md`

#### Concept Hierarchy Explorer and Ecosystem Namespace (WO-0155) — COMPLETED

- Completed: `WO-0155` concept hierarchy explorer and ecosystem namespace (2026-04-01)
- Result:
  - the project now has a single interactive explorer for showing the breadth of Universal Manifest application domains
  - the ecosystem namespace framing is documented as part of the forward-looking compliance/discovery model
- Key artifacts:
  - `docs/workorders/WO-0155-concept-hierarchy-explorer-and-ecosystem-namespace.md`
  - `site/public/tools/concept-explorer/index.html`
  - `site/public/tools/concept-explorer/concepts.json`

#### Agent-Friendly Multi-Surface Program (WO-0157 through WO-0160) — COMPLETED

- Completed: `WO-0157` landing surface and multi-layer interaction architecture (2026-03-15)
- Completed: `WO-0158` agent discovery and machine-readable entrypoints (2026-03-15)
- Completed: `WO-0159` external-agent onboarding and wild adoption documentation (2026-03-15)
- Completed: `WO-0160` agent-facing content completeness and verification gates (2026-03-15)
- Result:
  - `universalmanifest.net` now exposes a first-class discovery layer for humans and agents
  - `myum.net` now exposes runtime/security/openapi descriptors as part of the public resolver contract

#### Landing-First Public Experience and Cleanup Wave (WO-0161 through WO-0164) — COMPLETED

- Completed: `WO-0161` landing-page and docs-secondary-route implementation (2026-03-15)
- Completed: `WO-0162` agent-path drift reconciliation and Starlight warning cleanup (2026-03-17)
- Completed: `WO-0163` remaining site build warning triage and noise reduction (2026-03-17)
- Completed: `WO-0164` docs-root relocation and warning-free build baseline (2026-03-19)
- Result:
  - `/` is now the public landing surface
  - `/docs/` is the curated docs entry
  - `/docs/overview/` holds the long-form overview that previously occupied docs-root
  - the site build baseline is now warning-free

#### Documentation and Spec Hardening Wave (WO-0165 through WO-0170) — COMPLETED

- Completed: `WO-0165` through `WO-0170` including W3C-style specification adoption, synthetic review protocols, TOC visual fixes, and identity cross-DID research.
- Result:
  - `universalmanifest.net` now serves the hardened W3C-style specification HTML as the root.
  - Critical architectural vulnerabilities tracked under `WO-0170` have complete research theses.
  - Deployment processes execute without Starlight warnings.

#### 2026-04-24 checkpoint (historical)

- This checkpoint predated the later `WO-0207` through `WO-0240` wave and should be read as history, not current queue state.
- `WO-0206` restored the K2B artifact contract and passed the Phase 9 mandatory command set at that time.
- `WO-0195` through `WO-0205` remain completed for the home-cluster execution sequence.
- `WO-0206` is completed.
- `WO-0171` remains the closure artifact for the homepage/spec-route rebalance.
- The previously cited frontier items `WO-0142`, `WO-0143`, `WO-0145`, and `WO-0155` remain `COMPLETED`.
- The identity-binding / Bag-of-Claims follow-on remains integrated into committed decision, threat-model, spec-delta, and schema artifacts rather than re-opened as a standalone proposal thread.

#### 2026-04-24 micro-closeouts (subtask-level, not formal WOs)

The following subtask-level refinements landed on 2026-04-24 alongside `WO-0206` and the surface-drift scan. They are captured here for canonical traceability only; none of them were promoted to formal work orders, and this section should be read as the 2026-04-24 checkpoint rather than the current late-April queue state.

- Orchestrator WO-scope and Phase 9 evidence closeout — `.dev/ai/subtask-comms/2026-04-24-orchestrator-wo-scope-and-phase9-closeout.md`
- Private facets, encryption, and attested identifier/control binding surfacing across Home-cluster IA, copy briefs, and audience briefs — `.dev/ai/subtask-comms/2026-04-24-private-facets-attested-ownership-surfacing.md`
- Private facets and attested-ownership source-grounding review (reference-only, no IA/copy edits) — `.dev/ai/subtask-comms/2026-04-24-private-facets-attested-ownership-source-review.md`
- IWPS portaling source-grounding correction across Home-cluster sitemap, copy briefs, and audience briefs — `.dev/ai/subtask-comms/2026-04-24-iwps-portaling-source-grounding-correction.md`
- Home-cluster copy briefs and source-fidelity closeout (copy briefs, audience briefs, and markdown/source fidelity process) — `.dev/ai/subtask-comms/2026-04-24-home-cluster-copy-briefs-and-source-fidelity-closeout.md`

These closeouts did not change spec, fixture, or runtime behavior; they refined the Home-cluster brief layer and the markdown/source fidelity governance process. Readers arriving here should treat each bullet's path as the authoritative source of what was done and why.

## Priority context (2026-04-12)

The project is no longer blocked on the public front door. The homepage now leads with audience comprehension and routing, while the latest W3C-style spec has a dedicated subordinate route.

That returned the execution posture to drift governance and explicit re-entry for future work at the time:

- later follow-on WOs (`WO-0207` through `WO-0240`) superseded this checkpoint
- any additional execution should follow the current queue summary above rather than implied continuation from older waves

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
- Historical K2B completeness note was referenced in earlier status snapshots, but that `.dev` artifact is not present in the current checkout.

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
- Historical IA delta artifact was referenced in earlier status snapshots, but that `.dev` spec artifact is not present in the current checkout.
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

## Local verification status (rolling)

- `site` build (`cd site && npm run build`): PASS with no warnings (2026-03-19, `WO-0164`)
- Served-route checks after the final public-surface cleanup pass: PASS for `/`, `/docs/`, and `/docs/overview/` (2026-03-19)
- Served-route checks during the agent-path reconciliation and warning-reduction passes: PASS for `/for-agents/`, `/for-agents/external-agent-onboarding/`, `/about/agent-briefing/`, `/publishing/domain-split/`, `/workbench/`, `/workbench/index/`, and `/sandbox/gs-01-first-manifest-v2/` (2026-03-17)
- `packages/universal-manifest` tests (`npm test`): PASS (46/46 fixtures, 2026-02-28)
- Journeys proof (`npm run journeys`): PASS (11/11, 2026-02-28)
- Endpoint smoke prod (`npm run smoke:endpoints:prod`): PASS (9/9 endpoints, 2026-02-28)
- Endpoint smoke dev (`npm run smoke:endpoints:dev`): N/A when dev servers are not running; not treated as a failure
- v0.2 signature verification: WORKING

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

### Milestone A — Drift governance after the front-door correction

- After `WO-0171`, re-run the recurring verification gates in `docs/CRITICAL-PATH.md`.
- Treat earlier completed WOs as closed history; new sequencing should flow from approved re-entry work, not stale milestone text.

## How other systems should adopt it today (v0.1)

Recommended adoption tier for external systems *right now*:

- Validate required fields (`@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`)
- Enforce TTL for caching decisions
- Use `pointers` and known `facets` for projection
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
