# WO-0228: Synthetic-Monitoring SLO Re-check Against Published-Not-Draft Surface

**Status:** OBSOLETE 2026-04-28 — depended on the WO-0215 expanded synthetic monitoring (reverted in commit `e493b3e`). The synthetic-monitoring workflow is back to its budget-zero state. Re-scope a fresh WO if the user later re-enables monitoring against the published surface.
**Priority:** P1
**Depends on:** WO-0222
**Unblocks:** none
**Derived from:** 2026-04-26 v0.2 publication push plan, item 9; WO-0117 (synthetic monitoring + SLO policy)

## Objective

Re-read the SLO policy WO-0117 set up against the new published surface. Confirm that thresholds, alert conditions, and route lists still match the post-publication URL set. Add `/spec/v0.2/` to the monitored route list if it is not already present.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0117-add-synthetic-monitoring-alerting-and-slo-policy.md`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/synthetic-monitoring.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/synthetic-monitoring-staging.yml`
- `/Users/grig/work/repo/universalmanifest/docs/governance/ADOPTER-SLA.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/RELEASE-CADENCE.md`

## Work to perform

1. **Read the WO-0117 SLO policy** and list its current monitored routes and threshold targets. Capture in the result report.
2. **Diff against the new published URL set** from WO-0221 / WO-0222 / WO-0223 / WO-0224 / WO-0225:
   - `/spec/v0.2/` (new durable URL)
   - `/conformance/v0.2/` (already monitored?)
   - `/governance/breaking-change-policy/` (already monitored?)
   - `https://universalmanifest.net/ns/universal-manifest/v0.2/schema.json{,ld}` (already monitored?)
3. **Add missing routes** to the synthetic-monitoring config.
4. **Adjust thresholds** if the published surface materially changes performance characteristics (e.g., a heavier spec page). Default: keep thresholds as-is unless evidence shows drift.
5. **Document the re-check** in a new section of `docs/governance/ADOPTER-SLA.md` (or as a subtask-comm if ADOPTER-SLA doesn't track this).

## Files to modify

- `.github/workflows/synthetic-monitoring.yml`
- `.github/workflows/synthetic-monitoring-staging.yml`
- `docs/governance/ADOPTER-SLA.md` (only if it specifies monitored routes; otherwise document elsewhere)

## Constraints

- **Do not loosen thresholds** to make the publication "look green" — if a threshold needs loosening, that is a separate WO with explicit governance rationale.
- **Do not touch alerting credentials** — those are operator-owned outside the agent boundary.
- The monitored route list MUST include the durable `/spec/v0.2/` URL after this WO.

## Acceptance criteria

- All new published-surface routes are in the synthetic-monitoring route list.
- The result report includes a before/after table of monitored routes and thresholds.
- No threshold was loosened without an explicit rationale.
- `actionlint` (if available) passes on the modified workflow files.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0228-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0228-BLOCKED.md`
