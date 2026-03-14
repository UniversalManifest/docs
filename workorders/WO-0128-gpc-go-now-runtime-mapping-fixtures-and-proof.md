# WO-0128 — GPC Go-Now Runtime Mapping, Fixtures, and Proof

**Status:** COMPLETED  
**Created:** 2026-03-06  
**Updated:** 2026-03-06  
**Priority:** P0  
**Owner:** Reference Implementation + Standards Integration  
**Source:** `docs/workorders/WO-0127-gpc-standards-integration-review-and-gap-analysis.md`

## Objective

Execute the immediate GPC Go-Now implementation wave in the TypeScript reference implementation and proof surfaces, following the completed standards review and published integration lane.

## Problem Statement

Universal Manifest now has a standards-aligned GPC review and non-normative integration guidance, but it still lacks executable reference behavior for runtime signal normalization, support-resource parsing, fixture coverage, and journey-level proof. Without that implementation wave, the GPC integration remains descriptive rather than operational.

## Scope

In scope:

- Add runtime-authoritative GPC normalization helpers to the TypeScript reference implementation.
- Add `/.well-known/gpc.json` support-resource parsing helpers.
- Add optional projection helpers for GPC evidence into UM consent/pointer structures.
- Add GPC fixtures covering runtime, support-resource, and manifest-projection evidence cases.
- Add executable validation and journey proof for GPC integration behavior.
- Synchronize non-normative registry/conformance/docs status where the new execution wave creates durable surface area.

Out of scope:

- Promotion of GPC behavior into normative v0.1 or v0.2 conformance requirements.
- Legal interpretation beyond the bounded scope already documented in WO-0127 outputs.
- Browser or resolver production deployment changes unrelated to reference proof.

## Deliverables

1. GPC runtime normalization helpers in:
   - `packages/universal-manifest/src/index.ts`
2. GPC example/fixture pack:
   - `examples/integrations/gpc/`
   - `examples/v0.1/stubs/gpc-evidence-projection-manifest.jsonld`
3. GPC validation coverage:
   - `packages/universal-manifest/scripts/validate-gpc.mjs`
   - package script wiring in `packages/universal-manifest/package.json`
4. GPC journey proof:
   - `packages/universal-manifest/scripts/run-journeys.mjs`
   - `docs/journeys/J21-gpc-runtime-signal-and-evidence-projection.md`
   - `docs/journeys/README.md`
5. Registry/docs synchronization:
   - `spec/v0.1/REGISTRY.md`
   - `spec/v0.1/CONFORMANCE.md`

## Acceptance Criteria

- [x] Reference implementation exports a deterministic GPC normalization helper covering header, JS, and provenance branches.
- [x] Support-resource parsing rejects invalid shape/media assumptions and tolerates unknown members safely.
- [x] Optional GPC evidence projection can be expressed with UM consent/pointer structures without changing core required fields.
- [x] `npm test` covers the new GPC fixtures and passes.
- [x] `npm run journeys` includes a GPC journey row and passes.
- [x] Registry and conformance docs reflect the new non-normative GPC key family and proof coverage boundaries.

## Dependencies

- `docs/workorders/WO-0127-gpc-standards-integration-review-and-gap-analysis.md`
- `integrations/gpc-global-privacy-control.md`
- `site/src/content/docs/integrations/gpc-global-privacy-control.md`
- `.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-review-v3-gap-closed.md`
- `.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-integration-options-and-recommendation.md`

## Execution Progress (2026-03-06)

Started in this pass:

- WO created and marked `IN_PROGRESS`.
- Runtime/helper, fixture, journey, and docs synchronization implementation started immediately.

Completed in this pass:

- Added GPC runtime normalization, support-resource parsing, and evidence-projection helpers:
  - `packages/universal-manifest/src/index.ts`
- Added GPC fixture pack:
  - `examples/integrations/gpc/runtime/header-active.json`
  - `examples/integrations/gpc/runtime/header-inactive.json`
  - `examples/integrations/gpc/runtime/header-duplicate-active.json`
  - `examples/integrations/gpc/runtime/js-only-active.json`
  - `examples/integrations/gpc/runtime/no-signal-unknown.json`
  - `examples/integrations/gpc/runtime/intermediary-active.json`
  - `examples/integrations/gpc/support-resource/valid.json`
  - `examples/integrations/gpc/support-resource/unknown-members.json`
  - `examples/integrations/gpc/support-resource/invalid-last-update.json`
  - `examples/integrations/gpc/support-resource/wrong-media-type.json`
  - `examples/v0.1/stubs/gpc-evidence-projection-manifest.jsonld`
- Added dedicated GPC validation harness and package wiring:
  - `packages/universal-manifest/scripts/validate-gpc.mjs`
  - `packages/universal-manifest/package.json`
- Added GPC journey proof and documentation:
  - `packages/universal-manifest/scripts/run-journeys.mjs`
  - `docs/journeys/J21-gpc-runtime-signal-and-evidence-projection.md`
  - `docs/journeys/README.md`
- Synchronized non-normative registry and conformance docs:
  - `spec/v0.1/REGISTRY.md`
  - `spec/v0.1/CONFORMANCE.md`
- Recorded governance/status updates:
  - `docs/DECISIONS.md`
  - `docs/STATE-OF-THE-PROJECT.md`
  - `docs/CRITICAL-PATH.md`
- Captured validation artifacts:
  - `docs/reports/2026-03-06-gpc-go-now-npm-test.txt`
  - `docs/reports/2026-03-06-gpc-go-now-journeys.txt`
  - `docs/journeys/_artifacts/2026-03-06T07-50-34-715Z-journey-report.json`

## Completion notes

- The GPC execution wave is now operational in the TypeScript reference implementation and proof suite.
- Core UM contract boundaries were preserved: GPC remains a non-normative integration lane with runtime-authoritative handling and optional document-level evidence projection.
