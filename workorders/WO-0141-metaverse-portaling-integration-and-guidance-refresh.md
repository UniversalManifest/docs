# WO-0141 — Metaverse Portaling Integration and Guidance Refresh

**Status:** COMPLETED  
**Created:** 2026-03-06  
**Updated:** 2026-03-06  
**Priority:** P1  
**Owner:** Metaverse Integration Lane  
**Source:** `/Users/grig/work/repo/universalmanifest/docs/explainers/metaverse-portaling.md`, `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`, `/Users/grig/work/repo/universalmanifest/docs/journeys/journey-09-metaverse-crossworld-projection.md`

## Objective

Make metaverse portaling an explicit first-class concept in the Universal Manifest repo: jumping between different platforms using a Universal Manifest to bring pointer-based content, identity, and policy state with you.

## Problem Statement

The repo already supported cross-world projection, but the portaling concept was mostly implicit. The existing language described projection and portability, yet it did not clearly say that the intended user experience is movement between different platforms where the Universal Manifest carries avatar, inventory, profile, and policy references into the destination environment.

## Scope

In scope:

- Define portaling clearly in the metaverse integration lane.
- Update journey and sandbox language so portaling is explicit in the proof and teaching surfaces.
- Integrate the existing `docs/explainers/metaverse-portaling.md` file into the tracked documentation set.
- Preserve the existing fixture and proof route without changing the UM core contract.

Out of scope:

- New normative spec fields.
- New metaverse-specific required registry keys.
- Claims that every destination platform must render all incoming content identically.

## Deliverables

- Portaling integration note:
  - `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-metaverse-portaling-integration-note.md`
- Updated metaverse lane docs:
  - `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/metaverse.md`
- Updated proof and teaching surfaces:
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/journey-09-metaverse-crossworld-projection.md`
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/README.md`
  - `/Users/grig/work/repo/universalmanifest/docs/explainers/metaverse-portaling.md`
  - `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/integration-lanes/il-03-metaverse-crossworld.ts`
  - `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/integration-lanes/il-03-metaverse-crossworld-v2.ts`
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs`

## Acceptance Criteria

- [x] Portaling is explicitly defined as cross-platform movement using UM as the portable envelope.
- [x] Existing metaverse guidance explains pointer resolution, consent enforcement, and graceful degradation during portaling.
- [x] Journey and sandbox surfaces use portaling language rather than relying only on “cross-world projection” wording.
- [x] No UM core schema change is introduced.
- [x] Local verification passes.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0126-metaverse-universal-manifest-go-now-execution-and-integration-pages.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0140-k2b-concept-integration-transfer-map.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-05-metaverse-universal-manifest-gap-and-implementation-report.md`

## Execution Notes

- Completed on 2026-03-06.
- Preserved the current architectural boundary: portaling is an integration concept built from existing UM primitives and runtime rules, not a new normative spec layer.
- Verification completed with package tests, journey proof, and site build.
