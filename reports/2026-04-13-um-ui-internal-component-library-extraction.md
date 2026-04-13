# 2026-04-13 — UM UI Internal Component Library Extraction

## Summary

This report closes `WO-0175` by turning the tuned two-page MVP shell into the first reusable internal UI system for the standards host.

The goal was not to migrate the whole site. The goal was to stop treating the homepage shell as a one-off design and instead extract the first reusable primitives that later reintegration work can build on.

## Components Added

Created under `site/src/components/ui/`:

- `SiteHeader.astro`
- `SiteFooter.astro`
- `PublicPanel.astro`
- `SurfaceCard.astro`
- `SectionHeader.astro`
- `ActionRow.astro`
- `ChipRow.astro`

## Token Structure

Added:

- `site/src/styles/ui-tokens.css`

This file now owns the core visual tokens derived from the MVP shell:

- color tokens
- surface/border tokens
- radius tokens
- typography stacks
- shared shadow token

The remaining shared surface classes continue to live in:

- `site/src/styles/public-surface.css`

## Initial Adoption

### Shared layout

- `site/src/layouts/PublicSurfaceLayout.astro` now consumes the extracted `SiteHeader` and `SiteFooter` components.

### Homepage

- `site/src/pages/index.astro` now consumes:
  - `PublicPanel`
  - `SurfaceCard`
  - `SectionHeader`
  - `ActionRow`
  - `ChipRow`

### Review surfaces

- `site/src/pages/review/full-site-audit.astro` now consumes:
  - `PublicPanel`
  - `SectionHeader`
  - `ActionRow`

- `site/src/pages/review/reorganization-blueprint.astro` now consumes:
  - `PublicPanel`
  - `SectionHeader`
  - `ActionRow`

## Verification

- Ran `npm run build` successfully in `site/`.
- Browser sanity checks confirmed the homepage and review blueprint still render with the expected shell, CTA structure, and footer/header behavior after the extraction.

## Outcome

The project now has a real internal `UM UI` starting point rather than a conceptual plan only. The next wave should use this extracted layer to reintroduce selected reading surfaces under the shared public shell in `WO-0176`.
