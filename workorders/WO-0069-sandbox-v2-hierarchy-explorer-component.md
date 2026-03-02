# WO-0069 -- HierarchyExplorer: Reusable Collapsible JSON Tree-View Component

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-02-28
**Priority:** P1 (Phase 1 -- Foundation)
**Source:** Sandbox V2 UI Redesign Proposal, Task T1
**Tags:** [site], [sandbox], [component]
**Blocks:** WO-0070, WO-0072, WO-0074
**Dependencies:** None (foundational component)
**Estimated effort:** 1.5 days
**Proposal:** `.dev/ai/proposals/2026-03-01-02-39-39Z-universalmanifest-sandbox-ui-redesign-proposal.md`

## Objective

Build a reusable collapsible tree-view component (HierarchyExplorer) for rendering any JSON/structured data as an interactive, expandable tree. This component is the shared rendering primitive used across all detail panels in the V2 sandbox layout.

## Why this work matters

The V1 sandbox displayed manifests as flat, syntax-highlighted JSON text. The V2 redesign requires an interactive tree view that lets users drill into nested structures, expand and collapse nodes, and understand manifest hierarchy at a glance. The HierarchyExplorer is used by DetailsCard, EntityColumn, and SubjectPanel -- it is the most reused component in the V2 architecture.

## Scope

### Files created

- `site/src/components/sandbox/HierarchyExplorer.astro` -- Astro shell with template and client script slot
- `site/src/scripts/sandbox/hierarchy-explorer.ts` -- Client-side logic: recursive tree rendering, expand/collapse state management, path highlighting, depth-limited rendering
- `site/src/styles/sandbox/hierarchy-explorer.css` -- Tree-view styles: indentation guides, expand/collapse icons, path highlights

### Capabilities

- Renders any JSON value (object, array, string, number, boolean, null) as a collapsible tree
- Supports expand/collapse at any node level
- Supports path highlighting (highlight a specific key path in the tree)
- Supports depth-limited rendering (collapse beyond N levels by default)
- Uses BEM naming with `sb-hx-` prefix

## Acceptance criteria

- [x] HierarchyExplorer renders a Universal Manifest JSON as a collapsible tree with at least 3 levels of nesting.
- [x] Expanding a node shows its children; collapsing hides them.
- [x] Array items display with array indices.
- [x] Component is reusable with no sandbox-specific logic baked in.
- [x] CSS uses `sb-hx-` prefix; no global style pollution.
