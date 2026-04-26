# WO-0215: Extend Synthetic Monitoring to Full Resolver Contract Coverage

**Status:** COMPLETED — 6/8 status codes always-on + OPTIONS; full header contract assertions; SLO policy and playbook updated; actionlint clean
**Priority:** CRITICAL (P0)
**Depends on:** none
**Unblocks:** —
**Derived from:** 2026-04-26 resolver runtime drift scan, finding 1 (CRITICAL)

## Objective

Existing synthetic-monitoring workflows (`.github/workflows/synthetic-monitoring.yml`, `synthetic-monitoring-staging.yml`) probe latency only. Contract violations on error-status paths (304, 307, 410, 500, etc.) and header contract (ETag, Cache-Control, source headers, exposed headers) go undetected for hours. Wire the existing `packages/universal-manifest/scripts/smoke-endpoints.mjs` contract suite into the synthetic monitoring path so silent contract failures alert immediately.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/.github/workflows/synthetic-monitoring.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/synthetic-monitoring-staging.yml`
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/smoke-endpoints.mjs`
- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/CONTRACT.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0117-add-synthetic-monitoring-alerting-and-slo-policy.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0116-expand-resolver-test-suite-for-contract-coverage.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-resolver-runtime-drift-scan.md`

## Work to perform

1. **Inventory current monitoring coverage** — list which assertions the synthetic workflows currently make. Confirm by reading: latency only? Status 200 only? Anything about headers?
2. **Determine the right call shape** — `smoke-endpoints.mjs` likely supports an env var or flag for the resolver base URL. If not, add one (`--resolver-base=https://myum.net`) without changing existing CI users of the script.
3. **Extend the synthetic workflow** — replace or supplement the latency-only check with `npm run smoke:endpoints:prod` (or equivalent invocation). Capture the run output and surface failures with a useful alerting payload (workflow failure → notification).
4. **Cover all 8 contract status codes** — 200, 304, 307, 400, 404, 405, 410, 500. Add deterministic test fixtures or known-bad UMIDs that reliably exercise each status from the live resolver. Where the live resolver can't be safely poked into a 500, document it and skip with reason.
5. **Header assertions** — ETag, Cache-Control, source headers, CORS exposed headers. If `smoke-endpoints.mjs` doesn't already check these, extend it.
6. **SLO policy update** — `WO-0117` defines latency SLOs. Add error-path availability targets (per-status-class success rate). Cross-link.
7. **Escalation runbook** — short addition to the Phase 9 drift-recovery playbook (`docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md`) describing what to do when "contract violation detected" alerts fire.

## Files to modify

- `.github/workflows/synthetic-monitoring.yml` (primary)
- `.github/workflows/synthetic-monitoring-staging.yml` (parity with prod)
- `packages/universal-manifest/scripts/smoke-endpoints.mjs` (extend if needed)
- `packages/universal-manifest/package.json` (script entry if new)
- `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md` (escalation runbook section)
- `docs/workorders/WO-0117-add-synthetic-monitoring-alerting-and-slo-policy.md` (cross-link reference, do not rewrite)

## Constraints

- **Do not poke production into a true 500.** Use deterministic fixtures or skip with documentation.
- Do not add new secrets. If alerting needs a webhook, document the requirement; do not commit any token.
- Do not weaken the existing latency check.
- Do not commit, push, stage, or branch. Sibling commit agent owns git mutations.
- Run `git status --short` first; do not touch any file in their diff.

## Acceptance criteria

- Synthetic workflow asserts at least 6 of 8 contract status codes against the live resolver (or staging where prod can't be safely poked).
- Header contract assertions present and failing-loud on drift.
- SLO policy file (or its successor) references error-path availability targets.
- Playbook has an "alert: contract violation detected" subsection.
- Workflow YAML passes actionlint or equivalent.
- Existing latency check still present.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0215-result.md`
Blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0215-BLOCKED.md`

Report must include: before/after coverage table (status codes asserted), workflow YAML diff, smoke-endpoints.mjs diff if any, SLO policy reference, playbook subsection diff.
