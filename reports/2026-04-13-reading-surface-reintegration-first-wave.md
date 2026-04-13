# Report — 2026-04-13 — Reading-Surface Reintegration First Wave

## Scope

This report records the first completed `WO-0176` reintegration wave after the two-page MVP and the initial `UM UI` extraction.

## What changed

- Preserved the two-page public MVP (`/` and `/spec/latest/`) without widening the primary menu.
- Kept `/docs/` as the curated documentation entry under the shared public shell.
- Reintroduced the highest-value adopter-facing reader routes under the same shell:
  - `/about/why-um/`
  - `/about/one-pager/`
  - `/use-cases/`
- Added `site/src/components/ui/ReaderSurface.astro` as the shared reader-page pattern.
- Rendered the existing Starlight markdown entries as the source of truth for these routes rather than duplicating the content into second copies.
- Added shared prose styling and explicit Starlight heading-anchor handling so reintegrated reader pages do not expose accessibility-only anchor text visually.

## Verification

- `npm run build` passed in `site/`.
- Browser verification completed on:
  - `http://127.0.0.1:4325/about/why-um/`
  - `http://127.0.0.1:4325/about/one-pager/`
  - `http://127.0.0.1:4325/use-cases/`
- The route overrides build cleanly and take precedence over the underlying Starlight `[...slug]` routes as intended.

## Outcome

The first reintegration wave is complete. The public site now has a materially more unified reader family for the highest-value explanatory and adopter-facing surfaces while preserving the calm MVP front door.
