# WO-0097 — Publish Commercial Journeys on the Public Site

**Status:** COMPLETED
**Created:** 2026-03-01
**Priority:** P1 (Important)
**Source:** Project Completeness and Vision Audit (2026-03-01), Gap 4, Recommended Action P1-7
**Tags:** [site], [docs]
**Blocks:** None (enhances external communication)
**Dependencies:** None
**Estimated effort:** 3-4 hours

## Objective

Publish the commercial journey documents from `docs/journeys/commercial/` on the public `universalmanifest.net` site under a "Use Cases" or "Stories" section.

## Why this work matters

The completeness audit found that five compelling commercial journeys exist (creator, venue operator, app developer, privacy, enterprise) but are not published on the site. These narrative documents demonstrate UM's value in concrete, relatable terms and are among the project's strongest persuasion tools for non-technical audiences.

## Scope

### Source files

- `docs/journeys/commercial/creator-journey.md`
- `docs/journeys/commercial/venue-operator-journey.md`
- `docs/journeys/commercial/app-developer-journey.md`
- `docs/journeys/commercial/privacy-journey.md`
- `docs/journeys/commercial/enterprise-journey.md`

### New site pages to create

Create Starlight docs pages under a "Use Cases" or "Stories" section:

1. `site/src/content/docs/use-cases/index.md` — Index page
2. `site/src/content/docs/use-cases/creator.md`
3. `site/src/content/docs/use-cases/venue-operator.md`
4. `site/src/content/docs/use-cases/app-developer.md`
5. `site/src/content/docs/use-cases/privacy.md`
6. `site/src/content/docs/use-cases/enterprise.md`

### Sidebar changes

Add a "Use Cases" section to the site sidebar in `site/astro.config.mjs`.

### Content adaptation

- Add Starlight frontmatter.
- Update internal links to point to site pages.
- Ensure each journey is accessible to a non-technical reader.

## Acceptance criteria

- [ ] At least 5 commercial journeys are published as site pages.
- [ ] A "Use Cases" or "Stories" section exists in the site navigation.
- [ ] `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean` succeeds.
- [ ] Each published journey includes clear, relatable narrative.

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
- Manual review of published journey pages.
