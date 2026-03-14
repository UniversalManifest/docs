# WO-0103 — Update docs/README.md with All Missing Document References

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P0 (Critical)
**Source:** Documentation Freshness Audit (2026-03-01), Section 4, Section 5.7, Priority 2 recommendation
**Tags:** [docs]
**Blocks:** Documentation discoverability — newcomers cannot find 20+ new documents
**Dependencies:** None
**Estimated effort:** 2-3 hours

## Objective

Update `docs/README.md` to reference all new documents, directories, and file categories created during the 2026-02-22 through 2026-03-01 period. Currently approximately 20 categories of new content are not indexed.

## Why this work matters

The freshness audit found that `docs/README.md` is significantly stale — it has not been updated to reference approximately 20 new document categories created this week. The only report referenced is from 2026-02-18. A newcomer reading `docs/README.md` would have no awareness of the majority of the project's documentation.

## Scope

### File to modify

**`docs/README.md`**

### New references to add

**Documents:**
- `docs/UNIVERSAL-MANIFEST-BRIEFING.md` — Full AI agent briefing
- `docs/MANDATE-interactive-implementation-sandbox.md` — CEO mandate for sandbox
- `docs/teaching-scripts/` — Teaching scripts system (README, iconic representation, format, ideas)
- `docs/explainers/` — Explainer documents (paragraph, one-pager, full briefing, agent briefing, animation briefing)
- `docs/scripts/` — Animation scripts (what-is-um, how-it-works, why-it-matters, day-in-the-life)
- `docs/guides/integration-authoring-guide.md` — Integration lane authoring guide
- `docs/journeys/commercial/` — Commercial journeys (creator, venue operator, app developer, privacy, enterprise)
- `docs/governance/` — Governance framework files (GOVERNANCE.md, branch protection, contributing registry, maintainers, RFC template)
- `docs/security/THREAT-MODEL.md` — Security threat model
- `docs/design/ANIMATED-SVG-WORKFLOW.md` — Animated SVG production workflow
- `docs/design/ANIMATED-SVG-SPEC.md` — Animated SVG specification
- `docs/design/ANIMATION-PLACEMENT-PLAN.md` — Animation placement plan
- `docs/design/ANIMATION-QA-CHECKLIST.md` — Animation QA checklist
- `docs/design/SVG-INFOGRAPHIC-STYLE-GUIDE.md` — SVG infographic style guide
- `docs/design/INFOGRAPHIC-STYLES-INVENTORY.md` — Complete infographic styles inventory
- `docs/design/CAPSULE-POD-DESIGN.md` — Capsule-Pod design spec
- `docs/design/PERMISSIONS-FIREWALL-DESIGN.md` — Permissions firewall design
- `docs/ENVELOPE-TOPOLOGY.md` — Already indexed (verify)

**Integration lanes (not in README.md):**
- `integrations/TEMPLATE.md`
- `integrations/oma-trust.md`
- `integrations/proof-of-personhood.md`
- `integrations/chia-vc.md`
- `integrations/education-credentials.md`
- `integrations/healthcare-patient-consent.md`
- `integrations/smart-home.md`

**Code and tooling:**
- `examples/code/` — 10+ runnable code examples
- `examples/demo-app/` — Full demo application

**Foundation files:**
- `CODE_OF_CONDUCT.md`
- `CONTRIBUTING.md`
- `LICENSE`
- `SECURITY.md`

**Reports directory:**
- Add a mention of `docs/reports/` directory and at minimum reference the most relevant recent reports (update from the single 2026-02-18 report reference).

## Acceptance criteria

- [ ] All 20+ new document categories listed above are referenced in docs/README.md.
- [ ] The reports section references the `docs/reports/` directory rather than a single outdated report.
- [ ] Foundation files (CODE_OF_CONDUCT, CONTRIBUTING, LICENSE, SECURITY) are mentioned.
- [ ] New integration lanes are referenced.
- [ ] Code examples directory is referenced.
- [ ] A newcomer reading docs/README.md would discover all major documentation areas.

## Validation commands

- Manual comparison of docs/README.md references against actual file inventory.
- `ls docs/` to verify all top-level docs are referenced.
