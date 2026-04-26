# WO-0238: Add Automated Rollback Workflow

**Status:** COMPLETED 2026-04-26 — new `.github/workflows/rollback-manual.yml` with 6 jobs (confirm_gate → build → rollback_docs+rollback_resolver in parallel → verify_rollback → audit_trail); reuses existing smoke + verify:postdeploy scripts; INCIDENT-RESPONSE.md §6.4 added; audit trail via artifact + operator-commits; actionlint clean
**Priority:** MEDIUM (P2)
**Depends on:** WO-0232 (deploy must work correctly before automated rollback can re-deploy a prior ref reliably)
**Unblocks:** Incident-response automation (operationalizes WO-0059)
**Derived from:** 2026-04-26 deployment pipeline drift scan, finding (MEDIUM) — no automated rollback workflow

## Objective

`WO-0059` mandated incident/rollback policies; the playbook exists but rollback is currently a manual sequence. Add a workflow that any operator can trigger via `workflow_dispatch` to re-deploy a chosen prior git ref to staging or production and re-run smoke. Reduces incident MTTR from "find the docs and run several commands" to "click the workflow, pick the ref, click run."

## Files to read first

- `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml` (the existing deploy primitives — reuse, don't duplicate)
- `/Users/grig/work/repo/universalmanifest/docs/governance/INCIDENT-RESPONSE.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0059-governance-completion-breaking-change-deprecation-incident.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-deployment-pipeline-drift-scan.md` (finding 7)

## Work to perform

1. **Create `.github/workflows/rollback-manual.yml`** with `workflow_dispatch` inputs:
   - `environment`: `choice` of `staging` | `production`
   - `git-ref`: string (commit SHA or tag) to re-deploy
   - `confirm`: string that must equal "ROLLBACK" before the workflow proceeds (sanity gate)
2. **Reuse existing deploy primitives** — call the same Cloudflare Pages and Worker deploy actions used in `deploy-gated.yml`. Do not duplicate logic.
3. **Re-run smoke** post-rollback using the same smoke harness path used by `deploy-gated.yml`'s `verify_staging` / `verify_production` jobs.
4. **Wire into `INCIDENT-RESPONSE.md` playbook** — add a section "Automated rollback" with the operator instructions.
5. **Audit trail** — write a rollback record to `.dev/ai/reports/rollbacks/{date}-{env}-{ref}.md` (or tracked equivalent if `.dev/ai/reports/` is not the canonical location).

## Files to modify / create

- `.github/workflows/rollback-manual.yml` (new)
- `docs/governance/INCIDENT-RESPONSE.md` (add Automated Rollback section)
- `docs/reports/rollbacks/.gitkeep` (new directory if needed)

## Constraints

- **Do NOT trigger an actual rollback** during this WO. The workflow lands; the operator decides when to invoke.
- The `confirm: "ROLLBACK"` input is a hard gate — workflow must early-fail if absent.
- Do not commit, push, stage, or branch.
- Run `git status --short` first; respect sibling commit agent's diff.
- `actionlint` if available.

## Acceptance criteria

- New `rollback-manual.yml` exists with the three inputs and the confirm gate.
- Deploy logic reuses (does not duplicate) existing primitives.
- Post-rollback smoke runs and gates the workflow's overall success.
- INCIDENT-RESPONSE.md has the operator guide.
- `actionlint` clean.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0238-result.md`
Blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0238-BLOCKED.md`
