# WO-0237: Add Reachability Assertion to Staging Smoke Gate

**Status:** COMPLETED 2026-04-26 — verify_staging now probes ${DOCS_BASE}/ and ${RESOLVER_BASE}/health with curl --max-time 30; fails fast on non-2xx; resolver /health confirmed extant at services/myum-resolver/src/index.ts:436-441; runbook documents Reachability Gate
**Priority:** HIGH (P1)
**Depends on:** none (independent of WO-0232/0234 file scope; touches staging-base script + runbook)
**Unblocks:** —
**Derived from:** 2026-04-26 deployment pipeline drift scan, finding (HIGH) — staging gate resolves base URLs but doesn't probe them before promotion

## Objective

The staging gate selects target URLs via `select-staging-bases.mjs` but never verifies the resolved targets are actually reachable before promotion proceeds. Add explicit reachability probes against the docs site root and the resolver health endpoint, fail `verify_staging` on probe failure.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/site/scripts/select-staging-bases.mjs` (or wherever the script lives — find it via grep)
- `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml` (the `verify_staging` job)
- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/` (find `/health` endpoint or equivalent contract)
- `/Users/grig/work/repo/universalmanifest/docs/site/STAGING-PROMOTION-RUNBOOK.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-deployment-pipeline-drift-scan.md` (finding 6)

## Work to perform

1. After `select-staging-bases.mjs` resolves `DOCS_BASE` and `RESOLVER_BASE`, add curl probes:
   - `curl -fsS -o /dev/null --max-time 30 "${DOCS_BASE}/"` — site root must return 2xx.
   - `curl -fsS -o /dev/null --max-time 30 "${RESOLVER_BASE}/health"` — resolver health endpoint must return 2xx.
2. Capture HTTP status + timing in workflow output for diagnostics.
3. Fail `verify_staging` if any probe fails; surface the failure with a clear message ("staging target unreachable: ${URL}").
4. Document the reachability gate in `docs/site/STAGING-PROMOTION-RUNBOOK.md`.
5. If `/health` endpoint doesn't exist on the resolver, escalate as a follow-on WO; do not invent one in this WO.

## Files to modify

- `.github/workflows/deploy-gated.yml` (add probe steps in `verify_staging` job)
- `docs/site/STAGING-PROMOTION-RUNBOOK.md` (document reachability gate)

## Constraints

- Do not commit, push, stage, or branch.
- Run `git status --short` first; if either `deploy-gated.yml` or the runbook is in WO-0232 or WO-0234 in-flight scope, wait or BLOCKED.
- Read-only git commands only.
- Don't add a probe that hits production. Staging only.
- If `actionlint` is available, run it post-edit.

## Acceptance criteria

- `verify_staging` runs reachability probes after `select-staging-bases.mjs`.
- Probes fail loudly with diagnostics.
- Runbook documents the gate.
- Resolver `/health` endpoint either confirmed extant or flagged as a follow-on WO.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0237-result.md`
Blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0237-BLOCKED.md`

Report must include: probe step diff, workflow output sample, runbook diff, `/health` endpoint confirmation or follow-on WO draft.
