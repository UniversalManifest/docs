# WO-0081 — Add Specification Identity Banner to All Entry-Point Documents

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P0 (Critical)
**Source:** Spec-vs-Implementation Boundary Audit (2026-03-01), Recommendation R1, Action Items 1 and 20
**Tags:** [docs], [spec], [onboarding]
**Blocks:** External perception of UM as a specification (not a TypeScript library)
**Dependencies:** None
**Estimated effort:** 2-4 hours

## Objective

Add an explicit "Universal Manifest is a specification" banner or callout to the four highest-traffic entry-point documents, ensuring that any newcomer encountering UM for the first time understands within 30 seconds that UM is a specification implementable in any language.

## Why this work matters

The boundary audit found that none of the primary entry points (root README, site landing page, spec READMEs) include an explicit statement that UM is a specification. This causes newcomers to perceive UM as "a TypeScript project" rather than "an open specification with a TypeScript reference implementation."

## Scope

Add the following standard banner language (or a context-appropriate variant) to each file:

> Universal Manifest is an open specification for portable state capsules. It is not tied to any particular programming language, framework, or runtime. The TypeScript helper in this repository is one reference implementation; you can build a conformant implementation in any language using the published spec artifacts and conformance fixtures.

### Files to modify

1. **`/Users/grig/work/repo/universalmanifest/README.md`** — Add banner near the top, before any code or npm commands.
2. **`/Users/grig/work/repo/universalmanifest/site/src/content/docs/index.md`** — Add as a prominent callout (Starlight `:::note` or similar) near the top of the landing page.
3. **`/Users/grig/work/repo/universalmanifest/spec/v0.1/README.md`** — Add as the first paragraph after the title.
4. **`/Users/grig/work/repo/universalmanifest/spec/v0.2/README.md`** — Add as the first paragraph after the title.

### Additional action

5. Surface the "Notes on origin-runtime relationship" text from `docs/STATE-OF-THE-PROJECT.md` (lines 316-322) on the site overview page or landing page, as it is the clearest statement of the spec-implementation relationship but is currently buried in a status document.

## Acceptance criteria

- [ ] All four entry-point documents contain an explicit "UM is a specification" statement.
- [ ] The statement appears within the first screen of content (above the fold).
- [ ] The statement mentions that the TypeScript helper is ONE reference implementation.
- [ ] The statement invites implementations in any language.
- [ ] The origin-runtime relationship text is surfaced on at least one public-facing site page.
- [ ] `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean` succeeds.

## Validation commands

- `rg -n "specification" /Users/grig/work/repo/universalmanifest/README.md` (confirm banner exists)
- `rg -n "specification" /Users/grig/work/repo/universalmanifest/site/src/content/docs/index.md` (confirm banner exists)
- `rg -n "specification" /Users/grig/work/repo/universalmanifest/spec/v0.1/README.md` (confirm banner exists)
- `rg -n "specification" /Users/grig/work/repo/universalmanifest/spec/v0.2/README.md` (confirm banner exists)
