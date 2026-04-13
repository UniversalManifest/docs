# Report — 2026-04-13 — Tool And Proof Hub First Slice

## Scope

This report records the first implementation slice for `WO-0177`.

## What changed

- Added `site/src/layouts/ToolSurfaceLayout.astro` as the first shared shell pattern for tool/proof entry routes.
- Rebuilt `site/src/pages/learning/index.astro` as the shared tool-and-proof hub under that shell.
- Rebuilt `site/src/pages/sandbox/index.astro` so the sandbox chooser now lives inside the shared shell instead of owning the whole route as a standalone document.
- Updated `site/src/components/sandbox/ScenarioModal.astro` and `site/src/styles/sandbox/modal.css` so the chooser can be embedded without depending on a standalone topbar or global `html, body` styling.
- Framed the sandbox, workbench, harness, proof journeys, and standards/discovery boundaries as one public route family instead of an isolated legacy landing page.
- Kept the homepage and primary public navigation unchanged so richer interactive surfaces continue to sit behind the calm two-page front door.

## Verification

- `npm run build` passed in `site/`.
- Browser verification completed on:
  - `http://127.0.0.1:4325/learning/`
  - `http://127.0.0.1:4325/sandbox/`
- The sandbox search/filter behavior was rechecked after the route migration by filtering the chooser to the revocation scenario.

## Outcome

`WO-0177` is now active with a concrete first slice in place: the project has a shared tool/proof shell, an updated `/learning/` hub, and a rebuilt `/sandbox/` chooser route under that shell. Workbench and the remaining proof/tool wrappers are still follow-on work.
