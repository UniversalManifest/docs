# Diagram Sources and Publishing

This folder stores editable source-of-truth diagram assets for Universal Manifest docs.

## DECISION: Static diagrams ON HOLD

There are two diagram production methods in this project:

1. **WO-0030 Prompt Pack Pipeline** (proven) — AI-generated animated SVGs via structured prompts. Produced all 29 currently-live production assets on universalmanifest.net (33 total including 2 test files and 2 pilot iterations). See `docs/design/ANIMATED-SVG-WORKFLOW.md` for the full workflow.

2. **Excalidraw** (set up but largely unused) — Manual/interactive diagram editing with `.excalidraw` source files. Only one template file exists.

### Static diagram status: ON HOLD

Infographics creation has been offloaded to the global agent system's infographics kit (outside this project). Static diagram work in this repo is paused until:

- the user returns with completed infographics work ready to integrate, or
- a knowledge gap analysis is needed and Excalidraw is useful for communicating those gaps to other agents.

Excalidraw is not approved for production visuals but may be used in the future for communicating complex logic flows or accurate infographic layouts when the above conditions are met. The prompt pack pipeline remains the default for animated explainers.

## Layout

- `docs/diagrams/excalidraw/` — editable `.excalidraw` source files (Excalidraw workflow)
- `site/public/diagrams/` — exported publish-ready assets (prefer SVG)
- `site/public/animations/` — animated SVG explainers (prompt pack pipeline)

## Excalidraw Workflow (if approved for your use case)

1. Edit diagram source in Excalidraw (`.excalidraw`).
2. Export to SVG (preferred for docs rendering quality).
3. Save exported SVG to `site/public/diagrams/`.
4. Reference the SVG from docs pages under `site/src/content/docs/`.

## Prompt Pack Pipeline Workflow (default for animated content)

See `docs/design/ANIMATED-SVG-WORKFLOW.md` for the complete process.

## Workflow and Deprecation Clarity

For canonical status of active workflow vs deprecated/historical tracks, see:

- `/Users/grig/work/repo/universalmanifest/docs/design/ANIMATION-WORKFLOW-AND-VERSION-STATUS.md`

Summary:
- Active production workflow: WO-0030 prompt-pack pipeline.
- Deprecated for production: Excalidraw exports and archived pre-upgrade asset tracks.

## Naming

Use stable, descriptive names:

- Excalidraw source: `<topic>-<purpose>.excalidraw`
- Static export: `<topic>-<purpose>.svg` (in `site/public/diagrams/`)
- Animated SVG: `<scenario>-<purpose>.svg` (in `site/public/animations/`)
