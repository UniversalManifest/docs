# WO-0020 — RP1 source ingestion and synthesis materialization

**Status:** COMPLETED  
**Created:** 2026-02-20

## Objective

Convert the RP1 integration lane from documented intent into traceable K2B-ingested knowledge and executable Universal Manifest artifacts.

## Scope

In scope:
- identify authoritative RP1 source documents and ingest them through Stage -1/0.
- localize selected RP1 sources into the project corpus with provenance mappings.
- reconcile RP1-to-UM conflicts and record decisions.
- materialize at least one RP1-informed fixture and one RP1-informed proof journey delta.

Out of scope:
- normative spec changes without corresponding conformance/version policy updates.

## Deliverables

- updated source inventory/selection/provenance artifacts under:
  - `.dev/ai/knowledge-index/`
  - `.dev/ai/knowledge-corpus/`
  - `.dev/ai/ingestion/records/`
- RP1 fixture addition under:
  - `examples/`
- RP1 journey/proof update under:
  - `docs/journeys/`
- decisions/state synchronization:
  - `docs/DECISIONS.md`
  - `docs/STATE-OF-THE-PROJECT.md`

## Acceptance criteria

- [x] RP1 sources are selected/deferred/excluded with rationale and provenance mappings.
- [x] strict K2B validator remains PASS after RP1 ingestion updates.
- [x] at least one RP1 fixture is added and validated.
- [x] at least one RP1 proof/journey update is added.
- [x] any RP1 conflicts with UM architecture are explicitly resolved in ingestion records and decisions docs.

## Dependencies

- `integrations/rp1-spatial-fabric.md`
- `docs/reports/2026-02-20-master-forward-worklist.md`
- `.dev/ai/reports/2026-02-20-k2b-integration-completeness-report.md`

## Progress update (2026-02-20)

Completed in this batch:
- Stage -1/0 RP1 source intake executed with three selected captures from official RP1 domains.
- source selection, provenance map, and ingestion ledger updated for RP1 batch.
- triage record added:
  - `.dev/ai/ingestion/records/2026-02-20-rp1-stage0-triage.md`
- RP1 fixture added and validated:
  - `examples/v0.1/stubs/rp1-spatial-fabric-manifest.jsonld`
- RP1 journey definition added:
  - `docs/journeys/journey-07-rp1-spatial-fabric-projection.md`
- Journey index updated:
  - `docs/journeys/README.md`

Remaining:
- none for WO scope; follow-on enhancements continue under regular conformance/interoperability hardening tracks.

Conflict reconciliation evidence:
- `.dev/ai/ingestion/records/2026-02-18-cross-source-conflicts.md` (`CON-UM-007`)
