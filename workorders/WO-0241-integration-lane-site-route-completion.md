# WO-0241: Integration Lane Site Route Completion

**Status:** COMPLETED 2026-04-29
**Priority:** MEDIUM (P2)
**Depends on:** WO-0219
**Unblocks:** Cleaner integration catalog status for runtime-profile and data-firewall-ux lanes
**Derived from:** WO-0219 residual risk report

## Objective

Publish dedicated site documentation routes for the integration lanes that currently have source lane docs and fixtures but no dedicated public integration route:

- `runtime-profile`
- `data-firewall-ux`

The goal is to make the integration catalog internally consistent: every lane listed as source-backed should have a published route unless it is intentionally source-only.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-28-23-54-48Z-T4-wo-0219-result.md`
- `/Users/grig/work/repo/universalmanifest/integrations/runtime-profile.md`
- `/Users/grig/work/repo/universalmanifest/integrations/data-firewall-ux.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/index.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/reference-runtime.md`

## Work to perform

1. Create or update Starlight content pages for:
   - `/integrations/runtime-profile/`
   - `/integrations/data-firewall-ux/`
2. Preserve the non-normative/source-of-truth boundary: the repo-root `integrations/*.md` files remain the source lane docs.
3. Add clear links back to the source lane docs, fixture directories, and relevant journeys/reference implementation patterns.
4. Update the integration catalog at `site/src/content/docs/integrations/index.md` so these two lanes point at their public routes.
5. Only mark a lane `Published` if the route, fixtures, and journey/reference pointers are all present and accurate; otherwise leave it `In Progress` with a precise reason.

## Files to modify

- `site/src/content/docs/integrations/runtime-profile.md`
- `site/src/content/docs/integrations/data-firewall-ux.md`
- `site/src/content/docs/integrations/index.md`

## Constraints

- Do not change normative spec text.
- Do not add top-level navigation.
- Do not create or modify CI workflows, schedules, releases, tags, commits, or deployment infrastructure.
- Do not rewrite the source lane docs unless a link is demonstrably broken.

## Acceptance criteria

- Public content pages exist for both lanes.
- The integrations catalog links to public routes rather than GitHub source URLs for both lanes.
- The pages link to the relevant fixture directories and journey/reference implementation coverage.
- `npm run build` passes from `/Users/grig/work/repo/universalmanifest/site`.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0241-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0241-BLOCKED.md`
