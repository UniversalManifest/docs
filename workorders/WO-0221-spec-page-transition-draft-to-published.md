# WO-0221: Spec Page Transition — Draft to Published (Status-of-This-Document Rewrite)

**Status:** COMPLETED 2026-04-30 — `/spec/latest/` now presents the published v0.2 posture, durable `/spec/v0.2/` route added, and focused build/diff verification passed; result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0221-result.md`
**Priority:** P0 (gates every downstream announcement and machine-readable surface)
**Depends on:** WO-0220
**Unblocks:** WO-0222, WO-0223, WO-0224, WO-0225, WO-0226
**Derived from:** 2026-04-26 v0.2 publication push plan, item 2

## Objective

Flip `/spec/latest/` from "Latest Draft Specification" to "Latest Published Specification" (or the project-correct equivalent for v0.x), rewrite the Status-of-This-Document section to match the published-but-still-v0.x posture (breaking changes still allowed across minor versions per `PUBLISHING-AND-VERSIONING.md` §5.2), and ensure `/spec/v0.2/` is the durable canonical URL with `/spec/latest/` redirecting (or linking) to it.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/docs/W3C-STYLE-SPEC.html` (lines 252–290 — the title, dt-published, and Status-of-This-Document blocks)
- `/Users/grig/work/repo/universalmanifest/site/src/pages/spec/latest.astro`
- `/Users/grig/work/repo/universalmanifest/docs/PUBLISHING-AND-VERSIONING.md` §5
- `/Users/grig/work/repo/universalmanifest/docs/governance/RELEASE-CADENCE.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/BREAKING-CHANGE-POLICY.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/spec/v0.2.md`

## Work to perform

1. **Rewrite the title:** `<h1 id="title" class="title p-name">Universal Manifest Latest Draft Specification</h1>` → `Universal Manifest v0.2 Specification` (or the operator's chosen exact phrasing — propose two variants and document the choice).
2. **Rewrite the subtitle:** "W3C-style draft specification on a stable subordinate route" → "W3C-style specification on a stable subordinate route".
3. **Rewrite Status-of-This-Document** (lines 285–289). The new text MUST:
   - declare v0.2 as the current published version
   - clarify that v0.x still permits breaking changes via minor-version bumps (cite `PUBLISHING-AND-VERSIONING.md` §5.2)
   - link to the migration guide (added in WO-0223 — leave the `href` placeholder `MIGRATION_GUIDE_HREF` and document for the next WO)
   - link to the RFC mechanism and breaking-change policy (`/governance/breaking-change-policy/` and `/governance/spec-improvement-queue/` — added in WO-0225)
   - remove the "synthetic peer review" hedge sentence; replace with a publication-status statement
4. **Update the `<dt>Latest published version:</dt>` block** (line 260) to point at `/spec/v0.2/` (the durable URL) rather than back at `/spec/latest/`. The latest-pointer on `/spec/latest/` MUST reference the durable canonical version.
5. **Decide and implement** the `/spec/v0.2/` durable route:
   - Option A: add a thin Astro page at `site/src/pages/spec/v0.2.astro` that reuses the same source-of-truth HTML import pattern as `latest.astro`.
   - Option B: configure a redirect from `/spec/latest/` to `/spec/v0.2/`.
   - Recommend Option A (durable page that stays at v0.2 even after v0.3 lands; latest.astro can later redirect to /spec/v0.3/).
6. **Update `site/src/content/docs/spec/v0.2.md`** front-matter title from `Specification v0.2 (draft)` to `Specification v0.2`.
7. **Verify** via local `npm run build` that the spec page renders with the new status block and TOC remains intact.

## Files to modify

- `docs/W3C-STYLE-SPEC.html` (primary — Status-of-This-Document, title, subtitle, dt blocks)
- `site/src/pages/spec/v0.2.astro` (new — mirrors `latest.astro` pattern)
- `site/src/content/docs/spec/v0.2.md` (front-matter title change only)

## Constraints

- **Do not change the normative spec body.** This WO is a publication-status flip only. Sections 1–N of the spec text remain byte-identical.
- **Do not delete `/spec/latest/`.** It remains the rolling pointer to the most recent published version. Today that is v0.2; tomorrow it will be v0.3.
- **No tag changes.** Tagging belongs to WO-0220.
- Migration-guide href stays as a `MIGRATION_GUIDE_HREF` placeholder until WO-0223 promotes the guide; track in result report.

## Acceptance criteria

- `docs/W3C-STYLE-SPEC.html` no longer says "draft specification" in the title, subtitle, or Status-of-This-Document section.
- A new `site/src/pages/spec/v0.2.astro` exists and renders the same source-of-truth HTML; `npm run build` passes.
- `/spec/latest/` and `/spec/v0.2/` both render the same body, but `/spec/v0.2/` is the durable URL the changelog and announcements cite.
- The Status-of-This-Document block contains: (a) "v0.2 is published"; (b) "minor-version bumps may still be breaking per the versioning policy"; (c) placeholder hrefs documented in the result report for WO-0223/WO-0225 to fill.
- No spec-body section heading or paragraph text changed.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0221-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0221-BLOCKED.md`
