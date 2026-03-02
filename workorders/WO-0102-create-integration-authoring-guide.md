# WO-0102 — Publish Integration Authoring Guide on the Site (Fix Broken Link)

**Status:** COMPLETED
**Created:** 2026-03-01
**Priority:** P1 (Important)
**Source:** Project Completeness and Vision Audit (2026-03-01), Gap 30; Verification report correction (file exists but link is broken)
**Tags:** [docs], [site]
**Blocks:** External contributors creating new integration lanes
**Dependencies:** None
**Estimated effort:** 2-3 hours

## Objective

Publish the existing integration authoring guide on the docs site to fix the broken link in the integration catalog index.

## Why this work matters

The verification agent confirmed that the integration authoring guide **exists** as a repo file at `docs/guides/integration-authoring-guide.md` (186 lines), but it is **not published** on the docs site. The integration catalog index (`site/src/content/docs/integrations/index.md`) links to `/docs/guides/integration-authoring-guide`, which is a dead URL because no `site/src/content/docs/guides/` directory exists. This is a BROKEN LINK issue, not a missing content issue. The original audit report incorrectly stated the guide "does not appear to exist."

## Scope

### Existing file (confirmed to exist)

**`/Users/grig/work/repo/universalmanifest/docs/guides/integration-authoring-guide.md`** — 186 lines, already written. Review for completeness and consistency with TEMPLATE.md.

### Create site page

**`site/src/content/docs/guides/integration-authoring.md`** — Publish the guide on the site with Starlight frontmatter. This requires creating the `site/src/content/docs/guides/` directory.

### Fix the broken link

Ensure the link path in the integration catalog index (`site/src/content/docs/integrations/index.md`) resolves to the newly published page.

### Cross-reference with TEMPLATE.md

Ensure the authoring guide and `integrations/TEMPLATE.md` are consistent and cross-linked. The guide should reference the template, and the template should reference the guide.

### Content review

The guide already covers (verify each is present and current):
1. When to create a new integration lane
2. How to use the template
3. Fixture requirements for the lane
4. Boundary statement requirements (normative vs non-normative)
5. How to submit the lane (PR process)

## Acceptance criteria

- [ ] Integration authoring guide exists and is complete.
- [ ] Guide is published as a page on the public site.
- [ ] Guide and TEMPLATE.md are consistent and cross-linked.
- [ ] The integration catalog index link resolves to the published guide.
- [ ] `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean` succeeds.

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
- Manual review of guide completeness.
- Verify link from integration catalog index resolves.
