# Work Orders — Universal Manifest

This folder tracks scoped, actionable work for the Universal Manifest spec repo.

Drift governance and follow-on WO trigger criteria:
- `docs/CRITICAL-PATH.md` (Phase 9)

## Index

- `docs/workorders/WO-0001-commit-and-push.md` — Commit + push current repo changes
- `docs/workorders/WO-0002-signature-profiles-v0-2.md` — Decide v0.2 signature profile + future Data Integrity path
- `docs/workorders/WO-0003-publishing-and-release.md` — Publish context/schema to stable URLs + release process
- `docs/workorders/WO-0004-conformance-expansion.md` — Expand conformance fixtures (TTL + unknown fields) + harness
- `docs/workorders/WO-0005-ts-helper-package.md` — Decide TS helper package distribution + usage guidance
- `docs/workorders/WO-0006-domain-and-hosting-architecture.md` — Adopt `universalmanifest.net` + `myum.net` architecture
- `docs/workorders/WO-0007-myum-resolver-and-um-static-publish.md` — Build `myum.net` resolver skeleton + `universalmanifest.net` static publish config
- `docs/workorders/WO-0008-spec-status-scope-and-foundations-audit.md` — Define scope/done-done/progress and audit against foundational references
- `docs/workorders/WO-0009-professional-docs-site-universalmanifest-net.md` — Build Linux Foundation-grade docs/publishing experience for `universalmanifest.net`
- `docs/workorders/WO-0010-build-out-reference-implementation-support.md` — Build implementation-grade reference implementation integration support
- `docs/workorders/WO-0011-linux-foundation-project-docs-benchmark.md` — Benchmark LF project docs (10 projects) to inform `universalmanifest.net`
- `docs/workorders/WO-0012-user-journeys-and-e2e-test-suite.md` — Define UM user journeys and ship an executable E2E proof suite
- `docs/workorders/WO-0013-harness-endpoint-test-surface.md` — Interactive /harness page for endpoint + fixture debugging (complements journeys)
- `docs/workorders/WO-0014-interactive-manifest-workbench.md` — Build interactive import/edit/validate/export workbench for manifests on `universalmanifest.net`
- `docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md` — [COMPLETED] Add first-time \"what is UM\" overview and visual onboarding flow
- `docs/workorders/WO-0016-gas-index-scan-and-knowledge-integration-ledger.md` — Maintain a living source-to-artifact knowledge integration ledger from GAS indexes and external corpus
- `docs/workorders/WO-0017-corpus-to-ia-and-journey-synthesis.md` — Convert full selected corpus into concrete IA, onboarding, and journey execution deltas
- `docs/workorders/WO-0018-mum-lineage-and-emerging-integration-codification.md` — Codify MUM lineage and metaverse/RP1/smart-glasses integration guidance in source-of-truth docs
- `docs/workorders/WO-0019-resolver-j03-reliability-and-routing-hardening.md` — Clear J03 reliability blocker, deploy latest workbench pages, and bind `www.myum.net` resolver routing
- `docs/workorders/WO-0020-rp1-source-ingestion-and-synthesis-materialization.md` — Ingest RP1 sources into K2B pipeline and materialize fixture/journey outputs
- `docs/workorders/WO-0021-smart-glasses-consent-fixtures-and-proof-journeys.md` — Implement smart-glasses consent fixtures and proof journeys
- `docs/workorders/WO-0022-metaverse-lane-fixtures-and-proof-hardening.md` — Implement metaverse-lane fixtures and proof hardening
- `docs/workorders/WO-0023-production-deployment-drift-prevention-automation.md` — Add deploy drift prevention and post-deploy verification automation
- `docs/workorders/WO-0024-multi-provider-proof-of-personhood-social-did-chia-integration.md` — Integrate 3 proof-of-personhood providers with Mastodon/Bluesky-linked manifests, multi-DID support, and Chia lane proof
- `docs/workorders/WO-0025-documentation-human-readability-and-links.md` — [COMPLETED] Improve documentation readability, fix raw paths, and move tool links to header icons
- `docs/workorders/WO-0026-workbench-and-harness-redesign.md` — [COMPLETED] Redesign Workbench and Harness as visual, single-screen web apps
- `docs/workorders/WO-0027-omatrust-integration-lane-execution.md` — [COMPLETED] Execute OMATrust integration lane with concrete docs, fixtures, and journey proof (`J11`)
- `docs/workorders/WO-0028-astro-content-cache-clean-build-hardening.md` — [COMPLETED] Eliminate Astro duplicate-id warning drift via clean-build hardening
- `docs/workorders/WO-0029-docs-nav-order-and-overview-clarity-pass.md` — [COMPLETED] Reorder/retitle Integrations, create sidebar Tools section, and improve Overview first-read clarity
- `docs/workorders/WO-0030-animated-svg-explainer-prompt-pack-and-production-pipeline.md` — [COMPLETED] Build deeply grounded animated SVG prompt pack and production pipeline for UM adoption explainers
- `docs/workorders/WO-0031-journey-proof-parity-and-decoupling-hardening.md` — [COMPLETED] Restore one-to-one journey proof traceability and remove hardcoded reference implementation path coupling in journey runner
- `docs/workorders/WO-0032-published-docs-stale-status-scan-and-fix.md` — [COMPLETED] Remove stale in-progress language from published docs and deploy corrected site content
- `docs/workorders/WO-0033-published-docs-label-first-link-normalization.md` — [COMPLETED] Convert publish-facing file/route path references to label-first clickable links across docs
- `docs/workorders/WO-0034-documentation-status-coherence-and-stale-reference-reconciliation.md` — [COMPLETED] Reconcile status-document drift and stale evidence references after WO closure wave
- `docs/workorders/WO-0035-human-reader-testing-policy-and-onboarding-evidence-alignment.md` — [COMPLETED] Onboarding policy aligned; mandatory human-evidence gate removed
- `docs/workorders/WO-0036-v0-2-publication-and-verification-edge-case-expansion.md` — [COMPLETED] Publish/verify v0.2 publication targets and expand verification edge-case fixture coverage
- `docs/workorders/WO-0037-integrity-profile-revocation-and-adversarial-conformance-hardening.md` — [COMPLETED] Define integrity/revocation hardening direction and add adversarial conformance coverage
- `docs/workorders/WO-0038-corpus-drift-governance-and-follow-on-workorder-cycle.md` — [COMPLETED] Operationalize recurring corpus drift checks and follow-on WO trigger criteria
- `docs/workorders/WO-0039-onboarding-plain-language-rewrite-and-source-propagation-hardening.md` — [COMPLETED] Rewrite onboarding language for first-read clarity and harden docs/backend wording source propagation paths
- `docs/workorders/WO-0040-v0-2-signature-verification-fix.md` — [COMPLETED] Investigate and confirm v0.2 signature verification is working (confirmed operational 2026-02-23)
- `docs/workorders/WO-0041-status-document-drift-reconciliation.md` — [COMPLETED] Reconcile stale and inflated status claims across project status documents
- `docs/workorders/WO-0042-animation-upgrade-phase-1-core-replacements-and-missing-scenarios.md` — [COMPLETED] Execute phase 1 animation upgrade: 7 SVGs (replaced pilots, upgraded overview, 4 new scenarios)
- `docs/workorders/WO-0043-animation-upgrade-phase-2-tools-and-integration-lane-explainers.md` — [COMPLETED] Execute phase 2 animation upgrade: 9 SVGs (2 tool explainers, 7 integration-lane explainers)
- `docs/workorders/WO-0044-public-open-source-examples-work-stream.md` — [COMPLETED] Public open-source examples and demos work stream
- `docs/workorders/WO-0045-commercial-explainer-ecosystem-and-integration-expansion.md` — [COMPLETED] Commercial explainer ecosystem and integration expansion
- `docs/design/INFOGRAPHIC-STYLES-INVENTORY.md` — [COMPLETED] Infographic styles inventory and viewer
- WO-0047 (no formal WO file; from audit report) — [COMPLETED] Security documentation and threat model (`docs/security/THREAT-MODEL.md`)
- WO-0048 (no formal WO file; from audit report) — [COMPLETED] Conformance suite expansion: 6 new fixtures (3 valid, 3 invalid)
- WO-0049 (no formal WO file; from audit report) — [COMPLETED] CI/CD hardening: 5-job GitHub Actions pipeline (`.github/workflows/ci.yml`)
- WO-0050 (no formal WO file; from audit report) — [COMPLETED] API reference, JSDoc, Lan→Um rename, package.json update
- WO-0051 (no formal WO file; from audit report) — [COMPLETED] Governance framework, RFC template, GitHub issue templates (`docs/governance/`)
- WO-0052 (no formal WO file; from audit report) — [COMPLETED] JSON audit: docs already clean, no changes needed

### External Adopter Verification Wave (WO-0053 through WO-0059)

- `docs/workorders/WO-0053-standalone-conformance-test-suite.md` — [COMPLETED] Extract conformance tests into standalone public suite with CLI runner, expected-results manifest, and badge mechanism (CRITICAL, blocks Gate G4)
- `docs/workorders/WO-0054-reference-implementation-repository-typescript.md` — [COMPLETED] Create separate public TypeScript reference implementation repo demonstrating full UM adoption (CRITICAL, blocks Gate G4; depends on WO-0053)
- `docs/workorders/WO-0055-adopter-onboarding-document-package.md` — [COMPLETED] Implementation guide, decision tree, FAQ, and agent-handoff document for external adopters delivered and published (CRITICAL, Gate G4 support; depends on WO-0053, WO-0054)
- `docs/workorders/WO-0056-adopter-feedback-loop-and-contract-system.md` — [COMPLETED] Structured feedback loop, SLA, adopter registry, spec improvement queue, regression prevention policy, runner baseline mode, and CI regression gate implemented (HIGH, Gate G4 + G6 support; depends on WO-0053, WO-0055)
- `docs/workorders/WO-0057-spec-vs-implementation-documentation-clarity.md` — [COMPLETED] Spec-vs-implementation audit and messaging updates completed with external implementation CTAs and evidence report (HIGH, Gate G4 support; depends on WO-0054)
- `docs/workorders/WO-0058-v01-to-v02-migration-guide.md` — [COMPLETED] v0.1-to-v0.2 migration guide, compatibility matrix, code examples, and deprecation policy linkage published (HIGH, Gate G6 support; depends on WO-0053, WO-0057)
- `docs/workorders/WO-0059-governance-completion-breaking-change-deprecation-incident.md` — [COMPLETED] Breaking-change/deprecation/incident/release cadence policies plus incident simulation evidence completed (CRITICAL, Gate G6 + World-ready support; depends on WO-0058)

### Interactive Implementation Sandbox Wave (WO-0060 through WO-0068)

**Mandate:** [MANDATE-interactive-implementation-sandbox.md](/docs/MANDATE-interactive-implementation-sandbox.md)
**Scenario catalog:** `site/public/agent/sandbox-scenarios.json`
**Priority:** HIGHEST (per CEO mandate -- comes before WO-0053 through WO-0059)

- `docs/workorders/WO-0060-sandbox-foundation-and-browser-validator.md` — [COMPLETED] Extract validation logic for browser use with Web Crypto API adapter; scaffold sandbox pages and fixture pipeline (HIGHEST, foundational; no dependencies)
- `docs/workorders/WO-0061-sandbox-three-panel-layout-and-step-engine.md` — [COMPLETED] Build three-panel layout shell, step-through engine, step controls, bubble annotations, and manifest viewer/editor (HIGHEST; depends on WO-0060)
- `docs/workorders/WO-0062-sandbox-scenario-modal-and-navigation.md` — [COMPLETED] Build scenario selection modal with card grid, search/filter, and navigation between modal and sandbox (HIGHEST; depends on WO-0061)
- `docs/workorders/WO-0063-sandbox-getting-started-scenarios.md` — [COMPLETED] Implement 4 Getting Started scenarios (GS-01 through GS-04): first manifest, facets, forward compatibility, resolver (HIGHEST; depends on WO-0062)
- `docs/workorders/WO-0064-sandbox-trust-verification-scenarios.md` — [COMPLETED] Implement 5 Trust & Verification scenarios (TV-01 through TV-05): signed manifest, tamper detection, expired, missing fields, invalid algorithm (HIGHEST; depends on WO-0063)
- `docs/workorders/WO-0065-sandbox-integration-lane-scenarios.md` — [COMPLETED] Implement 8 Integration Lane scenarios (IL-01 through IL-08): social, smart glasses, metaverse, RP1, OMATrust, Chia, personhood, venue (HIGHEST; depends on WO-0063)
- `docs/workorders/WO-0066-sandbox-edge-case-and-advanced-scenarios.md` — [COMPLETED] Implement 4 Edge Case + 4 Advanced scenarios: temporal misuse, missing sig, clock skew, facet type, cross-system, pointers, revocation, full v0.2 (HIGHEST; depends on WO-0064)
- `docs/workorders/WO-0067-sandbox-visual-polish-and-illustrations.md` — [COMPLETED] Create 25 SVG illustrations, refine animations, category colors, dark mode, responsive polish (HIGH; depends on WO-0063, WO-0064, WO-0065, WO-0066)
- `docs/workorders/WO-0068-sandbox-ci-parity-testing-and-qa.md` — [COMPLETED] CI parity testing (Node vs browser validator), scenario smoke tests, accessibility audit, performance audit (HIGH; depends on WO-0060, WO-0063, WO-0064, WO-0065, WO-0066)

### Interactive Sandbox V2 Redesign Wave (WO-0069 through WO-0080)

**Proposal:** [Sandbox V2 UI Redesign Proposal](/.dev/ai/proposals/2026-03-01-02-39-39Z-universalmanifest-sandbox-ui-redesign-proposal.md)
**Handoff:** [V2 Handoff](/.dev/ai/handoffs/2026-03-01-03-55-34Z-handoff-universalmanifest.md)
**Priority:** HIGH (CEO-directed redesign of sandbox detail page to symmetrical two-entity protocol lens layout)

- `docs/workorders/WO-0069-sandbox-v2-hierarchy-explorer-component.md` — [COMPLETED] HierarchyExplorer: reusable collapsible JSON tree-view component (Phase 1 foundation; no dependencies)
- `docs/workorders/WO-0070-sandbox-v2-details-card-component.md` — [COMPLETED] DetailsCard: dual-mode detail card with hierarchy/JSON toggle (Phase 1 foundation; depends on WO-0069)
- `docs/workorders/WO-0071-sandbox-v2-session-state-and-types.md` — [COMPLETED] SessionStateIndicator + ScenarioDefinitionV2 types (Phase 1 foundation; no dependencies)
- `docs/workorders/WO-0072-sandbox-v2-entity-column-component.md` — [COMPLETED] EntityColumn: symmetrical entity panel with session state and manifest explorer (Phase 2 panels; depends on WO-0070, WO-0071)
- `docs/workorders/WO-0073-sandbox-v2-protocol-lens-component.md` — [COMPLETED] ProtocolLens: step-by-step protocol interaction viewer (Phase 2 panels; depends on WO-0071)
- `docs/workorders/WO-0074-sandbox-v2-subject-panel-component.md` — [COMPLETED] SubjectPanel: exchanged object display with dual-mode rendering (Phase 2 panels; depends on WO-0070)
- `docs/workorders/WO-0075-sandbox-v2-layout.md` — [COMPLETED] SandboxLayoutV2: new CSS Grid layout with header transport controls (Phase 3 layout; depends on WO-0072, WO-0073, WO-0074)
- `docs/workorders/WO-0076-sandbox-v2-engine.md` — [COMPLETED] SandboxEngineV2: two-entity state management with subject and protocol lens (Phase 3 engine; depends on WO-0071)
- `docs/workorders/WO-0077-sandbox-v2-scenario-detail-page-rewrite.md` — [COMPLETED] Scenario detail page rewrite: wire V2 layout, components, and engine (Phase 4 integration; depends on WO-0075, WO-0076)
- `docs/workorders/WO-0078-sandbox-v2-getting-started-scenario-migration.md` — [COMPLETED] Getting Started scenario migration to V2 format, GS-01 through GS-04 (Phase 4 integration; depends on WO-0076)
- `docs/workorders/WO-0079-sandbox-v2-remaining-scenario-migration.md` — [COMPLETED] Remaining scenario migration to V2 format: TV, IL, EC, AD -- 21 scenarios (Phase 5 polish; depends on WO-0077, WO-0078)
- `docs/workorders/WO-0080-sandbox-v2-responsive-polish-animations-a11y.md` — [COMPLETED] Responsive polish, animations, and accessibility audit (Phase 5 polish; depends on WO-0077)

### Audit-Driven Work Orders (WO-0081 through WO-0111)

**Source:** Three audit reports from 2026-03-01:
- Spec-vs-Implementation Boundary Audit
- Project Completeness and Vision Audit
- Documentation Freshness Audit

#### Spec-vs-Implementation Boundary Fixes

- `docs/workorders/WO-0081-add-specification-identity-banner-to-entry-points.md` — [COMPLETED] Add "UM is a specification" banner to root README, site landing page, and spec READMEs (P0; no dependencies)
- `docs/workorders/WO-0082-remove-implementation-references-from-spec-documents.md` — [COMPLETED] Remove or qualify implementation-specific references (Shield, TS file paths, Solid Pod) from spec documents (P0; no dependencies)
- `docs/workorders/WO-0083-restructure-root-readme-quick-start.md` — [COMPLETED] Restructure root README Quick Start to lead with the specification, not npm commands (P0; depends on WO-0081)
- `docs/workorders/WO-0084-restructure-site-sidebar-spec-vs-implementation.md` — [COMPLETED] Restructure docs site sidebar to separate spec from implementation; also fix 3 missing integration lanes in sidebar (P1; no dependencies)
- `docs/workorders/WO-0085-create-build-your-own-implementation-page.md` — [COMPLETED] Create "Build Your Own Implementation" language-neutral page for the docs site (P1; coordinates with WO-0084)
- `docs/workorders/WO-0086-add-spec-implementation-language-guidelines.md` — [COMPLETED] Add spec-vs-implementation language guidelines and agent boundary awareness to PROJECT-RULES.md and Quick Start (P1; no dependencies)
- `docs/workorders/WO-0087-reposition-typescript-in-agent-briefing-and-explainers.md` — [COMPLETED] Reposition TypeScript helper in agent briefing and explainer docs — move from Key Facts to Reference Implementation section (P1; no dependencies)
- `docs/workorders/WO-0088-qualify-typescript-references-in-integration-docs.md` — [COMPLETED] Qualify TypeScript-specific references in integration template, social.md, and rp1-spatial-fabric.md (P1; no dependencies)
- `docs/workorders/WO-0089-fix-legacy-naming-and-branding-leaks.md` — [COMPLETED] Fix legacy @localartistnetwork package name, Shield device references in governance, NVIDIA references in briefing (P2; no dependencies)
- `docs/workorders/WO-0090-add-governance-boundary-awareness-section.md` — [COMPLETED] Add normative-vs-supplementary hierarchy to GOVERNANCE.md project scope (P2; no dependencies)

#### Project Completeness and External-Facing Content

- `docs/workorders/WO-0091-publish-explainer-documents-on-site.md` — [COMPLETED] Publish one-pager, full briefing, and agent briefing as pages on universalmanifest.net under "About" section (P0; no dependencies)
- `docs/workorders/WO-0092-create-standalone-adoption-guide.md` — [COMPLETED] Create "How to Adopt UM" guide consolidating adoption tiers and adoption path for third parties (P0; coordinates with WO-0055)
- `docs/workorders/WO-0093-create-standards-positioning-document.md` — [COMPLETED] Create standards positioning document covering W3C, IETF, MSF, OMA3, LF relationship and standardization intent (P0; no dependencies)
- `docs/workorders/WO-0094-fix-github-repository-url-inconsistencies.md` — [COMPLETED] Resolve 4 conflicting GitHub URLs (LocalArtistNetwork, WebOfTrustInfo, nicholasgrigoriadis, universalmanifest) across all files (P0; no dependencies)
- `docs/workorders/WO-0095-create-outreach-and-adoption-strategy-document.md` — [COMPLETED] Create outreach strategy with target audiences, channels, launch checklist, and timeline (P1; no dependencies)
- `docs/workorders/WO-0096-create-why-um-page-on-site.md` — [COMPLETED] Create "Why UM?" non-technical landing page leading with the fragmentation problem (P1; depends on WO-0091)
- `docs/workorders/WO-0097-publish-commercial-journeys-on-site.md` — [COMPLETED] Publish 5 commercial journeys (creator, venue, app dev, privacy, enterprise) as site pages under Use Cases (P1; no dependencies)
- `docs/workorders/WO-0098-create-resolver-api-reference-page.md` — [COMPLETED] Consolidate resolver documentation into single API reference page on the site (P1; no dependencies)
- `docs/workorders/WO-0099-create-standards-landscape-comparison-page.md` — [COMPLETED] Publish standards comparison page (UM vs VCs, DIDComm, Solid, OIDC) on the site (P1; depends on WO-0093)
- `docs/workorders/WO-0100-create-how-we-build-this-contributor-page.md` — [COMPLETED] Create contributor-facing methodology page explaining journeys, done-done, and work orders (P1; no dependencies)
- `docs/workorders/WO-0101-add-changelog-and-release-notes-page-to-site.md` — [COMPLETED] Add changelog/release notes page to the public site (P1; no dependencies)
- `docs/workorders/WO-0102-create-integration-authoring-guide.md` — [COMPLETED] Publish existing integration authoring guide on the site and fix broken catalog link (P1; no dependencies)
- `docs/workorders/WO-0110-create-msf-relationship-document.md` — [COMPLETED] Document Metaverse Standards Forum lineage, current relationship, and future plans (P2; coordinates with WO-0093)
- `docs/workorders/WO-0111-organize-animated-svgs-into-browsable-gallery.md` — [COMPLETED] Organize 29 production animated SVGs into browsable gallery page on the site (P2; depends on WO-0105)

### myum Resolver Consumer Frontend + Runtime Reality (WO-0112)

- `docs/workorders/WO-0112-myum-consumer-frontend-and-runtime-reality-audit.md` — [COMPLETED] Deliver a senior-team-grade live-vs-stub/mocks comprehensive report and implement a friendly consumer resolver frontend with detailed page specs and HTML wireframes (P0; depends on WO-0098 and current myum audit baseline)

### Deployment and Operations Hardening Wave (WO-0113 through WO-0118)

- `docs/workorders/WO-0113-establish-staging-environments-and-promotion-model.md` — [COMPLETED] Staging infrastructure is operational on active custom domains (`staging.universalmanifest.net`, `staging.myum.net`, `www.staging.myum.net`) with isolated staging KV/routes, promotion flow, and fallback hosts retained for resilience (P0; foundational for safe release iteration)
- `docs/workorders/WO-0114-automate-deploy-pipeline-with-release-gates.md` — [COMPLETED] Gated staged/prod deployment workflow is implemented and verified green on custom-domain staging targets (P0; depends on WO-0113)
- `docs/workorders/WO-0115-pin-toolchain-versions-and-runtime-baselines.md` — [COMPLETED] Pinned Node/Wrangler/runtime baselines across local + CI and verified baseline commands (P1; supports reproducible builds/tests/deploys)
- `docs/workorders/WO-0116-expand-resolver-test-suite-for-contract-coverage.md` — [COMPLETED] Added resolver contract test suite with full status/header/path coverage and wired it into CI (`resolver-contract` job) (P0; hardens `myum.net` behavior regression detection)
- `docs/workorders/WO-0117-add-synthetic-monitoring-alerting-and-slo-policy.md` — [COMPLETED] Continuous synthetic monitoring and SLO policy are active for production plus custom-domain staging, with fallback-host resilience and alerting templates (P1; depends on WO-0113 and WO-0114)
- `docs/workorders/WO-0118-staging-custom-domain-dns-cutover-automation.md` — [COMPLETED] Automated staging target selection now prefers custom domains when reachable and falls back to staging hosts with shared logic across deploy gates and synthetic monitoring (P1; depends on WO-0113, WO-0114, and WO-0117)

### Runtime Reality and Post-Deploy Follow-on Wave (WO-0119 through WO-0122)

- `docs/workorders/WO-0119-resolver-route-canonicalization-and-fixture-freshness-lock.md` — [COMPLETED] Removed resolver route canonicalization loop risk and refreshed default resolver fixture validity window with staged/prod deployment plus live freshness verification (P0; follows WO-0112/WO-0114)
- `docs/workorders/WO-0120-harness-307-contract-parity-and-trust-matrix.md` — [COMPLETED] Harness resolver flows now treat contract-valid `307` redirects as pass with deployed browser verification evidence and production smoke/post-deploy checks (P1; follows WO-0112/WO-0116)
- `docs/workorders/WO-0121-synthetic-alert-delivery-and-escalation-drill.md` — [COMPLETED] External webhook alerting configured and sustained-failure drill executed with delivered payload and incident evidence (P1; follows WO-0117)
- `docs/workorders/WO-0122-runtime-status-messaging-reconciliation.md` — [COMPLETED] Runtime-facing docs and resolver metadata reconciled to active deployed-service language, with residual historical references inventoried (P2; follows WO-0112/WO-0113)

### Credential Stabilization Follow-on (WO-0123)

- `docs/workorders/WO-0123-cloudflare-credential-stabilization-for-gated-production-promotions.md` — [COMPLETED] Cloudflare staging/production credential isolation applied and validated by two consecutive green gated production promotions (`22658547313`, `22658652963`) with production resolver/docs/verify gates all passing (P0; follows WO-0113 through WO-0118 and post-hardening validations)

### Credential Durability Hardening (WO-0124)

- `docs/workorders/WO-0124-rotate-ci-cloudflare-secrets-to-long-lived-api-tokens.md` — [COMPLETED] Enforced API-token-only deploy auth (`CF_REQUIRE_API_TOKEN_STAGING/PRODUCTION=true`), fixed auth-type matching for Cloudflare `Account API Token`, and validated full gated production promotion + synthetic production monitor green (`22659412126`, `22659519824`); post-closeout permission-gap remediation reconfirmed production promotion green after zone route scope correction (`22702756070`) (P0; follows WO-0123)

#### Documentation Freshness and Maintenance

- `docs/workorders/WO-0103-update-docs-readme-with-missing-references.md` — [COMPLETED] Update docs/README.md to reference ~20 new document categories created this week (P0; no dependencies)
- `docs/workorders/WO-0104-update-critical-path-with-current-work-streams.md` — [COMPLETED] Update CRITICAL-PATH.md with sandbox wave, external adopter wave, teaching scripts, and code examples phases (P0; no dependencies)
- `docs/workorders/WO-0105-fix-animated-svg-count-across-documents.md` — [COMPLETED] Fix animated SVG count from "16" to actual count (29 production, 33 total) across STATE-OF-THE-PROJECT, diagrams/README, and ANIMATED-SVG-WORKFLOW (P1; no dependencies)
- `docs/workorders/WO-0106-update-state-of-the-project-with-current-status.md` — [COMPLETED] Fix stale status pointers, update WO-0060-0068 status to COMPLETED, correct SVG and fixture counts (P0; depends on WO-0107)
- `docs/workorders/WO-0107-commit-interactive-sandbox-and-design-artifacts.md` — [COMPLETED] Commit all uncommitted sandbox code (V1+V2), design docs, and configuration changes (P0; no dependencies)
- `docs/workorders/WO-0108-create-formal-wo-files-for-sandbox-v2.md` — [COMPLETED] Create formal WO files for WO-0069 through WO-0080 (Sandbox V2 redesign) and add to index (P1; depends on WO-0107)
- `docs/workorders/WO-0109-add-ci-workflow-decision-record.md` — [COMPLETED] Add decision record for expanded CI workflow (ci.yml, WO-0049) to DECISIONS.md (P2; no dependencies)

### Go-Now Program Execution Wave (WO-0125 through WO-0126)

- `docs/workorders/WO-0125-portable-identity-profile-go-now-execution-and-integration-pages.md` — [COMPLETED] Portable Identity Profile Go-Now stream (`PIP-GN-01` through `PIP-GN-06`) executed with integration pages, implementation-path guidance, and governance synchronization evidence (P0)
- `docs/workorders/WO-0126-metaverse-universal-manifest-go-now-execution-and-integration-pages.md` — [COMPLETED] Metaverse Universal Manifest Go-Now stream (`MUM-GN-01` through `MUM-GN-06`) executed with integration hardening, synchronization-profile guidance, and governance synchronization evidence (P0)

### Privacy Signal Standards Review Wave (WO-0127)

- `docs/workorders/WO-0127-gpc-standards-integration-review-and-gap-analysis.md` — [COMPLETED] Three-draft, standards-grounded GPC integration review with overlap/gap analysis, normative reference crosswalk, and facet-vs-non-facet recommendation package (P0)
- `docs/workorders/WO-0128-gpc-go-now-runtime-mapping-fixtures-and-proof.md` — [COMPLETED] Execute GPC runtime mapping, support-resource parsing, fixture coverage, and journey proof in the TypeScript reference implementation (P0)

### Inbox Corpus Hygiene Wave (WO-0129)

- `docs/workorders/WO-0129-universal-manifest-inbox-dedupe-import-and-archive.md` — [COMPLETED] Audited the Universal Manifest inbox corpus, localized missing research/design materials, and archived processed inbox sources into the imported-project lane (P1)

### Localized Source Follow-on Wave (WO-0130 through WO-0136)

- `docs/workorders/WO-0130-composite-architecture-and-active-runtime-alignment.md` — [COMPLETED] Aligned source-of-truth architecture docs with the composite-stack model and local-first active-runtime behavior surfaced by the newly localized corpus (P0)
- `docs/workorders/WO-0131-did-vc-and-metaverse-lane-refresh-from-localized-corpus.md` — [COMPLETED] Refresh DID + VC and metaverse integration lanes from the newly localized corpus with stronger volatility and non-lock-in boundaries (P1)
- `docs/workorders/WO-0132-research-first-protocol-volatility-proximity-and-federation-gaps.md` — [COMPLETED] Convert unresolved protocol-volatility, proximity-credential, and federation-bridge gaps into an explicit Research-First decision package with promotion gates (P1)
- `docs/workorders/WO-0133-protocol-recommendation-governance-and-standards-currency-matrix.md` — [COMPLETED] Create the governance and standards-currency mechanism that determines when volatile protocol families move from examples to recommended guidance (P1)
- `docs/workorders/WO-0134-proximity-credential-and-presentation-profile-assessment.md` — [COMPLETED] Define the boundary profile for proximity-triggered credential presentation without collapsing transport semantics into the UM core contract (P1)
- `docs/workorders/WO-0136-omb-wiki-spatial-fabric-source-refresh-and-primary-source-crosscheck.md` — [COMPLETED] Audit `omb.wiki` for spatial-fabric details not yet reflected in the RP1 lane, while preserving primary repositories/specs as the source of record when the wiki lags or diverges (P1)
- `docs/workorders/WO-0135-federation-and-bridge-strategy-decision-package.md` — [COMPLETED] Produce a standards-neutral decision package for federation, sync, and closed-surface bridge roles around subject-controlled runtimes (P1)

### Runtime Guidance and Spatial-Fabric Refresh Wave (WO-0137 through WO-0138)

- `docs/workorders/WO-0137-role-based-runtime-federation-and-bridge-guidance-refresh.md` — [COMPLETED] Refresh shared runtime and synchronization guidance with the new role-based federation and bridge taxonomy without making any substrate normative for UM (P1)
- `docs/workorders/WO-0138-rp1-msf-primary-source-refresh-and-integration-depth-pass.md` — [COMPLETED] Refresh RP1/MSF primary sources, localize additional open-source/runtime asset-delivery sources, and deepen the spatial-fabric integration lane while preserving the current UM core boundary (P1)

### RP1/MSF Adversarial Hardening Wave (WO-0139)

- `docs/workorders/WO-0139-rp1-msf-adversarial-attachment-and-session-hardening.md` — [COMPLETED] Add fail-closed RP1/MSF proof for stale attachment traversal and expired/revoked session-context replay without expanding the UM core contract (P1)

### Consumer Resolver UX Hardening (WO-0144)

- `docs/workorders/WO-0144-myum-consumer-provenance-and-example-state-hardening.md` — [COMPLETED] Eliminate live-vs-fallback ambiguity in the consumer resolver UX and add/verify live production example states for contract-visible redirect/revoked behavior where possible (P0)

### K2B Concept Integration Traceability (WO-0140)

- `docs/workorders/WO-0140-k2b-concept-integration-transfer-map.md` — [COMPLETED] Create a consolidated transfer map showing how the recent concept-integration wave materialized from research and blueprint inputs into integration guidance, journeys, and proof surfaces (P1)

### Metaverse Portaling Integration (WO-0141)

- `docs/workorders/WO-0141-metaverse-portaling-integration-and-guidance-refresh.md` — [COMPLETED] Make portaling explicit as the cross-platform movement model for the metaverse lane, journey language, and teaching surfaces without changing the UM core contract (P1)

### Ecosystem Expansion & Architecture Research (WO-0142 through WO-0143)

- `docs/workorders/WO-0142-payment-handles-and-fiat-crypto-gateway-integration.md` — [COMPLETED] Create explicit standard pointers/overlays for fiat (Stripe/PayPal) and crypto gateways, establishing universal payment handle integration without leaking financial data (P1)
- `docs/workorders/WO-0143-private-encrypted-inline-facets-vs-projection-model-analysis.md` — [COMPLETED] Deep analysis completed with accepted additive privacy model (projection normative + encrypted inline facets guidance), lifecycle guidance, and signed encrypted-facet lifecycle fixtures (P1)

### Vignette Explainer Library (WO-0145)

- `docs/workorders/WO-0145-vignette-video-library.md` — [COMPLETED] Established the foundational vignette library package (UI audit + V-01 through V-05 scripts + workflow), then formally handed off active production/publishing execution to the WO-0149 hierarchy pipeline and production queue (P1)

### IWPS Alignment and OMA3 Presentation Wave (WO-0146 through WO-0148)

- `docs/workorders/WO-0146-iwps-specification-localization.md` — [COMPLETED] Localized IWPS Base Specification v0.3 from OMA3 GitHub to project markdown at `docs/research/iwps-base-specification-v0.3.md` (877 lines, full spec with APIs, identity framework, auth tiers) (P0)
- `docs/workorders/WO-0147-iwps-um-alignment-analysis.md` — [COMPLETED] Comprehensive IWPS–UM alignment analysis: layer mapping, integration points, proposed portal flow, gap analysis, and OMA3 recommendations at `docs/reports/2026-03-11-iwps-um-alignment-analysis.md` (P0)
- `docs/workorders/WO-0148-oma3-presentation-explainer-package.md` — [COMPLETED] OMA3 presentation explainer package with 9-section architectural overview and NotebookLM briefs at `docs/presentations/2026-03-12-oma3-*` (P0)

### Video Explainer Hierarchy (WO-0149)

- `docs/workorders/WO-0149-video-explainer-hierarchy-of-discovery.md` — [COMPLETED] Designed 4-level video hierarchy of discovery (meta/index → master → audience summaries → topic deep dives → micro-vignettes) with NotebookLM briefs for 16 named videos; supersedes flat vignette approach (P1)

### Hackathon Learnings and Concept Documents (WO-0150 through WO-0151)

- `docs/workorders/WO-0150-spatial-fabric-hackathon-learnings-report.md` — [COMPLETED] Standalone hackathon learnings report documenting UM concepts validated in the peer-mesh-spatial-fabric proof-of-concept, IWPS alignment implications, and adoption patterns at `docs/reports/2026-03-11-spatial-fabric-hackathon-learnings.md` (P0)
- `docs/workorders/WO-0151-avatar-equip-tool-concept.md` — [COMPLETED] Avatar equip tool concept document: gamified UM management interface with AAA-style equip menu, facet-to-slot mapping, spec pressure points, and IWPS portaling relationship at `docs/concepts/avatar-equip-tool.md` (P1)

### Portal Loading Content (WO-0152)

- `docs/workorders/WO-0152-portal-loading-content-integration.md` — [COMPLETED] CEO mandate for destination-world loading content during portal transitions; integrated loading content pointers into metaverse integration lane, IWPS alignment, portaling explainer, and video briefs (P1)

### Facet Encryption Deep Dive (WO-0153)

- `docs/workorders/WO-0153-facet-encryption-deep-dive-report.md` — [COMPLETED] Comprehensive facet visibility and encryption deep dive: three approaches (projection, consent, encrypted inline), three encryption methods (JWE, BBS+/SD-JWT, HPKE envelope), engineering justifications, and L3-10 video brief at `docs/explainers/facet-encryption-deep-dive.md` (P1)

### Hashing and Data Bundling Deep Dive (WO-0154)

- `docs/workorders/WO-0154-hashing-and-data-bundling-deep-dive.md` — [COMPLETED] Comprehensive hashing, caching, and data bundling deep dive: SHA-256 ETags, Ed25519+JCS signing, pointer-first architecture, CID deferral rationale, digestMultibase pointer integrity proposal, CBOR-LD future profile, and L3-11 video brief at `docs/explainers/hashing-and-data-bundling-deep-dive.md` (P1)

### Concept Hierarchy Explorer and Ecosystem Namespace (WO-0155)

- `docs/workorders/WO-0155-concept-hierarchy-explorer-and-ecosystem-namespace.md` — [COMPLETED] Interactive single-page concept hierarchy explorer showing the full breadth of UM application domains, plus ecosystem namespace vision for external compliance submissions and distributed name management (P0)

### OMA3 Handout Collection Site Publication (WO-0156)

- `docs/workorders/WO-0156-oma3-handout-collection-site-publication.md` — [COMPLETED] Publish OMA3 handout collection as navigable subsection on universalmanifest.net with proper Starlight integration (P0)

### Agent-Friendly Multi-Surface Program (WO-0157 through WO-0160)

- `docs/workorders/WO-0157-landing-surface-and-multi-layer-interaction-architecture.md` — [COMPLETED] Defined the target multi-surface public architecture and execution sequence for landing, docs, discovery, tooling, and runtime boundaries in `docs/reports/2026-03-15-multi-surface-agent-friendly-architecture.md` (P0)
- `docs/workorders/WO-0158-agent-discovery-and-machine-readable-entrypoints.md` — [COMPLETED] Published the public discovery layer across universalmanifest.net and myum.net, including `llms.txt`, `security.txt`, enriched well-known descriptors, a `/for-agents/` route, generated fixture/scenario catalogs, and runtime OpenAPI/security endpoints documented in `docs/reports/2026-03-15-agent-discovery-and-machine-readable-entrypoints-report.md` (P0)
- `docs/workorders/WO-0159-external-agent-onboarding-and-wild-adoption-documentation.md` — [COMPLETED] Added the external-agent onboarding path, updated discovery-facing docs/sidebar wiring, and documented the internal adoption argument plus measurable signals in `docs/reports/2026-03-15-external-agent-onboarding-and-adoption-memo.md` (P0)
- `docs/workorders/WO-0160-agent-facing-content-completeness-and-verification-gates.md` — [COMPLETED] Defined the agent-facing publication gate framework, public governance page, and publish/no-publish verification model in `docs/reports/2026-03-15-agent-facing-publication-gates-framework.md` (P0)

### Landing-First Public Experience Implementation (WO-0161)

- `docs/workorders/WO-0161-landing-page-and-docs-secondary-route-implementation.md` — [COMPLETED] Implemented the landing-first root experience, added `/docs/` as the curated secondary docs entry path, preserved existing deep routes, and introduced audience lanes plus shared public navigation documented in `docs/reports/2026-03-15-landing-first-public-experience-implementation-report.md` (P0)

### Agent Path Drift Reconciliation (WO-0162)

- `docs/workorders/WO-0162-agent-path-drift-reconciliation-and-starlight-warning-cleanup.md` — [COMPLETED] Reconciled older authority docs with the new agent path and resolved the Starlight duplicate-id warning by adopting the required `docsLoader()` configuration, documented in `docs/reports/2026-03-17-agent-path-drift-and-starlight-loader-fix.md` (P1)

### Remaining Site Build Warning Triage (WO-0163)

- `docs/workorders/WO-0163-remaining-site-build-warning-triage-and-noise-reduction.md` — [COMPLETED] Triaged the three remaining non-blocking site build warnings, removing the sandbox mixed-import warning and the Pagefind `/workbench/index/` warning while explicitly accepting the intentional Starlight `/` route-priority override in `docs/reports/2026-03-17-remaining-site-build-warning-triage-and-noise-reduction.md` (P2)

### Docs Root Relocation (WO-0164)

- `docs/workorders/WO-0164-docs-root-relocation-and-warning-free-build-baseline.md` — [COMPLETED] Relocated the old docs-root content to `/docs/overview/`, linked it from the curated `/docs/` entry, and removed the last Starlight root-route warning in `docs/reports/2026-03-19-docs-root-relocation-warning-free-build-baseline.md` (P2)

### Universal Manifest Architecture & Specification Update (WO-0165 through WO-0170)

- Historical note: the per-WO `.dev/ai/workorders/...` paths previously listed for WO-0165 through WO-0170 are not present in the current checkout. The surviving outputs of this wave are integrated into the main repo artifacts below.
- `docs/W3C-STYLE-SPEC.html` — [COMPLETED] W3C-style specification shell, sidebar behavior, and public root-route transition output.
- `site_backup.tar.gz` — [COMPLETED] Backup artifact captured before the public spec/homepage transition.
- `site/src/pages/index.astro` — [COMPLETED] Public root route now serves the W3C-style specification HTML shell.
- `docs/DECISIONS.md` — [COMPLETED] Architectural decisions from the synthetic-review and identity-binding wave recorded in the canonical decision log.
- `docs/VERSION-DIFFERENCES-V01-V02.md` — [COMPLETED] v0.2 identity-binding, trust-tier, and delegation deltas integrated into the version-differences layer.
- `docs/security/THREAT-MODEL.md` — [COMPLETED] Bag-of-Claims / identity-correlation threat model integrated into the security layer.
