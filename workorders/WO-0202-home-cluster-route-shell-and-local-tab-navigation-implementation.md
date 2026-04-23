# WO-0202 -- Home-Cluster Route Shell and Local Tab Navigation Implementation

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-04-22
**Completed:** 2026-04-22

## Objective

Implement the new `Home`-cluster route shell and local tab navigation while preserving the calm global menu of `Home` and `Latest Spec`.

## Context

The IA work is intended to result in a real route family, not just a content strategy document. This work order implements the structural shell for the `Home` cluster so content can be presented across multiple focused views.

## Scope

In scope:

1. Implement the local `Home` tab bar.
2. Implement the route family for the `Home` cluster.
3. Keep the top-level global menu limited to `Home` and `Latest Spec`.
4. Preserve spec continuity and the current calm public-shell model.

Out of scope:

- final explorer implementation
- final audience-page implementation
- broad route-retirement work outside this cluster

## Deliverables

- Working `Home`-cluster route shell.
- Local-tab navigation under the public header.
- Stable relationship between the root landing page and its subordinate views.

## Completion Notes

- Implemented the `Home`-cluster local-tab shell in `site/src/layouts/PublicSurfaceLayout.astro` and `site/src/components/ui/HomeClusterTabs.astro`.
- Reworked the root route into `Overview` and wired `/use-cases/`, `/explorer/`, `/how-it-works/`, and `/standards-fit/` into the shared local-tab family.
- Recorded implementation details in `docs/reports/2026-04-22-home-cluster-route-shell-explorer-and-audience-implementation.md`.

## Dependencies

- WO-0196

## Acceptance Criteria

- [x] The `Home` cluster exists as a real route family.
- [x] Local tabs work without widening the global nav.
- [x] The root page no longer has to carry every idea by itself.
- [x] `/spec/latest/` remains stable and obvious.
