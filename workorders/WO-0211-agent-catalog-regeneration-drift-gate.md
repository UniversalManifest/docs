# WO-0211: Agent Catalog Regeneration Drift Gate

**Status:** OBSOLETE 2026-04-28 — target workflow `.github/workflows/phase-9-gate.yml` was removed in revert commit `e493b3e`. The underlying need (gate agent-catalog regeneration) may still be valid but would require a different mechanism; re-scope from scratch if pursued.
**Priority:** MEDIUM (closes the same drift class WO-0207 manually audited; prevents silent divergence)
**Depends on:** WO-0210 (Phase 9 gate proven green first, so we extend a known-working workflow rather than debugging two gates at once)
**Unblocks:** —
**Derived from:** WO-0207 result (catalog counts verified accurate only because the regenerator had been run today); grep confirms `sync-agent-discovery` has a `site/package.json` script entry but zero CI workflow references

## Objective

Prevent the `site/public/agent/fixture-catalog.json` and `site/public/agent/sandbox-scenarios.json` files from drifting out of sync with their canonical sources (`examples/`, `docs/sandbox-scenarios/` or wherever the generator reads from) by wiring `site/scripts/sync-agent-discovery.mjs` into CI as a drift check. The script exists and is invokable as `npm run sync:agent-discovery` from `site/`; nothing currently gates on its output being reproducible.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/site/scripts/sync-agent-discovery.mjs`
- `/Users/grig/work/repo/universalmanifest/site/package.json` (confirm `sync:agent-discovery` script; check whether a `sync:agent-discovery:check` mode already exists)
- `/Users/grig/work/repo/universalmanifest/site/public/agent/fixture-catalog.json`
- `/Users/grig/work/repo/universalmanifest/site/public/agent/sandbox-scenarios.json`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/phase-9-gate.yml` (extension target)
- `/Users/grig/work/repo/universalmanifest/.github/workflows/ci.yml`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-wo-0207-result.md`

## Work to perform

1. **Inspect the regenerator** — read `sync-agent-discovery.mjs` and determine:
   - Its input sources (`examples/`, spec files, hand-curated scenario metadata, etc.)
   - Its output files (confirm the two JSON catalogs are the only outputs)
   - Whether it is deterministic (same input → byte-identical output)
   - Whether it supports a `--check` / `--dry-run` mode that exits non-zero on drift without writing
2. **Add a check mode if missing** — if the script does not already support `--check`, add a minimal flag that:
   - Runs the full generation in memory
   - Compares against the on-disk catalogs
   - Exits 0 on match, non-zero with a clear diff summary on mismatch
   - Does NOT write files in `--check` mode
3. **Expose the check via npm** — add `"sync:agent-discovery:check": "node scripts/sync-agent-discovery.mjs --check"` (or equivalent) to `site/package.json`.
4. **Wire into CI** — extend `.github/workflows/phase-9-gate.yml` (or `ci.yml` if that is the more appropriate home, per the Phase 9 gate's scope rationale) with a new job that runs `npm run sync:agent-discovery:check` from the `site/` directory on every PR. If the catalogs are out of sync, the job fails with a message telling the contributor to run `npm run sync:agent-discovery` and commit the result.
5. **Idempotence sanity check** — run the regenerator locally, diff the output against the committed catalogs. If there is any non-trivial diff (anything beyond a changed `generatedAt` timestamp), fix either the script (make timestamp optional in check mode) or flag for follow-up.
6. **Document** — add a note to `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md` under the appropriate section explaining the new gate.

## Files to modify / create

- `site/scripts/sync-agent-discovery.mjs` (add `--check` mode if absent)
- `site/package.json` (add check script)
- `.github/workflows/phase-9-gate.yml` OR `.github/workflows/ci.yml` (new job)
- `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md` (note the gate)

## Constraints

- **Determinism first.** If the current regenerator is not deterministic (embeds wall-clock `generatedAt`, random IDs, non-sorted object keys, etc.), the `--check` mode must normalize those before comparing. Do not make the gate flaky.
- **No write in check mode.** A check that writes to disk is not a check.
- **Do not regenerate and commit during this WO.** If running the regenerator locally produces a non-trivial diff, STOP. Write a BLOCKED report documenting the diff and let the user decide whether to regenerate+commit (possibly as its own micro-WO) before this gate is enabled. The reason: committing a regeneration during WO-0211 conflates "enable gate" with "close existing drift", which hides evidence.
- Do not weaken or remove any existing workflow job.
- Do not commit, push, stage, or branch. Sibling commit agent owns git mutations.
- Do not touch files in the sibling commit agent's current diff; run `git status --short` first.

## Acceptance criteria

- `npm run sync:agent-discovery:check` from `site/` exits 0 when catalogs are current, non-zero with a useful diff when they drift.
- CI job runs on every PR and fails loudly on drift with an actionable message.
- Regenerator's determinism concerns (timestamp/ID/sort) are explicitly addressed in `--check` mode.
- Playbook documents the gate.
- No existing workflow job is removed or weakened.

## Output

Write result report to: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-wo-0211-result.md`

If blocked (most likely: regenerator produces a non-trivial diff against committed catalogs): `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-wo-0211-BLOCKED.md`

Report must include: regenerator's input/output analysis, determinism findings, diff between fresh regeneration and committed catalogs (if any), `--check` mode implementation summary, CI job diff, and which workflow was chosen (phase-9-gate.yml vs. ci.yml) with rationale.
