# WO-0034 — Documentation status coherence and stale-reference reconciliation

**Status:** NOT_STARTED
**Created:** 2026-02-22
**Priority:** HIGH
**Source:** `/Users/grig/work/repo/universalmanifest/.dev/ai/LOOSE-ENDS-REVIEW-2026-02-22.md`

## Objective

Reconcile documentation/status drift introduced after rapid WO closure so project state claims, work-order evidence paths, and historical status reports are internally consistent.

## Why this work matters

Current docs contain contradictory status statements that can mislead operators and external adopters:

- `PROJECT-RULES.md` still states production deployment is blocked by `WO-0003`.
- `WO-0014` completion evidence references a missing filesystem path.
- `docs/reports/2026-02-20-master-forward-worklist.md` declares itself a single source for remaining work but is now historical.

## Scope

In scope:

- Update stale blocker language in `/Users/grig/work/repo/universalmanifest/PROJECT-RULES.md`.
- Correct stale/missing evidence path(s) in `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0014-interactive-manifest-workbench.md`.
- Add clear superseded/historical marker in `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-20-master-forward-worklist.md` pointing to canonical current-state docs.
- Add explicit note in current-state guidance that prior handoff/audit priority sections are time-scoped snapshots unless revalidated.
- Keep state docs and rule docs semantically aligned on current completion posture.

Out of scope:

- Deciding human-reader evidence policy for `WO-0015` (tracked by `WO-0035`).
- Net-new feature implementation or runtime behavior changes.

## Required deliverables

1. Reconciled status language in:
   - `/Users/grig/work/repo/universalmanifest/PROJECT-RULES.md`
2. Corrected completion evidence path references in:
   - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0014-interactive-manifest-workbench.md`
3. Historical/superseded marker in:
   - `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-20-master-forward-worklist.md`
4. Brief reconciliation note in:
   - `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
   - or an adjacent dated report under `/Users/grig/work/repo/universalmanifest/docs/reports/`

## Acceptance criteria

- [ ] `PROJECT-RULES.md` no longer claims `WO-0003` is an active blocker.
- [ ] `WO-0014` does not reference nonexistent workbench path(s).
- [ ] Historical forward-worklist doc clearly indicates it is a dated snapshot and not current source of truth.
- [ ] Current-state guidance explicitly treats old handoff/audit priority sections as historical snapshots unless revalidated.
- [ ] Reconciled docs contain no contradictory deployment-status claims for the current project snapshot.
- [ ] Site docs build still passes after edits.

## Validation commands

- `rg -n 'WO-0003|production publishing pending|blocked on external infra actions' /Users/grig/work/repo/universalmanifest/PROJECT-RULES.md`
- `rg -n 'site/public/getting-started/workbench/' /Users/grig/work/repo/universalmanifest/docs/workorders/WO-0014-interactive-manifest-workbench.md`
- `rg -n 'single source list of all remaining known work|superseded|historical snapshot' /Users/grig/work/repo/universalmanifest/docs/reports/2026-02-20-master-forward-worklist.md`
- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`

## Dependencies

- `WO-0035` for final wording convergence where onboarding evidence policy language intersects.
