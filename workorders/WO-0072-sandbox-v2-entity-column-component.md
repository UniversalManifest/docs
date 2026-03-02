# WO-0072 -- EntityColumn: Symmetrical Entity Panel with Session State and Manifest Explorer

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-02-28
**Priority:** P2 (Phase 2 -- Panels)
**Source:** Sandbox V2 UI Redesign Proposal, Task T4
**Tags:** [site], [sandbox], [component]
**Blocks:** WO-0075
**Dependencies:** WO-0070 (DetailsCard), WO-0071 (SessionStateIndicator + V2 types)
**Estimated effort:** 1.5 days
**Proposal:** `.dev/ai/proposals/2026-03-01-02-39-39Z-universalmanifest-sandbox-ui-redesign-proposal.md`

## Objective

Build the EntityColumn component that replaces the V1 EntityPanel. Each EntityColumn represents one side of a protocol interaction (Entity A on the left, Entity B on the right) and contains: entity type badge, SessionStateIndicator, entity DetailsCard, and manifest DetailsCard (with HierarchyExplorer). The component is parameterized so it can be instantiated for either entity.

## Why this work matters

The CEO mockup specifies a symmetrical two-entity layout. The V1 sandbox had a single EntityPanel on the left. The V2 EntityColumn provides independent state, details, and manifest exploration for each entity, making it possible to show both sides of a protocol interaction simultaneously.

## Scope

### Files created

- `site/src/components/sandbox/EntityColumn.astro` -- Full entity column: type badge, session state, entity details card, manifest details card
- `site/src/scripts/sandbox/entity-column.ts` -- Client-side logic: entity data binding, manifest loading, state updates

### Capabilities

- Parameterized for Entity A or Entity B (different accent colors)
- Entity type badge (consumer, site, oracle, platform)
- SessionStateIndicator showing current session state
- Entity details in a DetailsCard with dual-mode (hierarchy/JSON)
- Manifest explorer in a DetailsCard with dual-mode (hierarchy/JSON)
- Vertical stack layout within the column

## Acceptance criteria

- [x] EntityColumn renders entity type badge, session state, details card, and manifest card in a vertical stack.
- [x] Entity A and Entity B use different accent colors for visual differentiation.
- [x] Both DetailsCards support hierarchy/JSON toggle independently.
- [x] Component renders correctly when instantiated for either entity.
