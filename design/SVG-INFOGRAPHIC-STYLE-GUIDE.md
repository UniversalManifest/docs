# SVG Infographic Style Guide

This document specifies the **Headless SVG & Wrapper Pattern** required to ensure all infographics across the Universal Manifest project share a cohesive visual language and integrate correctly with the documentation aesthetics.

## The Objective
To create crisp, consistent, and beautiful infographics that perform perfectly across all browser types, don't clip text, and don't conflict with site-wide typography or theme settings. This document serves as the **Standard Operating Procedure (SOP) for AI Agents** generating new documentation SVGs.

## 1. The Headless SVG Pattern
Do **not** bake document headers, subtitles, or footer warnings into the SVG itself. 
The SVG must contain **only** the diagram geometry (nodes, edges, callouts).

### Wrapper Implementation
Instead of including text in the SVG, wrap the SVG with standard Markdown headers and blockquotes/alerts in the destination `.md` file.

**Correct Markdown Wrapper Example:**
```markdown
## Consuming Universal Manifests
The required 3-step pipeline to safely process, validate, and use a state capsule.

![Universal Manifest core flow pilot animation](/animations/um-core-flow-pilot.svg)

:::caution
Universal Manifests are **unsafe by default**. Always complete verification checks before projecting payload data.
:::
```

## 2. Canvas & Spacing Constraints (Rectangular Flow Chart Archetype)
When generating "Rectangular Flow Chart" style diagrams:
- **Canvas Size**: Fix the `viewBox` width tightly around the horizontal extent of the nodes, leaving a fixed margin of ~70px on the left and right edges. A typical 3-node row should use a `1060x320` canvas. Ensure `width="1060"` and `height="320"`. This prevents excessive border space and ensures text sizes beautifully on wide desktop screens and mobile.
- **Node Gaps**: Minimum gap between horizontally adjacent sibling nodes MUST be **160px**. No edge labels should overlap connection arrows. This is the most common reason for failure in standard LLM SVG generation.
- **Node Dimensions**: Typically `width="200"` and `height="200"`.
- **Typography & Spacing**: Use `font-family: system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, sans-serif;` with `letter-spacing: -0.01em;`.
- **Background**: Ensure the `rect` background of the SVG is `transparent` or `fill="none"` so it inherits the website background seamlessly. Do *not* hardcode a `#111` or dark background, as the website handles dark/light mode dynamically.

## 3. Visual Styling & Color Palette
Follow these strict CSS properties for SVGs to match the "Teacher Lens" Webby-quality examples:
- **Borders**: Nodes should have a `2px` stroke border (typically `var(--border): #e2e8f0`).
- **Rounding**: Apply `rx="16"` on node containers for soft corners.
- **Shadows**: Add a subtle `feDropShadow` (`#000000` at `0.06` opacity, `16px` blur) to node containers for depth.
- **Top Accents**: Add a thick `6px` colored stroke line at the top of the node inside its container (`stroke-linecap="round"`).

**Semantic Palettes (Tailwind-like):**
- **Blue (Resolve)**: `bg: #eff6ff`, `stroke: #3b82f6`, `text: #1d4ed8`
- **Amber (Verify)**: `bg: #fffbeb`, `stroke: #f59e0b`, `text: #b45309`
- **Emerald (Project)**: `bg: #ecfdf5`, `stroke: #10b981`, `text: #047857`

## 4. Animation Strategy (Resource Efficient)
Avoid animating `translateY` or position (no "bobbing"), as this is expensive for the browser and can clip text in grid layouts.
- **Static Nodes**: Nodes should fade in using CSS `opacity` (`@keyframes fade-in`). Map delays staggeringly (e.g., `delay: 0.1s`, `0.3s`, `0.5s`).
- **Edge Flow**: Use `stroke-dashoffset` over `stroke-dasharray` to simulate marching ants or flowing data on connector lines.
- **Accessibility**: Always wrap ALL animation CSS selectors in a `@media (prefers-reduced-motion: reduce)` block to disable animation and force opacity/transforms to default states if required by the user's OS.

## 5. Gold Standard Reference Template
Agents should use the following SVG as the structural basis for all new diagrams of the "Rectangular Flow Chart" archetype. Preserve the `<defs>`, `.box`, `.node-group`, and `@keyframes` exactly as written.

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1060 320" width="1060" height="320" role="img" aria-labelledby="title desc">
  <title id="title">Example Diagram</title>
  <desc id="desc">A description for accessibility.</desc>

  <defs>
    <style>
      :root {
        --bg: #ffffff;
        --ink: #0f172a;
        --muted: #64748b;
        --border: #e2e8f0;
        
        --blue-bg: #eff6ff; --blue-stroke: #3b82f6; --blue-text: #1d4ed8;
      }
      
      text {
        font-family: system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, sans-serif;
        letter-spacing: -0.01em;
      }
      
      .box { fill: var(--bg); stroke: var(--border); stroke-width: 2px; rx: 16px; }
      .label { font-size: 20px; font-weight: 700; fill: var(--ink); }
      .desc { font-size: 14px; font-weight: 400; fill: #475569; }
      .edge { stroke: #cbd5e1; stroke-width: 2px; fill: none; }
      .edge-label { font-size: 13px; font-weight: 600; fill: #64748b; }
      
      @keyframes fade-in { from { opacity: 0; } to { opacity: 1; } }
      @keyframes flow { from { stroke-dashoffset: 24; } to { stroke-dashoffset: 0; } }

      .edge-flow {
        stroke-dasharray: 8 4;
        animation: flow 1s linear infinite;
      }

      .node-group { animation: fade-in 0.6s ease-out both; }
      #node-1 { animation-delay: 0.1s; }
      #node-2 { animation-delay: 0.3s; }

      .edges { animation: fade-in 0.6s ease-out both; animation-delay: 0.5s; }

      @media (prefers-reduced-motion: reduce) {
        .node-group, .edges { animation: none !important; opacity: 1 !important; transform: none !important; }
        .edge-flow { animation: none !important; stroke-dasharray: none; }
      }
    </style>

    <filter id="shadow" x="-5%" y="-5%" width="120%" height="120%">
      <feDropShadow dx="0" dy="8" stdDeviation="16" flood-color="#000000" flood-opacity="0.06"/>
    </filter>

    <marker id="arrow-blue" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto">
      <path d="M 0 0 L 10 5 L 0 10 z" fill="var(--blue-stroke)" />
    </marker>
  </defs>

  <rect width="1060" height="320" fill="transparent" />

  <!-- Add edges and nodes here using the standard <g class="edges"> and <g class="node-group"> structures -->
</svg>
```
