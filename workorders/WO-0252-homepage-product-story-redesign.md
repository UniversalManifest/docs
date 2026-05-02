# WO-0252: Homepage Product Story Redesign

**Status:** SUPERSEDED 2026-05-02 — completed implementation retained as temporary evidence only; do not extend as final homepage direction
**Priority:** Historical P0; removed from active execution path
**Depends on:** v0.2 publication wave complete
**Unblocks:** none directly; superseded by WO-0253 before external-reader validation can resume
**Derived from:** 2026-05-01 user review of local homepage at `http://127.0.0.1:4300/`; 2026-05-02 objective realignment

## Problem

The current homepage fails as a front door. It reads like internal project inventory spread across a page instead of a clear product story. It exposes planning language such as "Home cluster" and "calm navigation," mixes announcement, audience routing, spec routing, and use-case cards without a clear hierarchy, and gives a first-time reader too many equally weighted paths before they understand why Universal Manifest exists.

This blocks external-reader validation because the reader cohort would be testing a confusing front door rather than the intended v0.2 publication experience.

## Supersession note

This work order produced a verified implementation pass, but that pass did not meet the user's quality bar for the public front door. Treat it as historical evidence of what was attempted, not as an approved design direction.

Do not keep iterating on this WO. The corrected active sequence is:

1. `WO-0253`: produce a design report for the five-page homepage cluster.
2. `WO-0254`: implement the approved design.
3. `WO-0255`: verify the production reader path.
4. `WO-0256`: run real external-reader validation.

## Objective

Rebuild the homepage into a coherent, reader-first product story that answers, in order:

1. What problem does Universal Manifest solve?
2. What is the promise in one concrete sentence?
3. What does a manifest carry?
4. Why does that matter in one or two high-signal scenarios?
5. Where should a reader go next based on intent?

## Files to read first

- `/Users/grig/work/repo/universalmanifest/site/src/pages/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/data/home-cluster.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/styles/public-surface.css`
- `/Users/grig/work/repo/universalmanifest/site/src/layouts/PublicSurfaceLayout.astro`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-04-30-v0-2-publication-evidence-pack.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0214-BLOCKED.md`

## Work to perform

1. Replace the homepage's inventory structure with a sequenced narrative:
   - hero: one sharp problem/promise statement
   - concrete "what travels" explanation
   - one or two example flows
   - proof/publication status
   - short next-step decision set
2. Remove internal-facing language from visible page copy, including "Home cluster," "top-level navigation stays calm," and similar project-management phrasing.
3. Reduce card sprawl. Use cards only where they help compare repeated choices; avoid nesting card-like surfaces.
4. Use an existing relevant visual asset from the repo, or a simple product-native layout, so the page has a real first-viewport signal rather than abstract decoration.
5. Preserve required published-v0.2 paths:
   - `/spec/latest/`
   - `/spec/v0.2/`
   - `/guides/migration-v01-v02/`
   - `/publishing/changelog/`
6. Keep the local tab system if useful, but do not force first-time readers through internal IA vocabulary.
7. Remove or neutralize decorative orb/backdrop styling on the homepage if it contributes to visual noise.
8. Verify locally at desktop and mobile widths.

## Files expected to modify

- `site/src/pages/index.astro`
- `site/src/styles/public-surface.css`
- Optional: `site/src/data/home-cluster.ts` if the homepage data model needs simpler labels or summaries

## Constraints

- Do not widen the global nav.
- Do not make a marketing landing page with vague claims.
- Do not hide the published v0.2 status; make it a trust/proof point, not the whole homepage.
- Do not remove working routes or publication links.
- Do not alter the spec content.

## Acceptance criteria

- A first-time reader can understand the problem, the promise, and the next action from the first screen.
- The homepage no longer exposes internal planning language.
- The visible structure has a clear hierarchy and no "sprayed sitemap" feel.
- The homepage links to the published spec, migration guide, changelog, and at least one concrete scenario path.
- `npm run build` passes from `/Users/grig/work/repo/universalmanifest/site`.
- Local review URL remains `http://127.0.0.1:4300/`.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-05-01-wo-0252-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-05-01-wo-0252-BLOCKED.md`
