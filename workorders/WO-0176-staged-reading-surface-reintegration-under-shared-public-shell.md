# WO-0176 -- Staged Reading-Surface Reintegration Under Shared Public Shell

**Status:** COMPLETED
**Priority:** P1
**Created:** 2026-04-12

## Objective

Reintroduce the highest-value reading surfaces after the MVP is live, using the shared homepage-led public shell rather than the current mixture of styles and route assumptions.

## Context

Once the two-page MVP is tuned and published, the project can start to add content back. That content should return in a controlled order and only through the shared public shell introduced by the MVP/component-library work.

## Scope

In scope:

1. Reintroduce docs entry, use cases, reference, guides, governance, and adjacent reading pages in deliberate waves.
2. Move those pages onto the shared public-reader shell.
3. Prioritize the highest-value explanatory and adopter-facing routes first.
4. Reduce the visible fragmentation between current reading surfaces.

Out of scope:

- Tool-shell unification.
- Sandbox/tool rework.
- Machine-readable endpoint redesign.

## Deliverables

- Staged reading-surface migration plan.
- Shared public-reader shell adoption across the selected routes.
- Verification that the reintroduced pages feel like one site family.

## Progress Notes

- The first reintegration slice has started with the curated `/docs/` entry page.
- `site/src/pages/docs/index.astro` now consumes the extracted `UM UI` primitives (`PublicPanel`, `SurfaceCard`, `SectionHeader`, `ActionRow`, `ChipRow`) instead of carrying one-off shell markup.
- The page remains in the shared public shell and continues routing readers into the broader long-form corpus without widening the public MVP navigation.
- The first reader wave is now complete. Exact public route overrides now exist for `/about/why-um/`, `/about/one-pager/`, and `/use-cases/`, each rendered through Astro pages that consume the existing docs markdown as the content source of truth.
- `site/src/components/ui/ReaderSurface.astro` now provides the shared reader-page hero/content pattern for these routes.
- `site/src/styles/public-surface.css` now includes shared prose styling for reintegrated markdown content, including explicit handling for Starlight heading-anchor wrappers so reader pages no longer leak accessibility-only anchor text into the visible layout.
- Browser verification completed successfully on `http://127.0.0.1:4325/about/why-um/`, `http://127.0.0.1:4325/about/one-pager/`, and `http://127.0.0.1:4325/use-cases/` after a clean `npm run build`.

## Dependencies

- WO-0175 provides the internal UI/layout foundation.

## Acceptance Criteria

- [x] Reintroduced reading pages use the shared public shell.
- [x] Priority explanatory/adopter-facing pages return before lower-value route expansion.
- [x] The public site looks materially more unified after the first reintegration wave.
