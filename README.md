# Universal Manifest — Documentation Index

This is the entry point for the Universal Manifest spec repo.

Canonical repo path: `<repo-root>`

## Repo map

- `spec/` — Versioned spec artifacts (JSON-LD context, schemas, normative text)
- `examples/` — Example manifests (valid + invalid fixtures as the spec stabilizes)
- `examples/code/` — 12 runnable code examples (hello-world, validation, signing, facets, resolution, projection, and more)
- `examples/demo-app/` — Full demo application with server and library
- `integrations/` — Practical guidance for consuming/producing manifests across adopter surfaces
- `research/` — Imported background docs and synthesis from supporting design libraries
- `packages/` — Reusable code (types/validators) for producers/consumers
- `docs/workorders/` — Work orders for scoped project tasks

## Foundation files

- [`CODE_OF_CONDUCT.md`](../CODE_OF_CONDUCT.md) — Community code of conduct
- [`CONTRIBUTING.md`](../CONTRIBUTING.md) — Contribution guidelines
- [`LICENSE`](../LICENSE) — Project license
- [`SECURITY.md`](../SECURITY.md) — Security policy and vulnerability reporting
- Project-specific onboarding and operational rules are maintained through the repo’s active root instructions when present.

## Key docs

- [`docs/PROJECT-VISION.md`](PROJECT-VISION.md) — What this standard aims to enable (and what’s out of scope)
- [`docs/DEPTH-AND-SCOPE.md`](DEPTH-AND-SCOPE.md) — High-level depth + scope map for this repo
- [`docs/STATE-OF-THE-PROJECT.md`](STATE-OF-THE-PROJECT.md) — Current status, milestones, and next steps
- [`docs/COMPREHENSIVE-PROJECT-PROPERTIES-AND-SURFACES-MAP.md`](COMPREHENSIVE-PROJECT-PROPERTIES-AND-SURFACES-MAP.md) — Full structural map of repo ownership, public properties, route families, runtime surfaces, and source-of-truth boundaries
- [`docs/CANONICAL-ROUTE-AND-COMPATIBILITY-ALIAS-POLICY.md`](CANONICAL-ROUTE-AND-COMPATIBILITY-ALIAS-POLICY.md) — Canonical versus alias-only route policy for public paths, compatibility shims, and retirement candidates
- [`docs/FIXTURE-SOURCE-OF-TRUTH-AND-PUBLISHED-MIRROR-POLICY.md`](FIXTURE-SOURCE-OF-TRUTH-AND-PUBLISHED-MIRROR-POLICY.md) — Canonical authored-versus-generated policy for fixtures, browser-published mirrors, and sync behavior
- [`docs/HOME-CLUSTER-SITEMAP.md`](HOME-CLUSTER-SITEMAP.md) — Approved IA direction for the public Home cluster before implementation resumes
- [`docs/HOME-CLUSTER-COPY-BRIEFS.md`](HOME-CLUSTER-COPY-BRIEFS.md) — Copy briefs for the approved Home-cluster pages
- [`docs/AUDIENCE-PAGE-BRIEFS.md`](AUDIENCE-PAGE-BRIEFS.md) — First-wave audience-page briefs for approved audience routes
- [`docs/MARKDOWN-SOURCE-FIDELITY-PROCESS.md`](MARKDOWN-SOURCE-FIDELITY-PROCESS.md) — Process for keeping markdown/source, rendered pages, machine-readable files, and agent-facing variants aligned
- [`docs/CRITICAL-PATH.md`](CRITICAL-PATH.md) — Minimal sequence for adoption + publishing + “world-ready” claims
- [`docs/UNIVERSAL-MANIFEST-BRIEFING.md`](UNIVERSAL-MANIFEST-BRIEFING.md) — Full AI agent briefing on the Universal Manifest standard
- [`docs/MANDATE-interactive-implementation-sandbox.md`](MANDATE-interactive-implementation-sandbox.md) — CEO mandate for the interactive implementation sandbox
- [`docs/DOMAIN-ARCHITECTURE.md`](DOMAIN-ARCHITECTURE.md) — Domain split: standards site vs UMID resolver
- [`docs/reports/2026-03-15-multi-surface-agent-friendly-architecture.md`](reports/2026-03-15-multi-surface-agent-friendly-architecture.md) — Current public-surface architecture for landing, docs, discovery, tooling, and runtime boundaries
- [`docs/PUBLISHING-AND-VERSIONING.md`](PUBLISHING-AND-VERSIONING.md) — How spec artifacts get hosted + versioned for adopters
- [`docs/RELEASING.md`](RELEASING.md) — Draft release process for spec versions + publishing
- [`docs/DEPLOY-CHECKLIST.md`](DEPLOY-CHECKLIST.md) — One linear checklist for first real deploy (`universalmanifest.net` + `myum.net`)
- [`docs/CRUCIAL-DETAILS.md`](CRUCIAL-DETAILS.md) — Non-obvious decisions and “gotchas”
- [`docs/DECISIONS.md`](DECISIONS.md) — Decisions made while drafting the standard
- [`docs/VERSION-DIFFERENCES-V01-V02.md`](VERSION-DIFFERENCES-V01-V02.md) — v0.1 to v0.2 delta including signatures, claim authenticity, tiered trust, `claimProof`, and identity binding
- [`docs/ENVELOPE-TOPOLOGY.md`](ENVELOPE-TOPOLOGY.md) — Structural topology analysis: what “envelope” means, how manifest layers relate, terminology guide
- [`docs/PROJECT-KNOWLEDGE-INDEX.md`](PROJECT-KNOWLEDGE-INDEX.md) — Pointer to GAS shared Universal Manifest master index
- [`docs/DONE-DONE-DEFINITION.md`](DONE-DONE-DEFINITION.md) — Official completion criteria (“done done”) for releases
- [`docs/DONE-DONE-CHECKLIST.md`](DONE-DONE-CHECKLIST.md) — Gate-by-gate checklist for release readiness
- [`docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`](DONE-DONE-EVIDENCE-PACK-TEMPLATE.md) — Required evidence template for done-done sign-off
- [`docs/TS-HELPER-PACKAGE.md`](TS-HELPER-PACKAGE.md) — What the TS helper is, how it’s used, distribution policy
- [`docs/journeys/README.md`](journeys/README.md) — Canonical user journeys mapped to an executable proof suite
- [`docs/diagrams/README.md`](diagrams/README.md) — Diagram source + export workflow (Excalidraw to SVG)
- [`docs/STUB-MANIFESTS.md`](STUB-MANIFESTS.md) — Near-real example manifests (fixtures) + section drivers
- [`docs/WORKLOG-2026-02-11.md`](WORKLOG-2026-02-11.md) — Initial repo bootstrap worklog
- [`docs/WORKLOG-2026-02-12.md`](WORKLOG-2026-02-12.md) — Stub fixtures + validation worklog
- [`docs/AGENT-OBSERVED-GAPS.md`](AGENT-OBSERVED-GAPS.md) — Append-only list of missing/unclear items

## Teaching scripts and explainers

- [`docs/teaching-scripts/`](teaching-scripts/) — Teaching scripts system with staged explanations for 30-second, 3-minute, and 15-minute audiences
  - [`README.md`](teaching-scripts/README.md) — Teaching scripts overview
  - [`01-ICONIC-REPRESENTATION.md`](teaching-scripts/01-ICONIC-REPRESENTATION.md) — Capsule-Pod iconic representation (approved)
  - [`02-SCRIPT-FORMAT.md`](teaching-scripts/02-SCRIPT-FORMAT.md) — Script format specification
  - [`03-SCRIPT-IDEAS.md`](teaching-scripts/03-SCRIPT-IDEAS.md) — 20 script ideas defined
- [`docs/explainers/`](explainers/) — Explainer documents at various depth levels
  - [`paragraph.md`](explainers/paragraph.md) — One-paragraph explainer
  - [`one-pager.md`](explainers/one-pager.md) — One-page explainer
  - [`full-briefing.md`](explainers/full-briefing.md) — Full briefing document
  - [`metaverse-portaling.md`](explainers/metaverse-portaling.md) — Explainer for cross-platform portaling with UM as the portable envelope
  - [`facet-encryption-deep-dive.md`](explainers/facet-encryption-deep-dive.md) — Facet privacy, projection, encrypted inline facets, and selective-disclosure tradeoffs
  - [`agent-briefing.md`](explainers/agent-briefing.md) — AI agent briefing
  - [`animation-briefing.md`](explainers/animation-briefing.md) — Animation briefing
- [`docs/scripts/`](scripts/) — Animation scripts
  - [`script-what-is-um.md`](scripts/script-what-is-um.md) — “What is Universal Manifest?” script
  - [`script-how-it-works.md`](scripts/script-how-it-works.md) — “How it works” script
  - [`script-why-it-matters.md`](scripts/script-why-it-matters.md) — “Why it matters” script
  - [`script-day-in-the-life.md`](scripts/script-day-in-the-life.md) — “Day in the life” script

## Commercial journeys

- [`docs/journeys/commercial/`](journeys/commercial/) — Commercial adoption journeys
  - [`creator-journey.md`](journeys/commercial/creator-journey.md) — Creator adoption journey
  - [`venue-operator-journey.md`](journeys/commercial/venue-operator-journey.md) — Venue operator adoption journey
  - [`app-developer-journey.md`](journeys/commercial/app-developer-journey.md) — App developer adoption journey
  - [`privacy-journey.md`](journeys/commercial/privacy-journey.md) — Privacy-focused adoption journey
  - [`enterprise-journey.md`](journeys/commercial/enterprise-journey.md) — Enterprise adoption journey

## Design and visual assets

- [`docs/design/ANIMATED-SVG-WORKFLOW.md`](design/ANIMATED-SVG-WORKFLOW.md) — Animated SVG production workflow
- [`docs/design/ANIMATED-SVG-SPEC.md`](design/ANIMATED-SVG-SPEC.md) — Animated SVG specification
- [`docs/design/ANIMATION-PLACEMENT-PLAN.md`](design/ANIMATION-PLACEMENT-PLAN.md) — Animation placement plan
- [`docs/design/ANIMATION-QA-CHECKLIST.md`](design/ANIMATION-QA-CHECKLIST.md) — Animation QA checklist
- [`docs/design/ANIMATION-WORKFLOW-AND-VERSION-STATUS.md`](design/ANIMATION-WORKFLOW-AND-VERSION-STATUS.md) — Canonical active/deprecated workflow and version status for animation assets
- [`docs/design/INFOGRAPHIC-STYLES-INVENTORY.md`](design/INFOGRAPHIC-STYLES-INVENTORY.md) — Complete infographic styles inventory
- [`docs/design/CAPSULE-POD-DESIGN.md`](design/CAPSULE-POD-DESIGN.md) — Capsule-Pod iconic representation design spec
- [`docs/design/LOGO-REFERENCE.md`](design/LOGO-REFERENCE.md) — Imported logo exploration asset reference pack
- [`docs/design/PERMISSIONS-FIREWALL-DESIGN.md`](design/PERMISSIONS-FIREWALL-DESIGN.md) — Permissions firewall design

## Governance

- [`docs/governance/`](governance/) — Governance framework
  - [`GOVERNANCE.md`](governance/GOVERNANCE.md) — Governance model
  - [`BRANCH-PROTECTION.md`](governance/BRANCH-PROTECTION.md) — Branch protection rules
  - [`CONTRIBUTING-REGISTRY.md`](governance/CONTRIBUTING-REGISTRY.md) — Contributor registry
  - [`MAINTAINERS.md`](governance/MAINTAINERS.md) — Maintainer roster
  - [`RFC-TEMPLATE.md`](governance/RFC-TEMPLATE.md) — RFC process template

## Security

- [`docs/security/THREAT-MODEL.md`](security/THREAT-MODEL.md) — Security threat model

## Guides

- [`docs/guides/integration-authoring-guide.md`](guides/integration-authoring-guide.md) — Integration lane authoring guide

## Reports

- [`docs/reports/`](reports/) — Project reports directory (audits, status summaries, evidence packs, and verification reports)
- [`docs/reports/2026-03-15-agent-discovery-and-machine-readable-entrypoints-report.md`](reports/2026-03-15-agent-discovery-and-machine-readable-entrypoints-report.md) — Discovery layer implementation across `universalmanifest.net` and `myum.net`
- [`docs/reports/2026-03-15-external-agent-onboarding-and-adoption-memo.md`](reports/2026-03-15-external-agent-onboarding-and-adoption-memo.md) — External-agent onboarding package and the internal adoption argument
- [`docs/reports/2026-03-15-agent-facing-publication-gates-framework.md`](reports/2026-03-15-agent-facing-publication-gates-framework.md) — Publication gates, anti-fabrication rules, and verification model for agent-facing surfaces
- [`docs/reports/2026-03-15-landing-first-public-experience-implementation-report.md`](reports/2026-03-15-landing-first-public-experience-implementation-report.md) — Landing-first `/` and curated `/docs/` implementation closeout
- [`docs/reports/2026-03-06-k2b-concept-integration-transfer-map.md`](reports/2026-03-06-k2b-concept-integration-transfer-map.md) — Consolidated map of how the recent concept-integration wave moved from research and blueprint into integration guidance, journeys, and proof
- [`docs/reports/2026-03-06-metaverse-portaling-integration-note.md`](reports/2026-03-06-metaverse-portaling-integration-note.md) — Clarifies portaling as the cross-platform movement model for the metaverse lane and shows where that concept landed in repo guidance
- [`docs/reports/2026-03-01-spec-vs-implementation-boundary-audit.md`](reports/2026-03-01-spec-vs-implementation-boundary-audit.md) — Spec vs implementation boundary audit
- [`docs/reports/2026-03-01-project-completeness-and-vision-audit.md`](reports/2026-03-01-project-completeness-and-vision-audit.md) — Project completeness and vision audit
- [`docs/reports/2026-03-01-documentation-freshness-audit.md`](reports/2026-03-01-documentation-freshness-audit.md) — Documentation freshness audit

## Integration lanes

- [`integrations/reference-runtime.md`](../integrations/reference-runtime.md) — Reference implementation integration contract (implementation-grade, non-normative)
- [`integrations/runtime-profile.md`](../integrations/runtime-profile.md) — Reference implementation conventions
- [`integrations/social.md`](../integrations/social.md) — Social/profile adoption notes (draft)
- [`integrations/metaverse.md`](../integrations/metaverse.md) — Metaverse integration lane with MUM lineage context
- [`integrations/rp1-spatial-fabric.md`](../integrations/rp1-spatial-fabric.md) — RP1 spatial-fabric integration lane
- [`integrations/smart-glasses.md`](../integrations/smart-glasses.md) — Smart-glasses social-layer integration lane
- [`integrations/oma-trust.md`](../integrations/oma-trust.md) — OMATrust integration lane
- [`integrations/proof-of-personhood.md`](../integrations/proof-of-personhood.md) — Proof-of-personhood multi-provider lane
- [`integrations/did-vc.md`](../integrations/did-vc.md) — DID + VC credential lane
- [`integrations/education-credentials.md`](../integrations/education-credentials.md) — Education credentials integration lane
- [`integrations/healthcare-patient-consent.md`](../integrations/healthcare-patient-consent.md) — Healthcare patient consent integration lane
- [`integrations/smart-home.md`](../integrations/smart-home.md) — Smart home integration lane
- [`integrations/data-firewall-ux.md`](../integrations/data-firewall-ux.md) — Firewall-style consent UX guidance
- [`integrations/TEMPLATE.md`](../integrations/TEMPLATE.md) — Integration lane template

## Agent-friendly public surface

- Public landing page: `https://universalmanifest.net/`
- Curated docs entry: `https://universalmanifest.net/docs/`
- Agent overview: `https://universalmanifest.net/for-agents/`
- External-agent onboarding: `https://universalmanifest.net/for-agents/external-agent-onboarding/`
- Discovery descriptor: `https://universalmanifest.net/.well-known/universal-manifest.json`
- llms.txt: `https://universalmanifest.net/llms.txt`
- Runtime descriptor: `https://myum.net/.well-known/myum-resolver.json`
- Runtime OpenAPI: `https://myum.net/openapi.json`

## Packages

- `packages/universal-manifest/` — TypeScript types + minimal runtime assertions for v0.1

## Spec versions

- [`spec/v0.1/README.md`](../spec/v0.1/README.md) — v0.1 draft overview
- [`spec/v0.1/CONFORMANCE.md`](../spec/v0.1/CONFORMANCE.md) — v0.1 conformance + fixtures
- [`spec/v0.2/SIGNATURE-PROFILE.md`](../spec/v0.2/SIGNATURE-PROFILE.md) — v0.2 signature direction (draft)
