# WO-0219: Cross-Domain Integration Lane Reference Consolidation

**Status:** NOT_STARTED
**Priority:** MEDIUM (P2)
**Depends on:** WO-0216 (fixtures must exist before they can be cross-linked from lane docs)
**Unblocks:** —
**Derived from:** 2026-04-26 resolver runtime drift scan, finding 7 (INFO) + adjacent integration-lane drift signals

## Objective

Each `integrations/{lane}.md` file is currently freestanding. Adopters reading one have no easy path to the matching fixtures, journey IDs, or reference TypeScript patterns. Standardize an "Implementation notes" cross-reference block across all lane docs so a reader navigating from any lane immediately sees: where the fixtures live, which journey exercises the lane, and which `um-typescript` patterns apply.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/integrations/` (all `*.md`)
- `/Users/grig/work/repo/universalmanifest/integrations/TEMPLATE.md` (if present; otherwise create one)
- `/Users/grig/work/repo/universalmanifest/examples/integrations/` (post-WO-0216 fixture baseline)
- `/Users/grig/work/repo/universalmanifest/docs/journeys/` (journey IDs per lane)
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0213-integration-lane-cross-reference-freshness-sweep.md` (companion)

## Work to perform

1. Update or create `integrations/TEMPLATE.md` with a standard "Implementation notes" section listing fixtures, journeys, and reference-impl patterns.
2. Apply the section to every `integrations/{lane}.md` post-WO-0216 (so the fixture links resolve).
3. Add a discovery page (or update an existing one) listing all 15 lanes with status badges: Published / In Progress / Planned.
4. Cross-check each lane doc against `WO-0213`'s freshness output to avoid re-introducing stale dates.

## Files to modify / create

- `integrations/TEMPLATE.md`
- All `integrations/{lane}.md` files
- A discovery page somewhere obvious (likely `site/src/pages/integrations/index.astro` or `docs/INTEGRATIONS.md`)

## Constraints

- Wait for WO-0216 fixtures to land. Cross-linking to non-existent fixtures is worse than no cross-link.
- Date hygiene: do not re-introduce stale dates fixed by WO-0213.
- Do not commit, push, stage, or branch.
- Run `git status --short` first; respect sibling commit agent's diff.

## Acceptance criteria

- Every lane doc has an "Implementation notes" block with fixture / journey / reference-impl pointers.
- Discovery page lists all 15 lanes with status.
- TEMPLATE.md exists and is the source of truth for new lane docs.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0219-result.md`
Blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0219-BLOCKED.md`
