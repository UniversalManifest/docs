# WO-0030 Pilot Animation Review

Date: 2026-02-22

## Pilot assets reviewed

- `site/public/animations/um-core-flow-pilot.svg`
- `site/public/animations/um-overlay-lanes-pilot.svg`

## Placement verified

- `site/src/content/docs/index.md`
- `site/src/content/docs/getting-started/universal-manifest-overview.md`

## Checklist result (pre-build)

- [x] Two pilot animations generated
- [x] Assets integrated into docs pages
- [x] Reduced-motion fallback present in both pilot SVG files
- [x] UM terminology included in labels
- [x] Site build verification (`npm run build`, `npm run build:clean`)
- [x] Browser visual verification (`agent-browser` checks on `/` and `/getting-started/universal-manifest-overview/`)

## Verification notes

- Build commands:
  - `cd site && npm run build`
  - `cd site && npm run build:clean`
- Browser checks (local):
  - `http://localhost:4321/`
  - `http://localhost:4321/getting-started/universal-manifest-overview/`
  - `http://localhost:4321/integrations/smart-glasses/`
  - `http://localhost:4321/getting-started/workbench/`
  - `http://localhost:4321/proof/harness/`
- Browser checks (live):
  - `https://universalmanifest.net/`
  - `https://universalmanifest.net/getting-started/universal-manifest-overview/`

Observed:

- The Overview page no longer includes \"Highlighted Tools\" text.
- The pilot animation image is present on `/` (`/animations/um-core-flow-pilot.svg`).
- The pilot animation image is present on the first-time overview page (`/animations/um-overlay-lanes-pilot.svg`).
- Smart Glasses integration page title renders as `Smart Glasses`.
- Pilot asset size check:
  - `um-core-flow-pilot.svg`: 3,597 bytes
  - `um-overlay-lanes-pilot.svg`: 4,368 bytes
  - both are within the defined hero/inline budgets in `ANIMATED-SVG-SPEC.md`.
