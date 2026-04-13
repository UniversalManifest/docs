# WO-0175 -- UM UI Internal Component Library Extraction

**Status:** COMPLETED
**Priority:** P1
**Created:** 2026-04-12
**Completed:** 2026-04-13

## Objective

Extract an internal Astro-native component library and token system from the tuned two-page MVP so later site reorganization uses one shared design system without requiring DaisyUI or a Tailwind migration.

## Context

The project does need a component library over time. The correct source, however, is the tuned MVP shell rather than a third-party framework layered over a mixed Astro/Starlight/static-HTML site.

This work order turns the MVP from a one-off design into reusable infrastructure.

## Scope

In scope:

1. Define design tokens derived from the MVP homepage/spec shell.
2. Create `site/src/components/ui/` primitives for shared public surfaces.
3. Extract reusable layouts for public reading pages and the spec shell.
4. Establish the naming and ownership model for the internal `UM UI` system.

Out of scope:

- Migrating the full site onto the new system.
- Rewriting Starlight content rendering.
- External framework adoption such as DaisyUI.

## Deliverables

- Internal `UM UI` component inventory.
- Shared token and layout structure.
- Initial adoption on the MVP homepage/spec shell.

## Progress Notes

- Added the first `UM UI` primitives under `site/src/components/ui/`:
  - `SiteHeader.astro`
  - `SiteFooter.astro`
  - `PublicPanel.astro`
  - `SurfaceCard.astro`
  - `SectionHeader.astro`
  - `ActionRow.astro`
  - `ChipRow.astro`
- Split the MVP visual tokens into `site/src/styles/ui-tokens.css` and kept the shared surface styling in `site/src/styles/public-surface.css`.
- Refactored the shared public layout to consume extracted header/footer components instead of owning that markup directly.
- Refactored the homepage plus the two review surfaces onto the extracted section/action/panel primitives so the system is adopted in multiple live pages rather than existing as an unused stub.
- Recorded the extraction inventory and verification evidence in `docs/reports/2026-04-13-um-ui-internal-component-library-extraction.md`.

## Dependencies

- WO-0172 through WO-0174 complete the MVP tuning and publication baseline.

## Acceptance Criteria

- [x] Shared UI primitives and tokens exist in the site codebase.
- [x] The homepage/spec shell uses extracted shared components instead of page-specific one-off structure where practical.
- [x] The project has a documented internal component-library direction that does not depend on DaisyUI.
