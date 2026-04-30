# WO-0230: Phase 19 — What-Comes-Next Definition

**Status:** COMPLETED 2026-04-30
**Priority:** P2 (planning; runs after publication closes)
**Depends on:** WO-0229
**Unblocks:** none directly; produces the next planning baseline.
**Derived from:** 2026-04-26 v0.2 publication push plan, item 10; WO-0214 (post-publication external reader validation, deferred)

## Objective

Define the Phase 19 work plan: what does the project do after v0.2 is published. Convert the deferred items from the publication scan and the existing future-roadmap signals into a concrete WO queue.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md` (Phase 19 stub from WO-0229)
- `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0214-post-publication-external-human-reader-validation.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-v0-2-publication-readiness-scan.md` (deferral list)
- `/Users/grig/work/repo/universalmanifest/docs/governance/SPEC-IMPROVEMENT-QUEUE.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md` §8 (deferred profiles)

## Work to perform

1. **Catalog the deferred items** from the publication-readiness scan (items 1–7 of the "Intentional Deferrals Properly Surfaced" list). Each is now eligible for promotion or a permanent-deferral decision.
2. **Author Phase 19 goals:**
   - external human reader validation (WO-0214 promotion)
   - adopter-feedback loop activation (WO-0056 promotion)
   - tier 2 / tier 3 identity-binding research (research-first decision package)
   - Data Integrity / RDF profile decision package
   - revocation-as-normative decision package (was optional in v0.2)
3. **Sketch follow-on WO IDs** starting at the next available non-conflicting ID. The original instruction said to start at WO-0232, but `WO-0232` through `WO-0242` already exist in the repository. Provide title, priority, and one-line objective for each. Do not draft full WOs — this is a queue definition, not the WOs themselves.
   - Completion note: the Phase 19 queue uses `WO-0243` through `WO-0251`.
4. **Update `docs/CRITICAL-PATH.md`** Phase 19 stub with the goal list and follow-on WO IDs.

## Files to modify

- `docs/CRITICAL-PATH.md` (expand the Phase 19 stub from WO-0229)
- `docs/governance/SPEC-IMPROVEMENT-QUEUE.md` (cross-link Phase 19 items)

## Constraints

- **No new WO drafts beyond the queue definition.** Full drafts come later under their own WOs.
- **Respect existing deferral decisions.** Items explicitly deferred in the publication scan stay deferred unless this WO promotes them with rationale.

## Acceptance criteria

- `docs/CRITICAL-PATH.md` Phase 19 has a list of named goals.
- Each goal has a stub WO ID (`WO-0243+`, reconciled against existing `WO-0232` through `WO-0242`) with title, priority, and one-line objective.
- `SPEC-IMPROVEMENT-QUEUE.md` references Phase 19.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0230-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0230-BLOCKED.md`
