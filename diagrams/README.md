# Diagram Sources and Publishing

This folder stores editable source-of-truth diagram assets for Universal Manifest docs.

## DECISION PENDING — Check with project owner before producing diagrams

There are two diagram production methods in this project. **Do NOT start diagram work without confirming which method to use:**

1. **WO-0030 Prompt Pack Pipeline** (proven) — AI-generated animated SVGs via structured prompts. Produced all 16 currently-live production assets on universalmanifest.net. See `docs/design/ANIMATED-SVG-WORKFLOW.md` for the full workflow.

2. **Excalidraw** (set up but largely unused) — Manual/interactive diagram editing with `.excalidraw` source files. Only one template file exists. May be appropriate for static architecture diagrams but this has not been validated.

**Before creating any new diagrams or animations, ask the project owner which method to use for your specific use case.** The prompt pack pipeline is the default for animated explainers. The role of Excalidraw for static diagrams is undecided.

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

## Naming

Use stable, descriptive names:

- Excalidraw source: `<topic>-<purpose>.excalidraw`
- Static export: `<topic>-<purpose>.svg` (in `site/public/diagrams/`)
- Animated SVG: `<scenario>-<purpose>.svg` (in `site/public/animations/`)
