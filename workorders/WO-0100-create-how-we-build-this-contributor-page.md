# WO-0100 — Create Contributor-Facing "How We Build This" Page

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P1 (Important)
**Source:** Project Completeness and Vision Audit (2026-03-01), Gap 25, Recommended Action P1-11
**Tags:** [site], [docs]
**Blocks:** Contributor onboarding and methodology transparency
**Dependencies:** None
**Estimated effort:** 2-3 hours

## Objective

Create a "How We Build This" page on the site that explains the journey-driven proof model, the done-done framework, and the work-order discipline to potential contributors.

## Why this work matters

The completeness audit found that the development methodology (done-done framework, journey-driven proof, work-order system) is documented to an exceptional degree but is not explained anywhere on the public site. A potential contributor would not discover these systems unless they browse the governance section of the repo. Making the methodology visible demonstrates the project's rigor and helps contributors understand how to participate effectively.

## Scope

### New site page

**`site/src/content/docs/governance/how-we-build.md`** (or `governance/methodology.md`)

### Content to cover

1. **Journey-driven proof model** — What journeys are, why "docs exist" is not proof, the journey system (J01-J11)
2. **Done-done framework** — Maturity targets (A, B, C), seven acceptance gates (G1-G7), evidence requirements
3. **Work order system** — How work is scoped, tracked, and verified
4. **Critical path** — How phases and milestones are organized
5. **How to contribute** — Link to CONTRIBUTING.md, explain the WO-driven workflow

### Source content

- `docs/DONE-DONE-DEFINITION.md`
- `docs/journeys/README.md`
- `docs/CRITICAL-PATH.md`
- `CONTRIBUTING.md`

### Sidebar integration

Add to the "Governance" section of the site sidebar.

## Acceptance criteria

- [ ] "How We Build This" page exists on the site.
- [ ] All three key methodology components (journeys, done-done, work orders) are explained.
- [ ] A potential contributor can understand how to participate after reading this page.
- [ ] `cd site && npm run build:clean` succeeds.

## Validation commands

- `cd site && npm run build:clean`
- Manual review of content completeness.
