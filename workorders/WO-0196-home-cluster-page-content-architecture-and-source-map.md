# WO-0196 -- Home-Cluster Page Content Architecture and Source Map

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-04-22
**Completed:** 2026-04-22

## Objective

Define the page-by-page content architecture for the new `Home` cluster so each page has a clear role, reader level, source map, and content boundary before any UI implementation begins.

## Context

WO-0195 established the `Home` cluster strategy and sitemap. The next step is to turn that into concrete page architecture for:

- `Overview`
- `Use Cases`
- `Explorer`
- `How It Works`
- `Standards Fit`

Without this step, the project will repeat the same failure mode as the current homepage: too many concepts mixed into one surface.

## Scope

In scope:

1. Define the purpose of each `Home`-cluster page.
2. Define the intended reader depth for each page.
3. Map canonical source files into each page.
4. Define what belongs on each page and what should be excluded.
5. Identify duplicate or conflicting existing public pages that the future implementation must reconcile.

Out of scope:

- writing final production copy
- implementing the UI
- changing the global nav

## Deliverables

- A page-by-page `Home`-cluster content architecture document.
- A source map from existing docs/integrations/pages into the new `Home` cluster.
- Clear inclusion/exclusion rules for each `Home` page.

## Completion Notes

- Defined the page-by-page architecture for `Overview`, `Use Cases`, `Explorer`, `How It Works`, and `Standards Fit`.
- Mapped each page to its reader depth, canonical source inputs, and exclusion boundaries so the implementation could proceed without collapsing back into a single overloaded homepage.
- Recorded the architecture and source map in `docs/reports/2026-04-22-home-cluster-page-content-architecture-and-source-map.md`.

## Dependencies

- WO-0195

## Acceptance Criteria

- [x] Each `Home`-cluster page has a documented goal.
- [x] Each page has a documented reader depth.
- [x] Each page has a documented source map.
- [x] Each page has documented content boundaries.
- [x] The future UI implementation can proceed without guessing page purpose.
