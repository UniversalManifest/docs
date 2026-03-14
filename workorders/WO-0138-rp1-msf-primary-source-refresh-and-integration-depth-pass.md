# WO-0138 — RP1/MSF Primary-Source Refresh and Integration-Depth Pass

**Status:** COMPLETED  
**Created:** 2026-03-06  
**Updated:** 2026-03-06  
**Priority:** P1  
**Owner:** Research Intake and Spatial Integration Architecture  
**Source:** `docs/reports/2026-03-06-omb-wiki-spatial-fabric-crosscheck.md`

## Objective

Refresh the RP1/MSF source corpus from primary repositories/specifications surfaced by the OMB crosscheck, then use those refreshed sources to deepen the RP1/MSF integration lane and related proof artifacts without changing the UM core contract.

## Problem Statement

The OMB audit concluded that the current UM architectural boundary for RP1/MSF remains correct, but the localized source corpus is too thin relative to the current spatial-fabric ecosystem map. The next gap is source completeness and integration depth, not core schema design.

## Scope

In scope:

- Localize additional primary RP1/MSF-adjacent sources surfaced by the OMB audit.
- Refresh provenance/ingestion records for the new source set.
- Deepen the RP1/MSF integration lane with better coverage of:
  - attachment-point composition,
  - primary vs secondary fabrics,
  - runtime-only presence vs portable manifest state,
  - asset/profile/tooling boundaries.
- Add one deeper non-normative example and one deeper proof artifact if justified by refreshed sources.

Out of scope:

- Core schema changes.
- Treating `omb.wiki` as the source of record.
- Promoting RP1/MSF semantics into normative UM requirements.

## Deliverables

- Refreshed source/provenance records under the repo intake lanes
- Updated RP1/MSF integration guidance under:
  - `integrations/rp1-spatial-fabric.md`
  - site mirror if applicable
- Follow-on fixture/journey or scenario update if justified by refreshed sources

## Acceptance Criteria

- [x] Additional RP1/MSF primary sources are localized with provenance.
- [x] The RP1/MSF integration lane is materially deeper while preserving the current core UM boundary.
- [x] Wiki-discovered concepts are promoted only after primary-source confirmation.
- [x] Any new proof artifact remains pointer-first, consent-gated, and non-normative.

## Dependencies

- `docs/workorders/WO-0136-omb-wiki-spatial-fabric-source-refresh-and-primary-source-crosscheck.md`
- `docs/reports/2026-03-06-omb-wiki-spatial-fabric-crosscheck.md`
- `docs/workorders/WO-0137-role-based-runtime-federation-and-bridge-guidance-refresh.md`

## Execution Notes

- Completed on 2026-03-06.
- Localized four additional primary RP1/MSF-adjacent sources:
  - `.dev/ai/knowledge-corpus/imports/external-29-manifolder-readme.md`
  - `.dev/ai/knowledge-corpus/imports/external-30-manifolder-data-model.md`
  - `.dev/ai/knowledge-corpus/imports/external-31-manifolder-client.md`
  - `.dev/ai/knowledge-corpus/imports/external-32-khronos-gltf-runtime-delivery.md`
- Refreshed provenance and ingestion records:
  - `.dev/ai/knowledge-corpus/SOURCE-MAP.md`
  - `.dev/ai/knowledge-index/CANDIDATE-SOURCES.md`
  - `.dev/ai/knowledge-index/SOURCE-SELECTION.md`
  - `.dev/ai/ingestion/LEDGER.md`
  - `.dev/ai/ingestion/records/2026-03-06-rp1-msf-source-refresh-stage0-triage.md`
- Deepened the RP1/MSF lane and proof/example surfaces:
  - `integrations/rp1-spatial-fabric.md`
  - `site/src/content/docs/integrations/rp1-spatial-fabric.md`
  - `examples/v0.1/stubs/rp1-spatial-fabric-manifest.jsonld`
  - `docs/journeys/journey-07-rp1-spatial-fabric-projection.md`
  - `packages/universal-manifest/scripts/run-journeys.mjs`
- Outcome:
  - the lane now explains parent/child scope composition and attachment points more concretely,
  - runtime-only vs portable-state boundaries are explicit,
  - asset delivery stays external-pointer-first,
  - no core UM schema change was introduced.
