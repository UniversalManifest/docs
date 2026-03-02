# WO-0075 -- SandboxLayoutV2: New CSS Grid Layout with Header Transport Controls

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-02-28
**Priority:** P3 (Phase 3 -- Layout + Engine)
**Source:** Sandbox V2 UI Redesign Proposal, Task T7
**Tags:** [site], [sandbox], [layout]
**Blocks:** WO-0077
**Dependencies:** WO-0072 (EntityColumn), WO-0073 (ProtocolLens), WO-0074 (SubjectPanel)
**Estimated effort:** 1 day
**Proposal:** `.dev/ai/proposals/2026-03-01-02-39-39Z-universalmanifest-sandbox-ui-redesign-proposal.md`

## Objective

Build the SandboxLayoutV2 component that replaces the V1 three-panel layout with the new CSS Grid layout matching the CEO's Excalidraw mockup: Entity A (left, ~25%), center column split between ProtocolLens (top) and SubjectPanel (bottom, ~50%), Entity B (right, ~25%). Move step transport controls from the footer to the header bar.

## Why this work matters

The V1 layout was a single-entity three-panel design (entity, consumer, protocol). The V2 layout is a symmetrical two-entity design with a center column for protocol and subject. This is the spatial framework that all V2 components compose into.

## Scope

### Files created

- `site/src/components/sandbox/SandboxLayoutV2.astro` -- New Astro layout component with CSS Grid named areas

### Files modified or extended

- `site/src/styles/sandbox/layout-v2.css` -- New CSS Grid layout with 5 named areas (entity-a, protocol-lens, subject, entity-b, header)
- `site/src/styles/sandbox/responsive-v2.css` -- Responsive breakpoints: desktop (1440px, 3-column), tablet (1024px, stacked), mobile (375px, single column)

### Layout structure

```
+-----------------------------------------------------------------------+
| HEADER: [<- BACK] [SCENARIO TITLE]           [STEP TRANSPORT CONTROLS]|
+-----------------------------------------------------------------------+
|  ENTITY A (25%)   |   CENTER (50%)    |  ENTITY B (25%)               |
|                   |  PROTOCOL LENS    |                               |
|                   |  (top ~40%)       |                               |
|                   +-------------------+                               |
|                   |  SUBJECT          |                               |
|                   |  (bottom ~60%)    |                               |
+-----------------------------------------------------------------------+
```

### Capabilities

- CSS Grid with named areas
- Header contains back link, scenario title, and step transport controls
- No footer (controls moved to header)
- Responsive: stacks entity columns vertically on narrow screens
- New CSS custom properties: `--sb-entity-b-accent`, `--sb-subject-accent`, `--sb-protocol-lens-accent`

## Acceptance criteria

- [x] Layout renders 5 named grid areas correctly at desktop width.
- [x] Transport controls appear in the header, not the footer.
- [x] Responsive layout stacks correctly at tablet (1024px) and mobile (375px) widths.
- [x] New CSS custom properties are defined and used by child components.
- [x] All existing CSS custom properties preserved.
