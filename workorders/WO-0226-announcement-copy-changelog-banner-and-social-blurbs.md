# WO-0226: Announcement Copy — Changelog Entry, Home Page Banner, Social Blurbs

**Status:** NOT_STARTED
**Priority:** P1
**Depends on:** WO-0221, WO-0222, WO-0223
**Unblocks:** WO-0229
**Derived from:** 2026-04-26 v0.2 publication push plan, item 4; `docs/MARKDOWN-SOURCE-FIDELITY-PROCESS.md`

## Objective

Produce the public-facing announcement of v0.2 across three surfaces: changelog (long-form), home page (short banner), and social/email blurbs (one-line, two-paragraph variants). Source-fidelity rules: markdown source first, rendered surface second.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/publishing/changelog.md`
- `/Users/grig/work/repo/universalmanifest/site/src/data/home-cluster.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/index.astro`
- `/Users/grig/work/repo/universalmanifest/docs/MARKDOWN-SOURCE-FIDELITY-PROCESS.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0205-home-cluster-migration-harmonization-and-publication-readiness.md`

## Work to perform

1. **Author the changelog entry** under the v0.2 section in `site/src/content/docs/publishing/changelog.md`. Replace the `(Draft)` heading with `(Published — 2026-04-26)`. Add a sub-entry describing what publication actually means: durable URL, immutable hashes (cite WO-0220's hashes), conformance suite, migration guide, governance.
2. **Author the home page banner copy.** Two variants:
   - Variant A: a thin announcement strip above the home cluster ("Universal Manifest v0.2 is published. Read the spec → Read the migration guide.")
   - Variant B: a tile inserted into the home cluster's news/announcements slot (if `home-cluster.ts` has one).
   Pick one based on existing surface design — do not introduce a new home-page section. If neither slot exists, add a small announcement strip above the cluster fold.
3. **Author the social/email blurbs** in a new file `docs/announcement/2026-04-26-v0-2-published.md`:
   - 1-line version (X/Twitter, Mastodon, BlueSky)
   - 2-paragraph version (LinkedIn, mailing list, Discord)
   - 5-paragraph version (blog post seed)
   Each variant cites the durable spec URL, the migration guide, the changelog entry, and the contact / discussion path. No emojis.
4. **Source-fidelity check:** the changelog markdown must be the source; the home-page banner copy and the social blurbs MUST cite the changelog entry's anchor URL as the canonical record.

## Files to modify

- `site/src/content/docs/publishing/changelog.md` (primary announcement record)
- `site/src/data/home-cluster.ts` (if it has a news/announcement slot) OR `site/src/pages/index.astro` (banner strip)
- `docs/announcement/2026-04-26-v0-2-published.md` (new — three blurb variants)

## Constraints

- **No emojis** in any announcement copy.
- **Calm front door.** No widening of the public top nav (per CRITICAL-PATH.md current focus).
- **Source-fidelity:** if the home page or social copy diverges from the changelog, the changelog wins. Document the rule in the result report.
- **No marketing fluff.** Match the project's existing tone (technical, calm, factual). Compare WO-0205 completion notes for tone.

## Acceptance criteria

- The changelog has a v0.2 published-on-2026-04-26 entry citing the WO-0220 hashes and the migration guide.
- The home page either has a banner strip or a news tile linking to the changelog and migration guide.
- `docs/announcement/2026-04-26-v0-2-published.md` contains exactly three variants (1-line, 2-paragraph, 5-paragraph).
- The home banner copy and social blurbs cite the changelog entry's URL as the canonical record.
- `npm run build` passes.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0226-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0226-BLOCKED.md`
