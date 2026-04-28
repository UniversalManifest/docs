# WO-0210: Phase 9 Gate First-Run Verification and Hardening

**Status:** OBSOLETE 2026-04-28 — target workflow `.github/workflows/phase-9-gate.yml` was removed in revert commit `e493b3e`. WO is structurally defunct; no first-run verification needed for a non-existent workflow.
**Priority:** MEDIUM (a never-run CI gate is a latent landmine; this WO proves it works)
**Depends on:** WO-0208 (created the gate), sibling commit agent's wave landing on `main`
**Unblocks:** —
**Derived from:** WO-0208 result report — workflow was YAML-validated but never executed end-to-end

## Objective

Prove that `.github/workflows/phase-9-gate.yml` runs green end-to-end on both its PR trigger and its scheduled/manual-dispatch trigger, then fix any bugs the first run surfaces. A CI workflow that has never been green is fragile — path issues, missing `npm ci` steps, wrong working directories, ripgrep regex quoting, schedule cron validity, and permission scopes only reveal themselves at runtime.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/.github/workflows/phase-9-gate.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/ci.yml` (for precedent: how the existing pipeline wires `npm ci`, caching, working-directory)
- `/Users/grig/work/repo/universalmanifest/.github/workflows/verify.yml`
- `/Users/grig/work/repo/universalmanifest/docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md`
- `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md` (Phase 9 section)
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-wo-0208-result.md`

## Work to perform

1. **Pre-flight local dry-run** — for each job defined in `phase-9-gate.yml`, reproduce the command sequence locally and confirm the working directory, `npm ci` / `npm install` requirements, and output are sensible. Note anything that would fail in a clean `ubuntu-latest` environment (e.g., missing lockfile, non-pinned Node version, tool not in default path).
2. **Actionlint** — if `actionlint` is available (install via `brew install actionlint` or `go install github.com/rhysd/actionlint/cmd/actionlint@latest`), run it on `phase-9-gate.yml` and fix every warning. If not available, at minimum pass through a YAML schema validator that understands GitHub Actions.
3. **Fix surfaced bugs** — apply minimal patches directly to `phase-9-gate.yml`. Common expected fixes:
   - explicit `working-directory:` for jobs that `cd` into `packages/universal-manifest/` or `site/`
   - explicit Node version via `actions/setup-node@v4` with `node-version-file:` or a pinned version matching `ci.yml`
   - `npm ci` rather than `npm install` in CI
   - `actions/cache` for `node_modules` if `ci.yml` uses it
   - corrected ripgrep regex quoting for the link-hygiene scan (shell escaping differs inside GitHub Actions YAML)
   - explicit `permissions:` block if the job uses `GITHUB_TOKEN`
4. **Manual dispatch trigger** — once the repo branch is merged to `main`, trigger the workflow via `workflow_dispatch` (manual) and capture the run URL. Confirm all jobs green. If any fail, fix and rerun.
5. **PR trigger verification** — open a trivial no-op PR (or use a scratch PR) to confirm the PR-trigger variant runs and passes. Cancel the PR after verification; do not merge the scratch.
6. **Schedule trigger verification** — because the schedule is weekly, direct observation requires waiting. Instead, use the `workflow_dispatch` input `run_production_routes: 'true'` to exercise the schedule-only job path manually and confirm it works. Record evidence.
7. **Document** — update `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md` with a "First green run evidence" subsection linking to the run URLs, and update `WO-0208` closeout comment if needed.

## Files to modify / create

- `.github/workflows/phase-9-gate.yml` (patches only, no rewrite)
- `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md` (append "First green run evidence" subsection)

## Constraints

- Do not weaken or remove any job. If a job is genuinely impossible to run in CI (e.g., needs a secret that does not exist), mark it `if: false` with a clear comment referencing this WO and document the blocker — do not delete.
- Do not add secrets. If the workflow needs one, document the requirement and flag it to the user.
- Do not commit, push, stage, or branch. Another agent owns the commit path; your patches land on the working tree and the sibling agent's next commit wave picks them up.
- Do not touch any file currently in the sibling commit agent's diff. Run `git status --short` first.
- First green run proof must be captured by URL; do not claim "it works" without a run log.

## Acceptance criteria

- `actionlint` (or equivalent) passes on `phase-9-gate.yml` with zero warnings.
- A PR-trigger run exists in GitHub Actions history with all jobs green.
- A `workflow_dispatch` run with `run_production_routes: 'true'` exists with all jobs green.
- Playbook has a "First green run evidence" subsection linking to both runs.
- Any applied patches are small and surgical; no job removed.

## Output

Write result report to: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-wo-0210-result.md`

If blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-wo-0210-BLOCKED.md`

Report must include: actionlint output before/after, list of patches applied, links to both green runs, and any `if: false` jobs with justification.
