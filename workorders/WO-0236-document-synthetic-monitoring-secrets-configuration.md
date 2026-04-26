# WO-0236: Document Synthetic Monitoring Secrets Configuration

**Status:** COMPLETED 2026-04-26 — new `docs/operations/SYNTHETIC-MONITORING-SETUP.md`; 4 secrets enumerated with type/shape/consuming-workflows/precedence; placeholder-only curl examples; cross-linked from SLO policy
**Priority:** MEDIUM (P2) — operator onboarding hygiene
**Depends on:** none
**Unblocks:** —
**Derived from:** 2026-04-26 deployment pipeline drift scan, finding (MEDIUM) — undocumented `UM_SYNTHETIC_*` secrets

## Objective

Several `UM_SYNTHETIC_*` secrets are referenced in CI workflows (`synthetic-monitoring.yml` and friends) but not documented in any operator-onboarding runbook. New maintainers can't reproduce the alerting wiring without spelunking workflow YAML.

## Files to read first

- All `.github/workflows/*.yml` (grep for `secrets.UM_SYNTHETIC_`, `secrets.SYNTHETIC_`, `secrets.WEBHOOK_`)
- `/Users/grig/work/repo/universalmanifest/docs/site/STAGING-PROMOTION-RUNBOOK.md`
- `/Users/grig/work/repo/universalmanifest/docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md` (added by WO-0215)
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-deployment-pipeline-drift-scan.md` (finding 5)

## Work to perform

1. Enumerate every `UM_SYNTHETIC_*` and other monitoring-secret reference across `.github/workflows/`.
2. For each, document: name, what it is (URL? token? webhook?), where to obtain it, what fails if it's missing, and which workflows consume it.
3. Add a "Synthetic Monitoring Secrets" section to either `docs/site/STAGING-PROMOTION-RUNBOOK.md` (existing) or create `docs/operations/SYNTHETIC-MONITORING-SETUP.md` (new). Pick whichever scales better; document the choice.
4. Provide a curl command for testing each webhook (no live secret values, just the shape).

## Files to modify / create

- `docs/operations/SYNTHETIC-MONITORING-SETUP.md` (new, recommended) OR section appended to `docs/site/STAGING-PROMOTION-RUNBOOK.md`
- Optional: cross-link from `docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md` (added by WO-0215)

## Constraints

- **Never log or print actual secret values.** Only names and shapes.
- Do not commit, push, stage, or branch.
- Run `git status --short` first; respect sibling commit agent's diff.
- Don't change workflow files in this WO; documentation only.

## Acceptance criteria

- Every monitoring-related `secrets.*` reference is documented with name + purpose + source + failure mode.
- New (or extended) runbook section is discoverable from the SLO policy doc.
- Curl examples are present for each webhook (without secret values).

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0236-result.md`
Blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0236-BLOCKED.md`
