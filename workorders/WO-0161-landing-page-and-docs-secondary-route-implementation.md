# WO-0161 -- Landing Page and Docs Secondary Route Implementation

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-03-15

## Objective

Implement the public experience shift that makes Universal Manifest a landing-first site with documentation as a secondary experience, while preserving route stability and the existing standards/reference depth.

## Context

The project currently has architecture and planning work for a multi-surface public system, but it still lacks an explicit implementation work order for the most visible change: turning `/` into a true landing page and moving the documentation experience into a clearly secondary path.

Without this work order, the program risks stopping at planning and discovery contracts while leaving the public home experience unchanged.

## Scope

In scope:

1. Design and implement a landing-first root experience for `universalmanifest.net`.
2. Define and implement the secondary docs/reference entry path.
3. Preserve compatibility for existing deep links and published docs routes.
4. Add clear audience lanes from the landing surface, including:
   - evaluators
   - implementers
   - agents
   - tooling/proof explorers
5. Ensure the landing surface, docs shell, and discovery layer reinforce one another rather than competing.

Out of scope:

- Full implementation of every machine-readable discovery artifact covered by WO-0158.
- Higher-agency runtime or agent-service behavior.
- Rewriting the entire docs corpus.

## Deliverables

- New landing page implementation.
- Secondary docs/reference entry route implementation.
- Redirect/compatibility plan for existing routes.
- Updated public navigation reflecting the landing/docs/tool split.

Completed artifacts:

- `docs/reports/2026-03-15-landing-first-public-experience-implementation-report.md`
- `site/src/layouts/PublicSurfaceLayout.astro`
- `site/src/styles/public-surface.css`
- `site/src/pages/index.astro`
- `site/src/pages/docs/index.astro`
- `site/scripts/sync-agent-discovery.mjs`
- `site/public/.well-known/universal-manifest.json`
- `site/public/llms.txt`
- `site/astro.config.mjs`

## Dependencies

- WO-0157 defines the target architecture.
- WO-0158 should define the discovery and route taxonomy that the landing page points to.

## Execution Notes

- The landing page should be concise and directional, not a second documentation home.
- Existing published deep links must remain safe during migration.
- The change should improve both human comprehension and agent routing.

## Acceptance Criteria

- [x] `/` behaves as a landing-first public entry surface.
- [x] Documentation has a clearly secondary entry path.
- [x] Existing deep links remain functional or redirect cleanly.
- [x] The new home experience clearly routes evaluators, implementers, agents, and tooling/proof users.
