# WO-0122 — Runtime Status Messaging Reconciliation

**Status:** IN_PROGRESS
**Created:** 2026-03-04
**Updated:** 2026-03-04
**Priority:** P2
**Owner:** Documentation + Platform
**Source:** Runtime truth audit/documentation drift follow-on

## Objective

Remove contradictory status messaging about whether this repository includes running services, while preserving the project’s spec-first positioning.

## Problem Statement

Several status/docs surfaces still frame the project as non-runtime-only, which conflicts with active production operations (`universalmanifest.net`, `myum.net`). This causes onboarding and handoff confusion.

## Scope

In scope:

- update state-of-project messaging to reflect active production surfaces
- update resolver README wording to distinguish minimal contract design from non-deployed status
- identify remaining stale phrasing for follow-on cleanup

Out of scope:

- changing architecture, contracts, or deployment topology

## Deliverables

1. Updated `STATE-OF-THE-PROJECT` top-line runtime statement.
2. Updated resolver README top-line deployment statement.
3. Follow-on list of additional docs needing wording harmonization.

## Acceptance Criteria

- [x] `docs/STATE-OF-THE-PROJECT.md` no longer states “not a running service”.
- [x] `services/myum-resolver/README.md` no longer claims non-production deployment.
- [ ] Remaining stale status language inventory documented in report.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/README.md`
