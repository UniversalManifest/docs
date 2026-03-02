# WO-0091 — Publish Explainer Documents on universalmanifest.net

**Status:** COMPLETED
**Created:** 2026-03-01
**Priority:** P0 (Critical)
**Source:** Project Completeness and Vision Audit (2026-03-01), Gap 1, Recommended Action P0-1
**Tags:** [site], [docs]
**Blocks:** External communication of UM's value proposition
**Dependencies:** None
**Estimated effort:** 3-5 hours

## Objective

Publish the explainer documents from `docs/explainers/` on the public `universalmanifest.net` site. These are the project's strongest external-facing assets but are currently only accessible by browsing the repo directly.

## Why this work matters

The completeness audit identified that the one-pager, full briefing, agent briefing, and animation briefing are among the strongest documents in the entire project, yet none of them are published on the public site. A potential evaluator or adopter visiting `universalmanifest.net` has no way to discover these documents.

## Scope

### New site pages to create

Create Starlight docs pages for each explainer:

1. **`site/src/content/docs/about/one-pager.md`** — adapted from `docs/explainers/one-pager.md`
2. **`site/src/content/docs/about/full-briefing.md`** — adapted from `docs/explainers/full-briefing.md`
3. **`site/src/content/docs/about/agent-briefing.md`** — adapted from `docs/explainers/agent-briefing.md`
4. **`site/src/content/docs/about/index.md`** — index page for the "About" or "Learn" section

### Sidebar changes

Add a new top-level "About" or "Learn" section to the site sidebar navigation in `site/astro.config.mjs` containing these pages.

### Content adaptation

- Add Starlight frontmatter (title, description) to each page.
- Ensure internal links point to site pages (not repo files).
- Verify formatting renders correctly in Starlight.

## Acceptance criteria

- [ ] At least 3 explainer documents are published as site pages.
- [ ] A new "About" or "Learn" section exists in the site navigation.
- [ ] The one-pager is discoverable within 2 clicks from the site landing page.
- [ ] `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean` succeeds.
- [ ] Links within the published explainers resolve correctly to other site pages.

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
- Manual review of published explainer pages in browser.
