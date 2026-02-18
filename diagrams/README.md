# Diagram Sources and Publishing

This folder stores editable source-of-truth diagram assets for Universal Manifest docs.

## Layout

- `docs/diagrams/excalidraw/` — editable `.excalidraw` source files
- `site/public/diagrams/` — exported publish-ready assets (prefer SVG)

## Workflow

1. Edit diagram source in Excalidraw (`.excalidraw`).
2. Export to SVG (preferred for docs rendering quality).
3. Save exported SVG to `site/public/diagrams/`.
4. Reference the SVG from docs pages under `site/src/content/docs/`.

## Naming

Use stable, descriptive names:

- Source: `<topic>-<purpose>.excalidraw`
- Export: `<topic>-<purpose>.svg`

Example:

- `docs/diagrams/excalidraw/universal-manifest-overview.excalidraw`
- `site/public/diagrams/universal-manifest-overview.svg`
