# WO-0071 -- SessionStateIndicator + ScenarioDefinitionV2 Types

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-02-28
**Priority:** P1 (Phase 1 -- Foundation)
**Source:** Sandbox V2 UI Redesign Proposal, Tasks T3 and T8
**Tags:** [site], [sandbox], [component], [types]
**Blocks:** WO-0072, WO-0073, WO-0076
**Dependencies:** None
**Estimated effort:** 1 day
**Proposal:** `.dev/ai/proposals/2026-03-01-02-39-39Z-universalmanifest-sandbox-ui-redesign-proposal.md`

## Objective

Build the SessionStateIndicator component (a badge showing per-entity session state with animated transitions) and define the V2 type system (ScenarioDefinitionV2, EntityStateV2, SubjectState, ProtocolLensState) that extends the existing V1 types with backward compatibility.

## Why this work matters

The V1 sandbox tracked a single entity with a single status field. The V2 redesign manages two entities, each with its own session state progression (idle, connecting, handshake, verified, error). The SessionStateIndicator provides the visual representation, and the V2 types provide the data model that the engine and all components depend on.

## Scope

### Files created

- `site/src/components/sandbox/SessionStateIndicator.astro` -- Badge/pill component showing session state with color coding
- `site/src/scripts/sandbox/session-state.ts` -- Client-side logic: state rendering and animated transitions
- `site/src/styles/sandbox/session-state.css` -- Session state colors, transitions, and pulse animations

### Files modified

- `site/src/scripts/sandbox/types.ts` -- Added V2 types: `EntityStateV2`, `SubjectState`, `ProtocolLensState`, `ProtocolInteraction`, `ScenarioDefinitionV2`, `SandboxStateV2`

### V2 type system

- `EntityStateV2`: id, type (consumer/site/oracle/platform), name, did, sessionState (idle/connecting/handshake/verified/error), manifestJson, details, highlightedFields, status
- `SubjectState`: type, label, data, status (idle/in-transit/resolved/rejected)
- `ProtocolLensState`: interactions array, currentInteraction index, status (idle/running/complete)
- `ProtocolInteraction`: from, to, action, description, timestamp
- `ScenarioDefinitionV2`: extends V1 with optional entity A/B metadata, subject definition, session state progression, protocol interactions
- Backward compatible: existing V1 ScenarioDefinition scenarios still type-check

## Acceptance criteria

- [x] SessionStateIndicator displays all 5 states (idle, connecting, handshake, verified, error) with distinct colors.
- [x] State transitions trigger CSS animations.
- [x] ScenarioDefinitionV2 compiles with TypeScript.
- [x] Existing V1 ScenarioDefinition scenarios still type-check.
- [x] CSS uses `sb-ss-` prefix.
