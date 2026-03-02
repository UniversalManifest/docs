# WO-0077 -- Scenario Detail Page Rewrite: Wire V2 Layout, Components, and Engine

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-02-28
**Priority:** P4 (Phase 4 -- Integration)
**Source:** Sandbox V2 UI Redesign Proposal, Task T10
**Tags:** [site], [sandbox], [integration]
**Blocks:** WO-0079, WO-0080
**Dependencies:** WO-0075 (SandboxLayoutV2), WO-0076 (SandboxEngineV2)
**Estimated effort:** 2 days
**Proposal:** `.dev/ai/proposals/2026-03-01-02-39-39Z-universalmanifest-sandbox-ui-redesign-proposal.md`

## Objective

Rewrite the scenario detail page (`site/src/pages/sandbox/[...scenario].astro`) to use the V2 layout, components, and engine. The page detects whether a scenario is V1 or V2 and renders the appropriate layout, wiring all V2 components (EntityColumn, ProtocolLens, SubjectPanel) to the V2 engine's state management.

## Why this work matters

This is the integration work order that connects all the V2 foundation components (WO-0069 through WO-0076) into a working page. Without this, the components exist in isolation but are not wired together.

## Scope

### Files modified

- `site/src/pages/sandbox/[...scenario].astro` -- Complete rewrite of layout composition and client-side wiring to support both V1 and V2 scenarios

### Integration points

- Detects V1 vs V2 scenario format
- V2 scenarios: renders SandboxLayoutV2 with EntityColumn (A and B), ProtocolLens, SubjectPanel
- V1 scenarios: renders in backward-compatible mode (Entity A only, no Entity B, no subject, step-list fallback in ProtocolLens)
- Wires engine-v2 events to component updates
- Step transport controls in header
- Keyboard navigation (arrow keys, space, escape) preserved

## Acceptance criteria

- [x] V2 scenarios render with Entity A, Entity B, ProtocolLens, and SubjectPanel.
- [x] V1 scenarios render in backward-compatible mode without errors.
- [x] Step transport controls work from the header.
- [x] Keyboard navigation works for step advancement and scenario reset.
- [x] No JavaScript errors in the browser console for either V1 or V2 scenarios.
