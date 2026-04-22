# WO-0188 -- Compatibility Surface Retirement Readiness

**Status:** COMPLETED
**Priority:** P2
**Created:** 2026-04-13

## Objective

Define and verify the exit criteria for retiring compatibility-only surfaces such as legacy deploy layers and alias routes once they are no longer needed.

## Context

Several compatibility layers remain appropriate today, but the project needs a clear readiness test for when they can be retired without breaking published use.

## Scope

In scope:

1. Define retirement readiness criteria for alias-only routes and compatibility deploy layers.
2. Identify required evidence before retirement.
3. Document a safe retirement sequence.

Out of scope:

- immediate removal of compatibility surfaces
- breaking backward compatibility without evidence

## Deliverables

- Retirement-readiness matrix.
- Compatibility exit criteria for legacy layers such as `deploy/localartist.network/` and alias-only routes.

## Dependencies

- WO-0183 canonical route and compatibility alias policy.
- Outputs of WO-0184 through WO-0187, because retirement readiness depends on the post-alignment shell strategy, the `/spec/latest/` long-term model, fixture-mirror policy, and asset continuity decisions.

## Acceptance Criteria

- [x] Compatibility-only surfaces have documented exit criteria.
- [x] Retirement sequencing is explicit.
- [x] The project can retire legacy surfaces deliberately rather than indefinitely.

## Completion Notes

- Retirement-readiness criteria are now documented in `docs/reports/2026-04-22-compatibility-surface-retirement-readiness.md`.
- The readiness matrix distinguishes redirect-only compatibility surfaces, keep-for-now compatibility infrastructure, and later retire candidates.
- The explicit retirement sequence now starts with low-risk alias-only routes, defers asset alias cleanup until later, and leaves `deploy/localartist.network/` as the highest-risk and latest retirement candidate.
