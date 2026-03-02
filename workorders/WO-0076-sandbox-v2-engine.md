# WO-0076 -- SandboxEngineV2: Two-Entity State Management with Subject and Protocol Lens

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-02-28
**Priority:** P3 (Phase 3 -- Layout + Engine)
**Source:** Sandbox V2 UI Redesign Proposal, Task T9
**Tags:** [site], [sandbox], [engine]
**Blocks:** WO-0077, WO-0078
**Dependencies:** WO-0071 (V2 types)
**Estimated effort:** 2 days
**Proposal:** `.dev/ai/proposals/2026-03-01-02-39-39Z-universalmanifest-sandbox-ui-redesign-proposal.md`

## Objective

Build the SandboxEngineV2 that extends the V1 engine with two-entity state management, subject state, protocol lens state, and per-entity session state transitions. The engine manages `SandboxStateV2` and emits events for component updates.

## Why this work matters

The V1 engine managed a single entity with a single status field. The V2 redesign requires independent state for two entities, a subject object, and a protocol lens -- all evolving per step. Without the V2 engine, the new components have no state management layer.

## Scope

### Files created

- `site/src/scripts/sandbox/engine-v2.ts` -- V2 engine: two-entity state, subject state, protocol lens state, session state transitions, event emission
- `site/src/scripts/sandbox/types-v2.ts` -- Additional V2 type exports (if not already in types.ts)

### Capabilities

- Manages `SandboxStateV2` with `entityA`, `entityB`, `subject`, and `protocolLens` fields
- Per-entity session state transitions (idle -> connecting -> handshake -> verified or error)
- Subject state transitions (idle -> in-transit -> resolved or rejected)
- Protocol lens interaction accumulation per step
- Detects V1 vs V2 scenarios and provides sensible defaults (V1 scenarios use single entity mode)
- V1 engine methods preserved for backward compatibility
- Emits state change events for component reactivity

## Acceptance criteria

- [x] Engine manages two entities independently with separate session states.
- [x] Subject state updates per step as the protocol progresses.
- [x] Protocol lens interactions accumulate as steps advance.
- [x] V1 scenarios still work with sensible defaults (single entity, no subject, step-list fallback).
- [x] Engine emits events that components can subscribe to for updates.
