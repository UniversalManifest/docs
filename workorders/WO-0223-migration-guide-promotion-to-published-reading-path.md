# WO-0223: Migration-Guide Promotion to Published Reading Path

**Status:** COMPLETED
**Priority:** P1 (gates the spec body's migration link and the announcement)
**Depends on:** WO-0221
**Unblocks:** WO-0226
**Derived from:** 2026-04-26 v0.2 publication push plan, item 5; `docs/workorders/WO-0058-v01-to-v02-migration-guide.md`

## Objective

Move WO-0058's migration guide out of the "guides" folder draft posture into the published reading path with a top-of-fold link from the v0.2 spec page and the home-cluster's adopter route. Replace the `MIGRATION_GUIDE_HREF` placeholder left by WO-0221.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/docs/guides/MIGRATION-V01-V02.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/guides/` (does a mirror exist?)
- `/Users/grig/work/repo/universalmanifest/docs/W3C-STYLE-SPEC.html` (the WO-0221 placeholder)
- `/Users/grig/work/repo/universalmanifest/site/src/data/home-cluster.ts`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0058-v01-to-v02-migration-guide.md`

## Work to perform

1. **Confirm the published surface for the migration guide.** Two options:
   - Option A: it is already mirrored at `site/src/content/docs/guides/migration-v01-v02.md` (Starlight content collection) — verify and use that URL.
   - Option B: it lives only in `docs/guides/` and needs a Starlight content-collection mirror. If so, create the mirror with appropriate front-matter (`title`, `description`, `sidebar.order`).
2. **Update `docs/W3C-STYLE-SPEC.html`** Status-of-This-Document section: replace the `MIGRATION_GUIDE_HREF` placeholder from WO-0221 with the canonical migration-guide URL.
3. **Add a top-of-fold migration callout** in the spec body — a short paragraph above the "Abstract" section or as a new banner in `latest.astro` / `v0.2.astro` reading "Coming from v0.1? See the [Migration Guide]." This is the single most important link a v0.1 adopter needs.
4. **Surface the link from the home cluster:**
   - In `site/src/data/home-cluster.ts`, add the migration guide to whichever cluster slot serves adopter onboarding (likely the `getting-started` or `for-developers` cluster card).
5. **Cross-link from `site/src/content/docs/spec/v0.2.md`** to the migration guide.
6. **Confirm migration-guide content currency.** Skim for v0.1-only language that should now read "previously published v0.1." If found, file follow-on hygiene as a new subtask-comm note (do not fix it in this WO — that scope creep risks delaying the wave).

## Files to modify

- `site/src/content/docs/guides/migration-v01-v02.md` (create or update mirror)
- `docs/W3C-STYLE-SPEC.html` (replace placeholder)
- `site/src/pages/spec/latest.astro` and/or `site/src/pages/spec/v0.2.astro` (add top-of-fold callout)
- `site/src/data/home-cluster.ts` (add migration-guide link to adopter slot)
- `site/src/content/docs/spec/v0.2.md` (cross-link)

## Constraints

- **No content rewrites of the migration guide.** Content was approved in WO-0058. This is a promotion + linking WO only.
- **No new home-cluster slots.** Use existing slots; do not widen the public top nav.
- The top-of-fold callout MUST NOT push the Status-of-This-Document section below the fold on a 1280×800 viewport.

## Acceptance criteria

- The migration guide is reachable from `/spec/latest/` (and `/spec/v0.2/`) via a visible top-of-fold link.
- The home cluster has at least one entry that links to the migration guide.
- The Status-of-This-Document section's migration-guide href is no longer a placeholder.
- `npm run build` passes; no broken-link warnings introduced.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0223-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0223-BLOCKED.md`
