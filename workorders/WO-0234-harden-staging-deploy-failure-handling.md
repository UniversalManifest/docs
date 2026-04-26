# WO-0234: Harden Staging Deploy Failure Handling in Release Gate

**Status:** COMPLETED 2026-04-26 — kept `continue-on-error: true` on staging deploys but added compensating gate (deploy_outcome outputs + verify_staging first-step assertion that exit 1s on failure); runbook documents Gate-Failure Semantics; actionlint clean
**Priority:** HIGH (P1)
**Depends on:** WO-0232 (don't compound a known-bad prod deploy with a hardened staging gate that blocks legitimate operator overrides)
**Unblocks:** —
**Derived from:** 2026-04-26 deployment pipeline drift scan, finding (HIGH) — staging deploys allow silent failures via `continue-on-error: true`

## Objective

`.github/workflows/deploy-gated.yml` lines 82 and 170 (staging docs and resolver deploy steps) carry `continue-on-error: true` with no compensating gate. A staging deploy can fail silently and the workflow proceeds to `verify_staging` against a non-deployed surface. Either remove the silent-error tolerance, or capture exit codes and explicitly fail `verify_staging` on staging deploy failure.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml` (lines 82, 170 with full surrounding context — and any other `continue-on-error` instances)
- `/Users/grig/work/repo/universalmanifest/docs/site/STAGING-PROMOTION-RUNBOOK.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-deployment-pipeline-drift-scan.md` (finding for line 82, 170)

## Work to perform

1. **Inventory `continue-on-error` instances** in deploy-gated.yml. Determine which were intentional (e.g., a non-blocking advisory check) and which are silent failures.
2. **Choose the fix shape** — remove `continue-on-error` outright if the step is meant to gate, OR capture the exit code and assert in `verify_staging`. Document which choice for each instance.
3. **Test (locally where possible)** — at minimum, lint the workflow with `actionlint`. If the project has a way to run the workflow against an intentional staging-failure scenario in a sandbox, do so.
4. **Update `STAGING-PROMOTION-RUNBOOK.md`** with the new gate-failure semantics: what fails the workflow, what's allowed to advisory-fail, and the operator's expected response when the gate fires.

## Files to modify

- `.github/workflows/deploy-gated.yml` (lines 82, 170 + any compensating `verify_staging` gate logic)
- `docs/site/STAGING-PROMOTION-RUNBOOK.md` (update gate-failure section)

## Constraints

- **Do NOT remove `continue-on-error` from a step that genuinely needs it** without compensating logic. If you're unsure whether a step is gating-or-advisory, mark it for follow-up rather than changing it.
- Do not commit, push, stage, or branch.
- Run `git status --short` first; if WO-0232 has not yet landed and is in your way (same file), wait for WO-0232's result and rebase. If WO-0232 is in flight and this WO would conflict, write to BLOCKED and stop.
- Read-only git commands only.
- Do not change production deploy behavior. Staging-only.

## Acceptance criteria

- No silent staging-deploy failures: every `continue-on-error: true` in deploy-gated.yml is justified or removed.
- `verify_staging` (or equivalent) blocks promotion if any staging deploy step failed.
- Runbook documents the new failure semantics.
- `actionlint` clean.
- Production deploy step unchanged.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0234-result.md`
Blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0234-BLOCKED.md`

Report must include: per-instance disposition table for `continue-on-error` flags, workflow diff, runbook diff, actionlint output.
