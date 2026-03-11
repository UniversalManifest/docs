# WO-0078 -- Getting Started Scenario Migration to V2 Format (GS-01 through GS-04)

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-02-28
**Priority:** P4 (Phase 4 -- Integration)
**Source:** Sandbox V2 UI Redesign Proposal, Task T11
**Tags:** [site], [sandbox], [scenarios]
**Blocks:** WO-0079
**Dependencies:** WO-0076 (SandboxEngineV2)
**Estimated effort:** 1.5 days
**Proposal:** `.dev/ai/proposals/2026-03-01-02-39-39Z-universalmanifest-sandbox-ui-redesign-proposal.md`

## Objective

Migrate the four Getting Started scenarios (GS-01 through GS-04) from V1 to V2 format, adding two-entity definitions (Entity A and Entity B), subject definitions, session state progressions, and protocol interactions for each scenario.

## Why this work matters

The Getting Started scenarios are the first thing new users see in the sandbox. Migrating them to V2 demonstrates the full two-entity protocol interaction that is the core value proposition of the V2 redesign.

## Scope

### Files created (V2 versions)

- `site/src/scripts/sandbox/scenarios/getting-started/gs-01-first-manifest-v2.ts`
- `site/src/scripts/sandbox/scenarios/getting-started/gs-02-manifest-with-facets-v2.ts`
- `site/src/scripts/sandbox/scenarios/getting-started/gs-03-forward-compatibility-v2.ts`
- `site/src/scripts/sandbox/scenarios/getting-started/gs-04-resolver-lookup-v2.ts`

### Scenario details

| Scenario | Entity A | Entity B | Subject |
|----------|----------|----------|---------|
| GS-01: First Manifest | Site (issuer) | Consumer (verifier) | Minimal manifest |
| GS-02: Manifest with Facets | Site (issuer) | Consumer (verifier) | Manifest with facets |
| GS-03: Forward Compatibility | Site (issuer, new version) | Consumer (older version) | Manifest with unknown fields |
| GS-04: Resolver Lookup | Resolver service | Consumer (requester) | Manifest fetched by UMID |

Each V2 scenario includes:
- Entity A and Entity B metadata (type, name, DID)
- Session state progression per step (idle -> connecting -> handshake -> verified)
- Protocol interactions describing the message flow
- Subject definition (what is being exchanged)

## Acceptance criteria

- [x] All four GS scenarios load and run in the V2 layout.
- [x] Entity A and Entity B are visible with correct types and names.
- [x] Protocol Lens shows interactions accumulating per step.
- [x] Subject panel shows the exchanged object and updates per step.
- [x] Session states progress correctly through the scenario.
