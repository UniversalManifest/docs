# Universal Manifest — Live Status and Next Critical Path

**Date:** 2026-02-18

## Current production status

Universal Manifest is live on the two-domain architecture:

- Standards/docs host: `https://universalmanifest.net`
- Resolver host: `https://myum.net`

Production smoke verification:

- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run smoke:endpoints:prod`
- Result: **PASS**

## Work-order status update

- `WO-0003` (publishing and release): **COMPLETED**
- `WO-0014` (interactive manifest workbench): **OPEN**
- `WO-0015` (first-time overview and visual onboarding): **IN PROGRESS**

## CEO-priority additions (source of truth)

1. Add an interactive manifest workbench page where users can import, explore/edit, create, validate, and export manifests.
2. Add a clear first-time overview of what Universal Manifest is and how to use it.

These priorities are recorded in:

- `docs/DECISIONS.md`
- `docs/workorders/WO-0014-interactive-manifest-workbench.md`
- `docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md`

## Visual onboarding structure now in place

- Diagram source scaffold: `docs/diagrams/`
- Excalidraw template source: `docs/diagrams/excalidraw/universal-manifest-overview-template.excalidraw`
- Published diagram asset: `site/public/diagrams/universal-manifest-overview-template.svg`
- First-time overview page template: `site/src/content/docs/getting-started/universal-manifest-overview.md`

## Next execution focus

1. Build the first usable version of the interactive workbench (`WO-0014`).
2. Validate first-time overview clarity with external readers and iterate (`WO-0015`).
3. Continue v0.2 interoperability hardening and conformance edge-case expansion.
