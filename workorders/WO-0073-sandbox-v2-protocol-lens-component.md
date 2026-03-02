# WO-0073 -- ProtocolLens: Step-by-Step Protocol Interaction Viewer

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-02-28
**Priority:** P2 (Phase 2 -- Panels)
**Source:** Sandbox V2 UI Redesign Proposal, Task T5
**Tags:** [site], [sandbox], [component]
**Blocks:** WO-0075
**Dependencies:** WO-0071 (V2 types with ProtocolLensState)
**Estimated effort:** 1.5 days
**Proposal:** `.dev/ai/proposals/2026-03-01-02-39-39Z-universalmanifest-sandbox-ui-redesign-proposal.md`

## Objective

Build the ProtocolLens component that occupies the upper portion of the center column in the V2 layout. It visualizes step-by-step protocol interactions between Entity A and Entity B as a message/sequence flow with directional arrows, entity labels, and action descriptions.

## Why this work matters

The V1 sandbox had a ProtocolPanel that showed step results and a checklist but did not visualize the back-and-forth protocol interaction between two parties. The ProtocolLens makes the protocol flow the focal point of the sandbox, showing how messages travel between entities during a handshake.

## Scope

### Files created

- `site/src/components/sandbox/ProtocolLens.astro` -- Astro shell for the protocol interaction sequence viewer
- `site/src/scripts/sandbox/protocol-lens.ts` -- Client-side logic: interaction rendering, directional arrows, step advancement, active highlight
- `site/src/styles/sandbox/protocol-lens.css` -- Message flow styles: arrows, entity labels, action descriptions, active step highlighting

### Capabilities

- Renders protocol interactions as a message flow between Entity A and Entity B
- Each interaction shows: source entity, target entity, action name, description
- Active interaction is highlighted as the scenario progresses
- Interactions accumulate as steps advance
- Falls back to a step-list view for V1 scenarios without protocol interaction data
- Uses BEM naming with `sb-pl-` prefix

## Acceptance criteria

- [x] ProtocolLens renders a sequence of protocol interactions with directional indicators.
- [x] Active interaction highlight moves as the scenario advances.
- [x] Interactions accumulate per step (previous interactions remain visible).
- [x] Falls back gracefully for V1 scenarios.
