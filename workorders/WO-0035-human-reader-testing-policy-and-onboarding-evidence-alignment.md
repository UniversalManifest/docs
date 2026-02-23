# WO-0035 — Human-reader testing policy and onboarding evidence alignment

**Status:** BLOCKED
**Created:** 2026-02-22
**Priority:** HIGH
**Source:** `/Users/grig/work/repo/universalmanifest/.dev/ai/LOOSE-ENDS-REVIEW-2026-02-22.md`

## Objective

Resolve contradictory onboarding-evidence policy statements by deciding whether human participant testing is mandatory for `WO-0015` closure, then align all related documents to one canonical policy.

## Why this work matters

Current documents conflict:

- `WO-0015` is marked completed but still contains pending external-reader closure language.
- The first-time reader protocol says external participant evidence is still required.
- `STATE-OF-THE-PROJECT` says human testing is recommended, not required.

This creates ambiguity in completion claims and onboarding-readiness messaging.

## Decision gate (blocking)

A user decision is required before implementation:

1. Policy A: Human participant evidence is mandatory for closure-grade completion.
2. Policy B: CLI-agent evidence is sufficient for current maturity; human participant evidence is recommended follow-up.

## Scope

In scope:

- Record chosen policy in `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`.
- Normalize wording and status implications across:
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md`
  - `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-19-first-time-reader-testing-protocol.md`
  - `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
- Remove placeholder artifact naming (`2026-02-XX-...`) from active guidance.

Conditional scope (if Policy A selected):

- Execute human-participant run and create a dated results artifact under:
  - `/Users/grig/work/repo/universalmanifest/docs/reports/`

Out of scope:

- Broader docs status drift cleanup not specific to onboarding evidence policy (`WO-0034`).

## Required deliverables

1. Policy record in:
   - `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
2. Aligned wording updates in the three core files listed above.
3. If policy requires human evidence, a dated results report in:
   - `/Users/grig/work/repo/universalmanifest/docs/reports/`

## Acceptance criteria

- [ ] One explicit policy statement exists and is traceable in `docs/DECISIONS.md`.
- [ ] `WO-0015`, protocol, and state docs no longer contradict each other on required evidence.
- [ ] Placeholder `2026-02-XX-first-time-reader-test-results.md` is removed from active instructions.
- [ ] If policy is mandatory-human, at least one dated human-participant report exists.

## Validation commands

- `rg -n 'human participant|recommended|required|pending|2026-02-XX-first-time-reader-test-results' /Users/grig/work/repo/universalmanifest/docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md /Users/grig/work/repo/universalmanifest/docs/reports/2026-02-19-first-time-reader-testing-protocol.md /Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
- `rg -n 'WO-0015|reader testing|human participant|CLI-agent evidence' /Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`

## Blocker

- User policy selection required (Policy A vs Policy B).

