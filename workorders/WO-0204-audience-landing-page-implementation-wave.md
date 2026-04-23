# WO-0204 -- Audience Landing Page Implementation Wave

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-04-22
**Completed:** 2026-04-22

## Objective

Implement the first audience landing pages so critical adopters can be directed to pages tailored to their ecosystem without bloating the homepage.

## Context

The IA now distinguishes between the `Home` cluster and audience-specific entry pages. This work order turns those audience pages into real public surfaces.

## Scope

In scope:

1. Implement the audience landing-page route family.
2. Implement the first audience pages using the completed content packs.
3. Link audience pages cleanly from the `Home` cluster and explorer.
4. Keep audience pages within the shared public shell family.

Out of scope:

- changing the global top nav
- rewriting the spec or docs corpus wholesale

## Deliverables

- Working audience landing-page family.
- First public audience pages implemented.

## Completion Notes

- Implemented the audience route family at `site/src/pages/audiences/[audience].astro`.
- Delivered metaverse and EU SSI audience pages as first-class public routes, alongside the remaining first-wave audience pages using the same shell and content model.
- Recorded implementation details in `docs/reports/2026-04-22-home-cluster-route-shell-explorer-and-audience-implementation.md`.

## Dependencies

- WO-0197
- WO-0199
- WO-0200
- WO-0201
- WO-0202

## Acceptance Criteria

- [x] Audience landing pages exist as real public routes.
- [x] Metaverse and EU SSI audience pages are implemented.
- [x] Audience pages are linked cleanly from the `Home` cluster.
- [x] The audience family remains secondary to the calm top-level nav.
