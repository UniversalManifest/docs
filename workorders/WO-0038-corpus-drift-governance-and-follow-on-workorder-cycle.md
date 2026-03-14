# WO-0038 — Corpus drift governance and follow-on work-order cycle

**Status:** COMPLETED
**Created:** 2026-02-22
**Priority:** LOW
**Source:** `docs/STATE-OF-THE-PROJECT.md`

## Objective

Operationalize recurring corpus drift checks and codify when drift requires opening new follow-on work orders.

## Why this work matters

Current state calls for ongoing drift checks when newly ingested sources affect adopter-facing IA or proof flows. This work is currently advisory and needs explicit repeatable procedure ownership.

## Scope

In scope:

- Define repeatable drift-check cadence and command sequence.
- Standardize report output location/format for drift-check runs.
- Define explicit thresholds for creating new WOs from detected drift.
- Include periodic completion-claim regression checks (routes, journeys, label-first link hygiene) in the same governance cadence.
- Execute one baseline drift-check run under the new process.

Out of scope:

- Full re-ingestion of external corpus in this WO.
- Major IA/spec rewrites not triggered by actual detected drift.

## Required deliverables

1. Drift-check runbook update in one of:
   - `docs/CRITICAL-PATH.md`
   - `docs/STATE-OF-THE-PROJECT.md`
   - `.dev/ai/ingestion/GATES.md`
2. Baseline drift report in:
   - `docs/reports/`
   - or `.dev/ai/reports/`
3. Follow-on WO trigger criteria documented in:
   - `docs/workorders/WO-INDEX.md`
   - or a dedicated governance doc referenced by the index

## Acceptance criteria

- [x] Drift-check cadence and owner are documented.
- [x] Recurring regression-verification checklist is documented with required commands.
- [x] One baseline drift-check report is published with date, input set, and outcome.
- [x] Clear threshold exists for when detected drift must become new WOs.
- [x] If baseline run finds actionable drift, follow-on WOs are created and indexed. (No new actionable failures found in baseline run.)

## Validation commands

- `/opt/homebrew/bin/bash /Users/grig/.agents/scripts/validate-k2b-gates.sh  --artifact-root .dev/ai --strict`
- `cd packages/universal-manifest && npm run journeys`
- `curl -I https://universalmanifest.net/ && curl -I https://universalmanifest.net/getting-started/workbench/ && curl -I https://universalmanifest.net/proof/harness/`
- `rg -n '/harness/|/proof/|/getting-started/|/spec/|/conformance/|/workbench/|/integrations/' site/src/content/docs --glob '*.md' | rg -v '\\]\\([^)]+'`
- `rg -n 'drift|follow-on|work order|threshold|cadence' docs/STATE-OF-THE-PROJECT.md docs/CRITICAL-PATH.md .dev/ai/ingestion/GATES.md`

## Completion evidence (2026-02-22)

- Baseline run report:
  - `docs/reports/2026-02-22-wo-0038-drift-governance-baseline-report.md`
- Runbook and index updates:
  - `docs/CRITICAL-PATH.md` (Phase 9)
  - `docs/workorders/WO-INDEX.md` (trigger criteria reference)
