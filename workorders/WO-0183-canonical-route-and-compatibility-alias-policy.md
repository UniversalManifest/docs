# WO-0183 -- Canonical Route and Compatibility Alias Policy

**Status:** ACTIVE
**Priority:** P1
**Created:** 2026-04-13

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

## Dependencies

- WO-0180 classified the current route families.
- WO-0182 defined the initial keep/merge/alias/retire package.

## Acceptance Criteria

- [ ] Canonical routes are explicitly documented.
- [ ] Compatibility-only routes are explicitly documented.
- [ ] Retirement candidates have documented exit criteria.
- [ ] Future site work can reference one authoritative route policy.
