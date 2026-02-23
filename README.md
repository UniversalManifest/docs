# Universal Manifest — Documentation Index

This is the entry point for the Universal Manifest spec repo.

Canonical repo path: `/Users/grig/work/repo/universalmanifest`

## Repo map

- `spec/` — Versioned spec artifacts (JSON-LD context, schemas, normative text)
- `examples/` — Example manifests (valid + invalid fixtures as the spec stabilizes)
- `integrations/` — Practical guidance for consuming/producing manifests across adopter surfaces
- `research/` — Imported background docs and synthesis from supporting design libraries
- `packages/` — Reusable code (types/validators) for producers/consumers (added later)
- `docs/workorders/` — Work orders for scoped project tasks

## Key docs

- `docs/PROJECT-VISION.md` — What this standard aims to enable (and what’s out of scope)
- `docs/DEPTH-AND-SCOPE.md` — High-level depth + scope map for this repo
- `docs/STATE-OF-THE-PROJECT.md` — Current status, milestones, and next steps
- `docs/reports/2026-02-18-live-status-and-next-critical-path.md` — Current live deployment status + next critical path
- `docs/CRITICAL-PATH.md` — Minimal sequence for adoption + publishing + “world-ready” claims
- `docs/DOMAIN-ARCHITECTURE.md` — Domain split: standards site vs UMID resolver
- `docs/PUBLISHING-AND-VERSIONING.md` — How spec artifacts get hosted + versioned for adopters
- `docs/RELEASING.md` — Draft release process for spec versions + publishing
- `docs/DEPLOY-CHECKLIST.md` — One linear checklist for first real deploy (`universalmanifest.net` + `myum.net`)
- `docs/CRUCIAL-DETAILS.md` — Non-obvious decisions and “gotchas”
- `docs/DECISIONS.md` — Decisions made while drafting the standard
- `docs/PROJECT-KNOWLEDGE-INDEX.md` — Pointer to GAS shared Universal Manifest master index
- `docs/DONE-DONE-DEFINITION.md` — Official completion criteria (“done done”) for releases
- `docs/DONE-DONE-CHECKLIST.md` — Gate-by-gate checklist for release readiness
- `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md` — Required evidence template for done-done sign-off
- `docs/TS-HELPER-PACKAGE.md` — What the TS helper is, how it’s used, distribution policy
- `docs/journeys/README.md` — Canonical user journeys mapped to an executable proof suite
- `docs/diagrams/README.md` — Diagram source + export workflow (Excalidraw → SVG)
- `docs/STUB-MANIFESTS.md` — Near-real example manifests (fixtures) + section drivers
- `docs/WORKLOG-2026-02-11.md` — Initial repo bootstrap worklog
- `docs/WORKLOG-2026-02-12.md` — Stub fixtures + validation worklog
- `docs/AGENT-OBSERVED-GAPS.md` — Append-only list of missing/unclear items
- `PROJECT-RULES.md` — Project-specific onboarding and operational rules (with global GAS `AGENTS.md`)
- `integrations/reference-runtime.md` — Reference implementation integration contract (implementation-grade, non-normative)
- `integrations/runtime-profile.md` — reference implementation conventions
- `integrations/social.md` — Social/profile adoption notes (draft)
- `integrations/metaverse.md` — Metaverse integration lane with MUM lineage context
- `integrations/rp1-spatial-fabric.md` — RP1 spatial-fabric integration lane (Stage -1/0 source intake complete)
- `integrations/smart-glasses-ar.md` — Smart-glasses AR social-layer integration lane
- `docs/workorders/WO-0014-interactive-manifest-workbench.md` — CEO-priority interactive manifest workbench
- `docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md` — CEO-priority first-time overview + visual onboarding
- `docs/workorders/WO-0018-mum-lineage-and-emerging-integration-codification.md` — CEO-priority lineage + metaverse/RP1/smart-glasses integration codification

## Packages

- `packages/universal-manifest/` — TypeScript types + minimal runtime assertions for v0.1

## Spec versions

- `spec/v0.1/README.md` — v0.1 draft overview
- `spec/v0.1/CONFORMANCE.md` — v0.1 conformance + fixtures
- `spec/v0.2/SIGNATURE-PROFILE.md` — v0.2 signature direction (draft)
