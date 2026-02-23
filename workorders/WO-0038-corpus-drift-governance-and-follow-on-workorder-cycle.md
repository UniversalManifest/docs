# WO-0038 — Corpus drift governance and follow-on work-order cycle

**Status:** NOT_STARTED
**Created:** 2026-02-22
**Priority:** LOW
**Source:** `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`

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
   - `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md`
   - `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
   - `/Users/grig/work/repo/universalmanifest/.dev/ai/ingestion/GATES.md`
2. Baseline drift report in:
   - `/Users/grig/work/repo/universalmanifest/docs/reports/`
   - or `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/`
3. Follow-on WO trigger criteria documented in:
   - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`
   - or a dedicated governance doc referenced by the index

## Acceptance criteria

- [ ] Drift-check cadence and owner are documented.
- [ ] Recurring regression-verification checklist is documented with required commands.
- [ ] One baseline drift-check report is published with date, input set, and outcome.
- [ ] Clear threshold exists for when detected drift must become new WOs.
- [ ] If baseline run finds actionable drift, follow-on WOs are created and indexed.

## Validation commands

- `/opt/homebrew/bin/bash /Users/grig/.agents/scripts/validate-k2b-gates.sh /Users/grig/work/repo/universalmanifest --artifact-root /Users/grig/work/repo/universalmanifest/.dev/ai --strict`
- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`
- `curl -I https://universalmanifest.net/ && curl -I https://universalmanifest.net/getting-started/workbench/ && curl -I https://universalmanifest.net/proof/harness/`
- `rg -n '/harness/|/proof/|/getting-started/|/spec/|/conformance/|/workbench/|/integrations/' /Users/grig/work/repo/universalmanifest/site/src/content/docs --glob '*.md' | rg -v '\\]\\([^)]+'`
- `rg -n 'drift|follow-on|work order|threshold|cadence' /Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md /Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md /Users/grig/work/repo/universalmanifest/.dev/ai/ingestion/GATES.md`
