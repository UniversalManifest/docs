# WO-0183 -- Canonical Route and Compatibility Alias Policy

**Status:** COMPLETED
**Priority:** P1
**Created:** 2026-04-13
**Completed:** 2026-04-13

## Objective

Convert the post-map route-classification decisions into an explicit canonical-versus-alias-versus-retirement policy for public routes so future site work stops accumulating path ambiguity.

## Context

The project now has a calm front door and a documented surface map, but several public paths still exist as compatibility shims, legacy redirects, or parallel entry points. Before more surface unification work happens, the path policy itself needs to be authoritative.

## Scope

In scope:

1. Define canonical public routes by surface family.
2. Define which routes are compatibility aliases only.
3. Define which routes are retirement candidates and the conditions for retirement.
4. Update project docs so the route policy is explicit.

Out of scope:

- redesigning tool internals
- changing normative spec artifacts
- removing compatibility routes before policy and evidence exist

## Deliverables

- Canonical route policy document and matrix.
- Alias/redirect policy for legacy public paths.
- Updated docs and deploy guidance reflecting the canonical route set.

## Completion Notes

- Added the canonical policy document at `docs/CANONICAL-ROUTE-AND-COMPATIBILITY-ALIAS-POLICY.md`.
- Classified the current public route model into canonical routes, compatibility aliases, and retirement candidates.
- Wired the route policy into:
  - `docs/DOMAIN-ARCHITECTURE.md`
  - `docs/COMPREHENSIVE-PROJECT-PROPERTIES-AND-SURFACES-MAP.md`
  - `docs/README.md`
  - `docs/PROJECT-KNOWLEDGE-INDEX.md`
  - `deploy/universalmanifest.net/README.md`
  - `deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`
- Recorded the closeout in `docs/reports/2026-04-13-canonical-route-and-compatibility-alias-policy.md`.

## Dependencies

- WO-0180 classified the current route families.
- WO-0182 defined the initial keep/merge/alias/retire package.

## Acceptance Criteria

- [x] Canonical routes are explicitly documented.
- [x] Compatibility-only routes are explicitly documented.
- [x] Retirement candidates have documented exit criteria.
- [x] Future site work can reference one authoritative route policy.
