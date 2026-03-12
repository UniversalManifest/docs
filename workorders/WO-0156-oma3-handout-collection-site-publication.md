# WO-0156 -- OMA3 Handout Collection Site Publication

**Status:** IN_PROGRESS
**Priority:** P0
**Created:** 2026-03-11

## Objective

Publish the OMA3 handout collection (10 documents: reading guide + 9 topic handouts) as a navigable subsection on universalmanifest.net with proper Starlight sidebar integration.

## Context

The OMA3 handout collection at `docs/handouts/oma3-2026-03-12/` contains 10 markdown files prepared for Alfred Tom and OMA3 members. These documents explain Universal Manifest architecture from the ground up, covering the problem, envelope format, facets/pointers, consent, signatures, resolver, IWPS integration, broader application space, and roadmap.

Publishing these as a dedicated section on the docs site makes them accessible via stable URLs for OMA3 reviewers and other stakeholders.

## Scope

1. Copy each handout file to `site/src/content/docs/handouts/` with Starlight-compatible frontmatter
2. Add an "OMA3 Handouts" sidebar section to `site/astro.config.mjs` using `autogenerate`
3. Update inter-document links to use site-relative paths instead of relative file references
4. Build-verify the site to confirm no errors
5. Deploy to production

## Deliverables

- 10 handout pages published under `/handouts/` on universalmanifest.net
- "OMA3 Handouts" sidebar section with ordered navigation (Start Here, 1-9)
- Original files in `docs/handouts/oma3-2026-03-12/` remain unmodified

## Acceptance Criteria

- [ ] All 10 handout pages render correctly on the site
- [ ] Sidebar shows "OMA3 Handouts" section with proper ordering
- [ ] Inter-document navigation links work
- [ ] Site builds without errors
- [ ] Deployed to production
