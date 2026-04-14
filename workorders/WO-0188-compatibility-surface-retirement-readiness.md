# WO-0188 -- Compatibility Surface Retirement Readiness

**Status:** PLANNED
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

## Acceptance Criteria

- [ ] Compatibility-only surfaces have documented exit criteria.
- [ ] Retirement sequencing is explicit.
- [ ] The project can retire legacy surfaces deliberately rather than indefinitely.
