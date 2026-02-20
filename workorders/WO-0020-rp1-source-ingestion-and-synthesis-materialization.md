# WO-0020 — RP1 source ingestion and synthesis materialization

**Status:** NOT_STARTED  
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
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-index/`
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/`
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/ingestion/records/`
- RP1 fixture addition under:
  - `/Users/grig/work/repo/universalmanifest/examples/`
- RP1 journey/proof update under:
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/`
- decisions/state synchronization:
  - `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
  - `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`

## Acceptance criteria

- [ ] RP1 sources are selected/deferred/excluded with rationale and provenance mappings.
- [ ] strict K2B validator remains PASS after RP1 ingestion updates.
- [ ] at least one RP1 fixture is added and validated.
- [ ] at least one RP1 proof/journey update is added.
- [ ] any RP1 conflicts with UM architecture are explicitly resolved in ingestion records and decisions docs.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/integrations/rp1-spatial-fabric.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-20-master-forward-worklist.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/2026-02-20-k2b-integration-completeness-report.md`

