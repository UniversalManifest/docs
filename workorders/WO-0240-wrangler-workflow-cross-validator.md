# WO-0240: wrangler.toml ↔ Workflow Cross-Validator

**Status:** OBSOLETE 2026-04-28 — `scripts/validate-wrangler-env-references.mjs` and the `wrangler-env-cross-check` job in `phase-9-gate.yml` were both removed in revert commit `e493b3e`. The bug class this guarded against (the WO-0232 `--env ""` failure) is also back since `deploy-gated.yml` was reverted; address separately if/when the user wants to re-apply the prod fix.
**Priority:** HIGH (P1) — closes the highest-leverage class of bugs that produced WO-0232
**Depends on:** WO-0232 (the bug it would have caught is now fixed; this WO prevents recurrence)
**Unblocks:** —
**Derived from:** WO-0232 result report — "what would have caught this earlier" analysis, suggestion #2

## Objective

WO-0232 surfaced a class of bug: `.github/workflows/deploy-gated.yml` referenced an environment via `--env ""` that did not exist in `services/myum-resolver/wrangler.toml`. The fix prevented the immediate harm; this WO prevents the entire bug class. Add a small CI cross-validator (~30-line script) that asserts every `wrangler --env <name>` invocation in any workflow file has a matching `[env.<name>]` block in the corresponding `wrangler.toml`. Run on every PR.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/wrangler.toml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml` (post-WO-0232 state)
- `/Users/grig/work/repo/universalmanifest/.github/workflows/` (any other workflows using wrangler)
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0232-result.md` (for the failure mode this prevents)

## Work to perform

1. **Inventory all wrangler invocations** — grep `npx wrangler` and `wrangler@` across `.github/workflows/`. Note every `--env <name>` flag.
2. **Inventory wrangler.toml env blocks** — every `[env.<name>]` section across the repo's wrangler config files.
3. **Build a small validation script** — `scripts/validate-wrangler-env-references.mjs` (or similar). Exits 0 if every `--env <name>` in workflows has a matching `[env.<name>]` block in the relevant wrangler.toml. Exits non-zero with a clear diff on mismatch.
4. **Wire into CI** — add a job to `.github/workflows/phase-9-gate.yml` (or a new dedicated workflow) that runs on every PR touching `.github/workflows/**` or `**/wrangler.toml`. Path-filter for cheapness.
5. **Document the gate** in `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md` (or appropriate runbook).

## Files to modify / create

- `scripts/validate-wrangler-env-references.mjs` (new)
- `.github/workflows/phase-9-gate.yml` (extension) OR `.github/workflows/wrangler-env-cross-check.yml` (new)
- `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md` (gate reference)

## Constraints

- **Keep the script small (~50 LOC max).** This is a focused linter, not a wrangler.toml parser. Use a permissive regex-based parse if it suffices; full TOML parsing is overkill.
- **Handle the empty-string edge case** — `--env ""` was the WO-0232 bug. The validator must flag empty-string env explicitly.
- **Handle the omit-`--env` case** — when `--env` is absent, validator should pass (top-level config is the implicit env).
- Do not commit, push, stage, or branch.
- Run `git status --short` first; respect sibling commit agent's diff.
- `actionlint` clean.

## Acceptance criteria

- New script exists and exits 0 against current (post-WO-0232) repo state.
- New CI gate runs the script on PRs that touch workflows or wrangler.toml.
- Script flags `--env ""` as an error (regression-prevent for WO-0232).
- Playbook references the new gate.
- Existing workflows pass.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0240-result.md`
Blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0240-BLOCKED.md`

Report must include: script content (or full diff), CI integration approach, sample run output, "what other bugs of this class this catches" enumeration.
