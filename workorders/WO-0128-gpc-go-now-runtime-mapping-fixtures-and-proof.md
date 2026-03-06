# WO-0128 — GPC Go-Now Runtime Mapping, Fixtures, and Proof

**Status:** COMPLETED  
**Created:** 2026-03-06  
**Updated:** 2026-03-06  
**Priority:** P0  
**Owner:** Reference Implementation + Standards Integration  
**Source:** `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0127-gpc-standards-integration-review-and-gap-analysis.md`

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
   - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/src/index.ts`
2. GPC example/fixture pack:
   - `/Users/grig/work/repo/universalmanifest/examples/integrations/gpc/`
   - `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/gpc-evidence-projection-manifest.jsonld`
3. GPC validation coverage:
   - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/validate-gpc.mjs`
   - package script wiring in `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/package.json`
4. GPC journey proof:
   - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs`
   - `/Users/grig/work/repo/universalmanifest/docs/journeys/J21-gpc-runtime-signal-and-evidence-projection.md`
   - `/Users/grig/work/repo/universalmanifest/docs/journeys/README.md`
5. Registry/docs synchronization:
   - `/Users/grig/work/repo/universalmanifest/spec/v0.1/REGISTRY.md`
   - `/Users/grig/work/repo/universalmanifest/spec/v0.1/CONFORMANCE.md`

## Acceptance Criteria

- [x] Reference implementation exports a deterministic GPC normalization helper covering header, JS, and provenance branches.
- [x] Support-resource parsing rejects invalid shape/media assumptions and tolerates unknown members safely.
- [x] Optional GPC evidence projection can be expressed with UM consent/pointer structures without changing core required fields.
- [x] `npm test` covers the new GPC fixtures and passes.
- [x] `npm run journeys` includes a GPC journey row and passes.
- [x] Registry and conformance docs reflect the new non-normative GPC key family and proof coverage boundaries.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0127-gpc-standards-integration-review-and-gap-analysis.md`
- `/Users/grig/work/repo/universalmanifest/integrations/gpc-global-privacy-control.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/gpc-global-privacy-control.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-review-v3-gap-closed.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-integration-options-and-recommendation.md`

## Execution Progress (2026-03-06)

Started in this pass:

- WO created and marked `IN_PROGRESS`.
- Runtime/helper, fixture, journey, and docs synchronization implementation started immediately.

Completed in this pass:

- Added GPC runtime normalization, support-resource parsing, and evidence-projection helpers:
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/src/index.ts`
- Added GPC fixture pack:
  - `/Users/grig/work/repo/universalmanifest/examples/integrations/gpc/runtime/header-active.json`
  - `/Users/grig/work/repo/universalmanifest/examples/integrations/gpc/runtime/header-inactive.json`
  - `/Users/grig/work/repo/universalmanifest/examples/integrations/gpc/runtime/header-duplicate-active.json`
  - `/Users/grig/work/repo/universalmanifest/examples/integrations/gpc/runtime/js-only-active.json`
  - `/Users/grig/work/repo/universalmanifest/examples/integrations/gpc/runtime/no-signal-unknown.json`
  - `/Users/grig/work/repo/universalmanifest/examples/integrations/gpc/runtime/intermediary-active.json`
  - `/Users/grig/work/repo/universalmanifest/examples/integrations/gpc/support-resource/valid.json`
  - `/Users/grig/work/repo/universalmanifest/examples/integrations/gpc/support-resource/unknown-members.json`
  - `/Users/grig/work/repo/universalmanifest/examples/integrations/gpc/support-resource/invalid-last-update.json`
  - `/Users/grig/work/repo/universalmanifest/examples/integrations/gpc/support-resource/wrong-media-type.json`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/gpc-evidence-projection-manifest.jsonld`
- Added dedicated GPC validation harness and package wiring:
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/validate-gpc.mjs`
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/package.json`
- Added GPC journey proof and documentation:
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs`
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/J21-gpc-runtime-signal-and-evidence-projection.md`
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/README.md`
- Synchronized non-normative registry and conformance docs:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/REGISTRY.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/CONFORMANCE.md`
- Recorded governance/status updates:
  - `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
  - `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
  - `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md`
- Captured validation artifacts:
  - `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-gpc-go-now-npm-test.txt`
  - `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-gpc-go-now-journeys.txt`
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/_artifacts/2026-03-06T07-50-34-715Z-journey-report.json`

## Completion notes

- The GPC execution wave is now operational in the TypeScript reference implementation and proof suite.
- Core UM contract boundaries were preserved: GPC remains a non-normative integration lane with runtime-authoritative handling and optional document-level evidence projection.
