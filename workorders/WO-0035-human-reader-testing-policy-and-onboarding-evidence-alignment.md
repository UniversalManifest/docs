# WO-0035 — Human-reader testing policy and onboarding evidence alignment

**Status:** COMPLETED
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

## Decision gate

Decision resolved (2026-02-23):

1. Mandatory human-participant evidence removed as a closure gate.
2. Human-reader runs remain optional quality validation.

## Scope

In scope:

- Record chosen policy in `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`.
- Normalize wording and status implications across:
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md`
  - `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-19-first-time-reader-testing-protocol.md`
  - `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
- Remove placeholder artifact naming (`2026-02-XX-...`) from active guidance.

Optional scope:

- Execute human-participant run and create a dated results artifact under:
  - `/Users/grig/work/repo/universalmanifest/docs/reports/`

Out of scope:

- Broader docs status drift cleanup not specific to onboarding evidence policy (`WO-0034`).

## Required deliverables

1. Policy record in:
   - `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
2. Aligned wording updates in the three core files listed above.
3. Optional dated results report in:
   - `/Users/grig/work/repo/universalmanifest/docs/reports/`
4. Human gate checklist artifact defining expected observations/questions:
   - `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-22-first-time-reader-human-gate-checklist.md`

## Acceptance criteria

- [x] One explicit policy statement exists and is traceable in `docs/DECISIONS.md`.
- [x] `WO-0015`, protocol, and state docs no longer contradict each other on required evidence.
- [x] Placeholder `2026-02-XX-first-time-reader-test-results.md` is removed from active instructions.
- [x] Policy and status documents are aligned so onboarding closure is not blocked by human-participant evidence.

## Validation commands

- `rg -n 'human participant|recommended|required|pending|2026-02-XX-first-time-reader-test-results' /Users/grig/work/repo/universalmanifest/docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md /Users/grig/work/repo/universalmanifest/docs/reports/2026-02-19-first-time-reader-testing-protocol.md /Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
- `rg -n 'WO-0015|reader testing|human participant|CLI-agent evidence' /Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`

## Blocker

- None.

## Progress evidence (2026-02-22)

- Policy-alignment report:
  - `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-22-wo-0035-policy-a-gate-alignment-report.md`
- Human gate checklist:
  - `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-22-first-time-reader-human-gate-checklist.md`

## Completion evidence (2026-02-23)

- Onboarding pages rewritten (WO-0039 Phases 1-4 complete):
  - Landing page: `/Users/grig/work/repo/universalmanifest/site/src/content/docs/index.md`
  - Overview: `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/universal-manifest-overview.md`
  - Concepts: `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/concepts.md`
  - Quick Start: `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/quick-start.md`
- Human reader test evidence template created:
  - Template: `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-23-first-time-reader-test-results-human.md`
- Pages live and ready for human review at `http://127.0.0.1:4300/`
- Policy update recorded in:
  - `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
- Work-order and status docs updated to remove human-evidence blocking semantics.
