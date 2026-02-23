# WO-0031 — Journey proof parity and decoupling hardening

**Status:** COMPLETED
**Created:** 2026-02-22
**Priority:** HIGH
**Source:** `/Users/grig/work/repo/universalmanifest/.dev/ai/audits/COMPLETION-AUDIT-2026-02-22-08-21-10Z.md`

## Objective

Close high-severity audit drift in the proof system by making journey evidence traceable one-to-one with documented journey IDs and removing hardcoded cross-repo path coupling from the journey runner.

## Why this matters

Current proof reporting claims success but does not emit per-journey execution for all documented journey IDs (`J01` through `J11`). It also hardcodes a reference implementation repository path, which weakens the decoupled-project claim and reproducibility for external adopters.

## Findings addressed

1. **High: Journey traceability drift**
   - `docs/journeys/README.md` documents 11 journeys and states each journey has a corresponding executable test step.
   - `packages/universal-manifest/scripts/run-journeys.mjs` currently emits `J01`, `J02`, `J03`, `J04`, `J05`, `J10`, `J11` only.
   - Latest artifact confirms 7-pass summary, not explicit per-step records for `J06`-`J09`.

2. **High: Decoupling drift**
   - `packages/universal-manifest/scripts/run-journeys.mjs` hardcodes reference implementation path:
     - `/Users/grig/work/repo/reference-platform`
   - This is non-portable and ties proof execution to a local machine path outside this repo.

## Scope

In scope:
- align journey docs and journey runner output contract.
- ensure each documented journey ID is represented in executable output.
- remove hardcoded absolute reference implementation path dependency from journey runner.
- preserve optional reference implementation smoke semantics while making path configurable.

Out of scope:
- redesigning journey semantics beyond parity and portability hardening.

## Required deliverables

1. Journey output contract hardening in:
   - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs`
2. Journey documentation alignment in:
   - `/Users/grig/work/repo/universalmanifest/docs/journeys/README.md`
3. Evidence artifact from updated runner:
   - `/Users/grig/work/repo/universalmanifest/docs/journeys/_artifacts/<timestamp>-journey-report.json`
4. Work order completion evidence note in this file.

## Acceptance criteria

- [x] Runner emits explicit records for all documented IDs (`J01`..`J11`) or docs are updated to exactly match emitted IDs and mapping rationale.
- [x] If multiple docs journeys are covered by one shared implementation function, the output still contains explicit per-ID pass/fail rows with deterministic evidence fields.
- [x] `J05` reference implementation smoke path is configurable (env var or CLI arg) and defaults to portable behavior when reference implementation repo is unavailable.
- [x] No hardcoded machine-specific reference implementation path remains in journey runner source.
- [x] `npm run journeys` passes and writes a report showing aligned journey coverage.
- [x] `docs/journeys/README.md` clearly states execution mapping and optional prerequisites.

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`
- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test`
- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`

## Notes

Any deliberate aggregation of journey logic is acceptable only if evidence remains per-journey and auditable.

## Completion evidence (2026-02-22)

- Runner hardening completed in:
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs`
    - explicit `J01`..`J11` journey rows now emitted
    - `J05` reference implementation smoke is configurable via `optional smoke flag` and `optional smoke path` (or CLI args `--optional-smoke`, `--optional-smoke-path`)
    - hardcoded reference implementation absolute path removed
- Journey documentation alignment completed in:
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/README.md`
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/journey-05-um-edge-to-display-smoke.md`
- Evidence artifact:
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/_artifacts/2026-02-22T22-55-37-227Z-journey-report.json`
- Validation results:
  - `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys` -> PASS (`J01`..`J11`)
  - `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test` -> PASS
  - `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean` -> PASS
