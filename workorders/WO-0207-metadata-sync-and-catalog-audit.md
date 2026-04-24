# WO-0207: Metadata Sync and Catalog Audit

**Status:** COMPLETED
**Priority:** MEDIUM (agent-facing freshness signal + count reconciliation)
**Depends on:** WO-0209 (canonical status trail must be current before metadata bump)
**Unblocks:** WO-0208
**Derived from:** 2026-04-24 surface drift scan (Findings 1.1, 5.1, 5.2)

## Objective

Bring agent-facing machine-readable metadata into parity with current canonical status (post WO-0206 + 2026-04-24 micro-closeouts), and reconcile the published fixture/scenario catalog counts to their canonical sources so the delta is auditable.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md` (post-WO-0209 state)
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md` (post-WO-0209 state)
- `/Users/grig/work/repo/universalmanifest/site/public/.well-known/universal-manifest.json`
- `/Users/grig/work/repo/universalmanifest/site/public/.well-known/security.txt`
- `/Users/grig/work/repo/universalmanifest/site/public/llms.txt`
- `/Users/grig/work/repo/universalmanifest/site/public/agent/fixture-catalog.json`
- `/Users/grig/work/repo/universalmanifest/site/public/agent/sandbox-scenarios.json`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-surface-drift-scan.md`

## Work to perform

1. **Timestamp sync** — set `lastUpdated` in `site/public/.well-known/universal-manifest.json` to `2026-04-24`.
2. **Closure signal** — if the descriptor schema allows, add `lastCompletedWo: "WO-0206"` and `closureWave: "home-cluster-rollout"` fields (or closest existing equivalent). If the schema is strict and no such field exists, document the absence in the WO report and skip the field — do not invent schema extensions that break consumers.
3. **Catalog count audit** — compare the published claim (`publicFixtures: 138`, `publicSandboxScenarios: 50`) against:
   - canonical `examples/` file count (total + split by v0.1 / v0.2 / invalid / stubs / integrations)
   - generated `fixture-catalog.json` entry count
   - generated `sandbox-scenarios.json` entry count
4. **Reconcile** — either (a) update the numeric claims to match measured reality, or (b) leave them and document the delta explicitly (e.g., "138 = 86 canonical + 46 mirrors + 6 integration lanes"). Choose (a) if the claim is wrong; choose (b) only if the claim is defensible and the breakdown is documented.
5. **Security contact freshness** — verify `securityContact` value exists and matches `site/public/.well-known/security.txt`; do not change the email address, only flag if they diverge.
6. **Byproduct files** — if any regeneration script exists for these catalogs, note its path in the WO report; do not regenerate without evidence the regenerator is idempotent.

## Files to modify

- `site/public/.well-known/universal-manifest.json` (primary)
- Optionally: `site/public/llms.txt` if it also carries a stale timestamp
- Optionally: `docs/reports/` — add a short audit report if the catalog-count delta warranted investigation

## Constraints

- Do not commit or push. Do not stage.
- Do not modify any file in the sibling agent's current commit set (fixtures under `examples/*`, site mirror fixtures under `site/public/harness/fixtures/*` and `site/public/sandbox/fixtures/*`, `packages/universal-manifest/scripts/resign-all-v02.mjs`, `site/scripts/parity-test.mjs`, `site/scripts/test-validator-parity.mjs`, `AGENTS.md`, `site/src/content/docs/handouts/09-whats-next.md`). Run `git status --short` first to confirm the current set; if the well-known descriptor is in that set, abort and write to the BLOCKED file.
- Do not invent JSON fields not already defined in `.well-known/universal-manifest.json`'s existing shape unless the existing documented schema explicitly allows them.
- No spec, fixture, or site-content changes. Metadata-only.

## Acceptance criteria

- `.well-known/universal-manifest.json` `lastUpdated` equals `2026-04-24`.
- Fixture-catalog and scenario-catalog count claims are either accurate or explicitly explained in the WO report.
- `curl -I https://universalmanifest.net/.well-known/universal-manifest.json` still returns 200 (post-next-deploy; local-change verification only — no deploy).
- JSON validates (`jq . site/public/.well-known/universal-manifest.json`).
- No changes bleed into the sibling commit agent's diff.

## Output

Write result report to: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-wo-0207-result.md`

If blocked (e.g., well-known descriptor was in sibling agent's diff): `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-wo-0207-BLOCKED.md`.

Report must include: before/after of `lastUpdated`, measured catalog counts with breakdown, files modified (absolute paths), and jq validation confirmation.
