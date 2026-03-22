# WO-0164 -- Docs Root Relocation and Warning-Free Build Baseline

**Status:** COMPLETED
**Priority:** P2
**Created:** 2026-03-19

## Objective

Remove the remaining Starlight `/` route-priority warning by relocating the old docs-root content off the site root while preserving that material as a published, reachable documentation page.

## Context

`WO-0161` intentionally moved the public root to a landing-first experience at `/` and introduced `/docs/` as the curated documentation entry point. `WO-0163` then documented the remaining Starlight root-route warning as an accepted condition because the old docs-root content still existed in `site/src/content/docs/index.md`.

That warning is now the only remaining site-build warning. The cleanest way to remove it is to stop publishing the old Starlight docs home at `/`, keep the landing page as the sole root owner, and republish the displaced content under an explicit non-root docs route.

## Scope

In scope:

1. Move the old docs-root content off the root route.
2. Preserve the content under a stable, non-conflicting docs route.
3. Update the curated `/docs/` entry so the relocated overview remains reachable.
4. Verify that the site build becomes warning-free.

Out of scope:

- Broader rewrite of the overview content.
- Landing-page redesign.
- Sidebar/IA changes beyond what is required to keep the relocated overview discoverable.

## Deliverables

- Updated `site/src/content/docs/index.md` frontmatter or replacement route ownership so it no longer maps to `/`.
- Updated docs entry routing or linking so the relocated overview is reachable.
- Build evidence showing the root-route warning is gone.

## Dependencies

- `WO-0161` established the landing-first `/` plus curated `/docs/` split.
- `WO-0163` reduced the warning baseline to the single remaining Starlight root-route warning.

## Execution Notes

- Preserve `/` as the landing page and `/docs/` as the curated docs start.
- Do not silently drop the old overview content; relocate it.
- Prefer the smallest route change that removes the warning without forcing broad IA churn.
- Final fix applied:
  - moved the old docs-root content to `slug: docs/overview`
  - added a note on the relocated page pointing readers back to `/docs/`
  - linked the relocated overview from the curated `/docs/` entry page

## Acceptance Criteria

- [x] The old docs-root content no longer conflicts with `/`.
- [x] The relocated overview content is still reachable from the public docs surface.
- [x] `cd /Users/grig/work/repo/universalmanifest/site && npm run build` completes without warnings.
