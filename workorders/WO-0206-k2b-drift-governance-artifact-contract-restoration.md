# WO-0206 -- K2B Drift-Governance Artifact Contract Restoration

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-04-24
**Completed:** 2026-04-24
**Owner:** K2B governance follow-up
**Source:** Phase 9 mandatory command failure in `docs/CRITICAL-PATH.md`

## Objective

Restore or explicitly update the K2B drift-governance artifact contract required by the Phase 9 strict gate.

## Context

Phase 9 requires this command before completion claims or milestone closure statements:

```bash
bash ~/.agents/scripts/validate-k2b-gates.sh <repo-root> --artifact-root .dev/ai --strict
```

The gate failed because required `.dev/ai` artifact-root files are missing in the current checkout. This work order records the required follow-up without fabricating historical artifacts or treating the broader completion queue as unblocked.

Fresh run recorded on 2026-04-24:

- Command: `bash ~/.agents/scripts/validate-k2b-gates.sh /Users/grig/work/repo/universalmanifest --artifact-root .dev/ai --strict`
- Result: 0 pass, 12 warn, 13 fail.

Missing strict-gate requirements observed in the current checkout:

- `.dev/ai/knowledge-index/PROJECT-MASTER-INDEX.md`
- `.dev/ai/knowledge-index/SOURCE-SELECTION.md`
- `.dev/ai/knowledge-index/MATERIALIZATION-MODE.md`
- `.dev/ai/reports/K2B-BOOTSTRAP-REPORT-*.md`
- `.dev/ai/reports/K2B-DECISION-AUDIT-*.md`
- `.dev/ai/ingestion/LEDGER.md`
- `.dev/ai/ingestion/records/`
- `.dev/ai/reports/extraction-inventory.md`
- `.dev/ai/research/RESEARCH-INDEX.md`
- specification markdown files in the expected K2B synthesis directories
- validation report in the expected K2B validation locations
- build extraction file in the expected K2B build-extraction locations
- `.dev/ai/workorders/WO-INDEX.md`

Additional warnings also showed absent or unevaluable Stage -1 and gate-tracking artifacts, including `.dev/ai/knowledge-index/CANDIDATE-SOURCES.md`, `.dev/ai/ingestion/GATES.md`, and reconciliation/research tracking markers.

## Resolution

The K2B artifact contract was restored from legitimate git history: commit `3eef43b` (`chore: add AI orchestration, audit, handoff, and post-deploy verification logs`), the last historical source found before commit `3f30d6b` removed internal AI orchestration state from the public spec tree.

Restored artifact families:

- `.dev/ai/knowledge-index/`
- `.dev/ai/knowledge-corpus/`
- `.dev/ai/ingestion/`
- `.dev/ai/research/`
- `.dev/ai/reports/K2B-BOOTSTRAP-REPORT-2026-02-17-21-19-44.md`
- `.dev/ai/reports/K2B-DECISION-AUDIT-2026-02-19-01-27-20.md`
- `.dev/ai/reports/extraction-inventory.md`
- `.dev/ai/reports/validation-report.md`
- `.dev/ai/reports/build-extraction.md`
- `.dev/ai/workorders/`
- `.dev/ai/decisions/`
- `.dev/ai/specs/`

The restored index, source-map, and ledger metadata were path-normalized to current absolute local evidence paths so the strict gate can verify real files in this checkout rather than historical placeholders, `~` paths, URLs, or removed local-download paths.

Completion run recorded on 2026-04-24:

- `bash ~/.agents/scripts/validate-k2b-gates.sh /Users/grig/work/repo/universalmanifest --artifact-root .dev/ai --strict` -- PASS, 41 pass, 0 warn, 0 fail.
- `cd packages/universal-manifest && npm run journeys` -- PASS, preflight 1 pass, journeys 23 pass, 0 fail.
- `curl -I -s https://universalmanifest.net/` -- 200.
- `curl -I -s https://universalmanifest.net/getting-started/workbench/` -- 200.
- `curl -I -s https://universalmanifest.net/proof/harness/` -- 200.
- Docs link-hygiene scan -- no findings.

## Scope

In scope:

1. Identify the exact `.dev/ai` files and directories required by the current strict K2B gate.
2. Determine whether the contract should be restored from legitimate source history/storage or updated to match the surviving governance artifacts in the repo.
3. Apply the approved restoration or contract update.
4. Re-run the Phase 9 mandatory command set and record the result honestly.
5. Update status documents only after the gate behavior is verified.

Out of scope:

- fabricating missing `.dev/ai` artifacts
- reopening K2B research or concept-integration scope
- changing package, example, or site implementation files
- making completion or milestone-closure claims while the strict K2B gate remains failing

## Blocker

Resolved. A legitimate artifact source was identified in git history and the restored/path-normalized artifact contract now passes the strict K2B gate.

## Deliverables

- Verified artifact-contract decision: restore from legitimate source, or update the gate contract.
- Phase 9 command result notes, including the strict K2B gate outcome.
- Minimal status/index updates reflecting the verified outcome.

## Dependencies

- `docs/CRITICAL-PATH.md` Phase 9 mandatory command set.
- `~/.agents/scripts/validate-k2b-gates.sh`.
- Existing or approved replacement source for required `.dev/ai` artifact-root files.

## Acceptance Criteria

- [x] The missing K2B artifact-root requirements are listed explicitly.
- [x] No missing artifact is recreated without a legitimate source or approved contract change.
- [x] The strict K2B gate passes, or the approved contract change is documented and the replacement gate passes.
- [x] The remaining Phase 9 mandatory commands are run before any completion claim.
- [x] `docs/CRITICAL-PATH.md`, `docs/STATE-OF-THE-PROJECT.md`, and `docs/workorders/WO-INDEX.md` no longer contradict the verified gate state.
