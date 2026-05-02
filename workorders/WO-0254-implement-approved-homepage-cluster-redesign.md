# WO-0254: Implement Approved Homepage Cluster Redesign

**Status:** COMPLETED 2026-05-02
**Priority:** P0 (blocks production verification and reader validation)
**Depends on:** WO-0253
**Unblocks:** WO-0255
**Derived from:** 2026-05-02 objective realignment

## Problem

The site implementation must reflect an approved homepage-cluster design before external-reader validation can produce meaningful evidence.

The current homepage implementation from `WO-0252` is superseded as final direction. Implementing more changes without the `WO-0253` design report risks repeating the same drift: visible page churn without a coherent public experience.

## Objective

Implement the approved homepage-cluster redesign across the public entry routes:

- `/`
- `/use-cases/`
- `/explorer/`
- `/how-it-works/`
- `/standards-fit/`

## Files to read first

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0253-homepage-cluster-design-direction-package.md`
- The delivered `WO-0253` design report under `/Users/grig/work/repo/universalmanifest/.dev/ai/designs/`
- `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md`
- `/Users/grig/work/repo/universalmanifest/docs/HOME-CLUSTER-SITEMAP.md`
- `/Users/grig/work/repo/universalmanifest/docs/HOME-CLUSTER-COPY-BRIEFS.md`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/use-cases/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/explorer/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/how-it-works/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/standards-fit/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/styles/public-surface.css`

## Work to perform

1. Translate the approved design report into Astro/CSS changes across the five-page homepage cluster.
2. Preserve the global navigation as `Home` and `Latest Spec`.
3. Preserve required v0.2 reader paths:
   - `/spec/latest/`
   - `/spec/v0.2/`
   - `/guides/migration-v01-v02/`
   - `/publishing/changelog/`
4. Remove or rewrite any visible copy that still reads like internal project-management language.
5. Ensure the homepage hero communicates what Universal Manifest is above the fold on desktop and mobile.
6. Keep the five pages distinct; do not let them repeat the same explanation.
7. Run build and visual verification.

## Files expected to modify

- `/Users/grig/work/repo/universalmanifest/site/src/pages/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/use-cases/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/explorer/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/how-it-works/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/standards-fit/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/styles/public-surface.css`
- Optional shared content/data files only if required by the approved design.

## Constraints

- Do not change normative spec content.
- Do not widen the top-level public nav.
- Do not implement a design direction that has not been approved or accepted.
- Do not remove published v0.2 paths.
- Do not add decorative visual noise as a substitute for a clear visual model.

## Acceptance criteria

- `npm run build` passes from `/Users/grig/work/repo/universalmanifest/site`.
- Desktop and mobile visual verification shows the new hero and page structure rendered correctly.
- Console check shows no errors introduced by the redesign.
- The homepage answers what Universal Manifest is, what it carries, why it matters, and where to go next from the first screen.
- All five homepage-cluster pages have distinct roles and no wall-of-paragraphs first impression.
- Required v0.2 routes remain linked and reachable locally.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0254-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0254-BLOCKED.md`

## Closeout Evidence

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-05-02-wo-0254-result.md`

Implementation completed across the approved homepage cluster:

- `/Users/grig/work/repo/universalmanifest/site/src/pages/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/use-cases/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/explorer/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/how-it-works/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/standards-fit/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/data/home-cluster.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/styles/public-surface.css`
- `/Users/grig/work/repo/universalmanifest/site/src/components/ui/SiteHeader.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/components/ui/SiteFooter.astro`

Verification completed:

- `npm run build` passed from `/Users/grig/work/repo/universalmanifest/site`.
- Local preview route checks returned HTTP 200 for `/`, `/use-cases/`, `/explorer/`, `/how-it-works/`, `/standards-fit/`, `/spec/latest/`, `/spec/v0.2/`, `/guides/migration-v01-v02/`, and `/publishing/changelog/`.
- Chrome DevTools visual checks completed at desktop `1440x900` and mobile `390x844`.
- Console checks found no errors on the five redesigned routes or the preserved spec/changelog routes.

Screenshot evidence is stored under `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/screenshots/`.

WO-0255 remains blocked on public deployment of the new site; implementation is complete, but production route verification is not available in this worker scope.
