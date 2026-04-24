# WO-0208: Phase 9 Drift-Governance Automation Hardening

**Status:** COMPLETED
**Priority:** HIGH (forward-looking; converts heroic WO-0206-style restoration into a procedural playbook + CI gate)
**Depends on:** WO-0209, WO-0207 (both complete; canonical state clean before baselining)
**Unblocks:** —
**Derived from:** 2026-04-24 surface drift scan (Finding 6.1), `docs/CRITICAL-PATH.md` Phase 9 section

## Objective

Convert Phase 9 drift governance from a manually-invoked cadence (currently a maintainer types the mandatory command set) into an automated, CI-gated, procedurally documented system that catches K2B artifact, journey-parity, production-route, and docs-link drift before it becomes a WO-0206-grade restoration.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md` (Phase 9 section + mandatory command set)
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0206-k2b-drift-governance-artifact-contract-restoration.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0023-production-deployment-drift-prevention-automation.md` (prior automation precedent)
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0114-automate-deploy-pipeline-with-release-gates.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0117-add-synthetic-monitoring-alerting-and-slo-policy.md`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/` (existing CI pipelines — discover then read)
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/smoke-endpoints.mjs`
- Any existing K2B gate script referenced from `~/.agents/scripts/validate-k2b-gates.sh`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-phase9-governance-refresh.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-surface-drift-scan.md`

## Work to perform

1. **Inventory current CI** — list every existing GitHub Actions workflow and what it already gates (build, tests, parity, deploy). Identify which of Phase 9's mandatory commands are already covered and which are still manual.
2. **Design the Phase 9 CI gate** — define a new or extended workflow that runs, on every PR and on a weekly schedule:
   - `npm test` in `packages/universal-manifest/` (valid + invalid fixtures)
   - `npm run journeys` in `packages/universal-manifest/`
   - validator parity via `site/scripts/test-validator-parity.mjs`
   - docs link-hygiene ripgrep from Phase 9
   - production route smoke (HEAD checks on the three canonical URLs) — scheduled only, not per-PR
   - K2B gate validation (`~/.agents/scripts/validate-k2b-gates.sh --strict`) — only if the script can be safely vendored or mirrored into the repo; otherwise document why this check remains manual
3. **Handle the K2B artifact root** — the strict K2B gate needs `.dev/ai` artifacts which are currently gitignored. Decide and document one of:
   - (a) mirror the required K2B contract files into a tracked `governance/k2b/` directory so CI can see them, or
   - (b) keep K2B gate manual but write a restoration playbook citing WO-0206 as the reference procedure
   Pick (b) unless (a) is provably safe; do not widen the tracked surface lightly.
4. **Write the drift-recovery playbook** — create `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md` that documents:
   - symptom → diagnosis → remediation for each mandatory command failure mode
   - the WO-0206 case study as the reference example (K2B artifact contract disappeared, was restored from commit `3eef43b`, path-normalized, re-verified)
   - escalation thresholds (when a failure needs a new WO vs. can be fixed inline)
5. **Schedule a monthly drift scan** — add a scheduled GitHub Actions cron (or equivalent) that re-runs today's drift-scan agent prompt and files the result under `.dev/ai/subtask-comms/` or a tracked `docs/reports/drift-scans/` directory (decide which; tracked is safer for audit).

## Files to modify / create

- `.github/workflows/phase-9-gate.yml` (new; or extend existing workflow)
- `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md` (new)
- `docs/CRITICAL-PATH.md` (update Phase 9 section to cite the new workflow + playbook)
- Optional: `governance/k2b/` (only if decision is (a) in step 3)

## Constraints

- **Do not weaken existing CI.** If a new workflow is added, existing gates must continue to pass.
- **Do not commit or push.** Another agent still owns the git path.
- **Do not regress production route checks** — if CI-side curl checks flap against Cloudflare, scope them to a scheduled job, not per-PR.
- **No CI tokens or secrets** — document any credential requirements; do not hard-code anything.
- Respect the standing rule in `AGENTS.md`: public copy must stay in sync with its markdown/source counterpart. The runbook is a new canonical document — it has no prior counterpart, so creation is correct.
- **Do not assume `~/.agents/scripts/validate-k2b-gates.sh` is available inside CI.** Either vendor it or document the manual step.

## Acceptance criteria

- A new or extended workflow runs the Phase 9 mandatory command set on PRs and weekly schedule.
- The runbook exists at `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md` with a WO-0206 case study section.
- `docs/CRITICAL-PATH.md` Phase 9 section references the new workflow + playbook.
- The K2B decision (vendor vs. manual) is explicitly documented with rationale.
- The workflow file validates syntactically (`actionlint` or equivalent if available; otherwise manual YAML parse).
- No existing CI check is removed or weakened.

## Output

Write result report to: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-wo-0208-result.md`

If blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-wo-0208-BLOCKED.md`.

Report must include: workflow file diff, playbook outline, K2B decision rationale, and a "what would have caught WO-0206 earlier" analysis.
