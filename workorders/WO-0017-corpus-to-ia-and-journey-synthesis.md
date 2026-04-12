# WO-0017 — Full-corpus to IA and journey synthesis execution

**Status:** COMPLETED
**Created:** 2026-02-18

## Objective

Convert the full selected corpus (including all previously deferred sources) into concrete, merged implementation outputs for:

1. docs/site information architecture,
2. first-time onboarding narrative,
3. user journeys and executable proof-plan sequencing.

This work order is the execution bridge between knowledge integration and productized adopter-facing assets.

## Scope

In scope:

- Apply conflict decisions from:
  - `.dev/ai/ingestion/records/2026-02-18-cross-source-conflicts.md`
- Produce IA deltas for overview/spec/integration/proof navigation and page intent.
- Produce journey backlog deltas (domain coverage + identity-method variants).
- Align workbench backlog with corpus-derived requirements.
- Update decisions and state docs with finalized outcomes.

Out of scope:

- Implementing full workbench UI (tracked by WO-0014)
- Completing all onboarding copy/testing (tracked by WO-0015)
- Shipping new normative spec version alone without conformance evidence

## Deliverables

- IA delta artifact:
  - Historical IA delta artifact referenced by this WO is not present in the current checkout.
- Journey expansion plan update:
  - `docs/journeys/README.md`
  - `docs/workorders/WO-0012-user-journeys-and-e2e-test-suite.md`
- Decisions/state updates:
  - `docs/DECISIONS.md`
  - `docs/STATE-OF-THE-PROJECT.md`

## Acceptance criteria

- [x] All conflict IDs `CON-UM-001` through `CON-UM-006` are reflected in at least one concrete artifact change.
- [x] IA documents include explicit first-time reader path and standards-neutral framing boundaries.
- [x] Journey plan includes cross-domain coverage and identity-method variants.
- [x] Workbench requirements explicitly include import/edit/validate/export behavior tied to conformance expectations.
- [x] Evidence links are present for every changed artifact.

## Execution Progress (2026-02-19T04:52:00Z)

Gap status movement from the historical K2B provenance audit captured during this execution pass:
- `GAP-K2B-001`: moved to CLOSED by the IA/materialization pass reflected in the surviving WO/journey artifacts.
- `GAP-K2B-002`: moved to CLOSED for planning-materialization by updates in:
  - `docs/journeys/README.md`
  - `docs/workorders/WO-0012-user-journeys-and-e2e-test-suite.md`
- `GAP-K2B-003`: moved to IN PROGRESS by corpus-derived requirement deltas in:
  - `docs/workorders/WO-0014-interactive-manifest-workbench.md`

Criterion-level evidence:
- Conflict coverage (`CON-UM-001`..`CON-UM-006`) evidence:
  - `docs/DECISIONS.md`
- IA first-time path + standards-neutral boundaries evidence:
  - `docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md`
- Journey expansion (cross-domain + identity variants) evidence:
  - `docs/journeys/README.md`
  - `docs/workorders/WO-0012-user-journeys-and-e2e-test-suite.md`
- Workbench requirement tie to conformance evidence:
  - `docs/workorders/WO-0014-interactive-manifest-workbench.md`

## Completion Evidence (2026-02-19T21:16:00Z)

Artifact evidence links:
- IA delta artifact:
  - Historical IA delta artifact referenced by this WO is not present in the current checkout.
- journey planning materialization:
  - `docs/journeys/README.md`
  - `docs/workorders/WO-0012-user-journeys-and-e2e-test-suite.md`
- onboarding alignment:
  - `docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md`
- workbench backlog hardening and implementation closure:
  - `docs/workorders/WO-0014-interactive-manifest-workbench.md`
- decisions and state synchronization:
  - `docs/DECISIONS.md`
  - `docs/STATE-OF-THE-PROJECT.md`
- execution reports:
  - Historical `.dev` execution reports referenced by this WO are not present in the current checkout.

## Dependencies

- Historical full-corpus synthesis artifact referenced by this WO is not present in the current checkout.
- `docs/workorders/WO-0014-interactive-manifest-workbench.md`
- `docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md`
- `docs/workorders/WO-0016-gas-index-scan-and-knowledge-integration-ledger.md`
