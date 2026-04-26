# WO-0229: CRITICAL-PATH and STATE-OF-THE-PROJECT Update — v0.2 Published, Queue Phase 19

**Status:** NOT_STARTED
**Priority:** P1
**Depends on:** WO-0220, WO-0221, WO-0222, WO-0223, WO-0224, WO-0225, WO-0226, WO-0227, WO-0228
**Unblocks:** WO-0230
**Derived from:** 2026-04-26 v0.2 publication push plan, item 10

## Objective

Update `docs/CRITICAL-PATH.md` and `docs/STATE-OF-THE-PROJECT.md` to reflect v0.2 as published. Close the publication wave (WO-0220 through WO-0228) in the canonical status chain. Queue the next phase (Phase 19 — what-comes-next; defined in WO-0230).

## Files to read first

- `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md`
- `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`
- All publication-wave result reports from WO-0220 through WO-0228 (`.dev/ai/subtask-comms/{date}-wo-022*-result.md`)

## Work to perform

1. **Update `docs/STATE-OF-THE-PROJECT.md`:**
   - Change the date stamp at the top.
   - Add a "v0.2 Published (2026-04-26)" subsection summarizing the publication-wave deliverables and citing the result-report paths.
   - Reconcile any "v0.2 draft" wording elsewhere in the file with the new published status.
2. **Update `docs/CRITICAL-PATH.md`:**
   - Mark the previous Phase 9 status block as "verified-clean prior to publication."
   - Add a new "Phase 19 — Post-publication adopter feedback and v0.3 input" section (or whatever the next phase number is per existing numbering — verify; the latest documented phase is 18). Stub the goals; deferred details to WO-0230.
   - Re-confirm the immediate rule list (calm public menu, /spec/latest/ remains obvious) holds with the new published surface.
3. **Update `docs/workorders/WO-INDEX.md`:**
   - Add a "v0.2 Publication Push Wave (WO-0220 through WO-0231)" section with all twelve WO IDs, statuses, and one-line summaries.

## Files to modify

- `docs/CRITICAL-PATH.md`
- `docs/STATE-OF-THE-PROJECT.md`
- `docs/workorders/WO-INDEX.md`

## Constraints

- **No re-opening of completed work.** This WO records facts; it does not re-litigate decisions.
- **Preserve existing wording tone.** Add, do not rewrite, per `WO-0209` precedent.
- **Phase 19 is a stub here.** Detailed queue belongs to WO-0230.

## Acceptance criteria

- `docs/STATE-OF-THE-PROJECT.md` declares v0.2 as published.
- `docs/CRITICAL-PATH.md` has a Phase 19 stub.
- `docs/workorders/WO-INDEX.md` has a v0.2 Publication Push Wave section listing all twelve WOs.
- A canonical reader arriving at `STATE-OF-THE-PROJECT.md` can trace the publication wave to its result reports in one click each.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0229-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0229-BLOCKED.md`
