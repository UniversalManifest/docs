# WO-0070 -- DetailsCard: Dual-Mode Detail Card with Hierarchy/JSON Toggle

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-02-28
**Priority:** P1 (Phase 1 -- Foundation)
**Source:** Sandbox V2 UI Redesign Proposal, Task T2
**Tags:** [site], [sandbox], [component]
**Blocks:** WO-0072, WO-0074
**Dependencies:** WO-0069 (HierarchyExplorer)
**Estimated effort:** 1 day
**Proposal:** `.dev/ai/proposals/2026-03-01-02-39-39Z-universalmanifest-sandbox-ui-redesign-proposal.md`

## Objective

Build a reusable card component (DetailsCard) that provides a consistent shell for all detail views in the V2 sandbox. Each card has a header (data-type label and title), a scrolling body, and a JSON toggle button that switches between two render modes: hierarchy (HierarchyExplorer tree view) and raw JSON (syntax-highlighted text).

## Why this work matters

The CEO mockup specifies that every detail panel (entity details, manifest explorer, subject details) uses the same card shell with a dual-mode toggle. This consistency makes the interface learnable and ensures all data views behave the same way. Without a shared DetailsCard, each panel would build its own bespoke UI.

## Scope

### Files created

- `site/src/components/sandbox/DetailsCard.astro` -- Astro shell with header, body slot, and JSON toggle button
- `site/src/scripts/sandbox/details-card.ts` -- Client-side logic: mode toggling between hierarchy and raw JSON, header rendering
- `site/src/styles/sandbox/details-card.css` -- Card styles: header, scrolling body, JSON toggle button, mode transition animations

### Capabilities

- Two render modes: hierarchy (uses HierarchyExplorer from WO-0069) and raw JSON (uses existing `highlight.ts`)
- Header displays a data-type label and a title
- Body scrolls when content exceeds viewport
- JSON toggle button at the bottom of the card
- Uses BEM naming with `sb-dc-` prefix

## Acceptance criteria

- [x] DetailsCard renders in hierarchy mode with HierarchyExplorer visible and JSON view hidden.
- [x] Clicking the JSON toggle switches to raw JSON mode.
- [x] Header shows the data-type label and title.
- [x] Body scrolls when content overflows.
- [x] Pattern is consistent across all detail views that use DetailsCard.
