# WO-0222: Machine-Readable Surface Refresh — Well-Known, llms.txt, and Agent Catalogs

**Status:** NOT_STARTED
**Priority:** P0 (announcement and smoke depend on this)
**Depends on:** WO-0221
**Unblocks:** WO-0226, WO-0227, WO-0228
**Derived from:** 2026-04-26 v0.2 publication push plan, item 3; WO-0207 partial sync

## Objective

Update the machine-readable discovery surfaces to reflect v0.2 as the current published spec version (and v0.1 as the previously published version). Add a `currentSpecVersion` field where one is missing and a publication-status flag where appropriate.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/site/public/.well-known/universal-manifest.json`
- `/Users/grig/work/repo/universalmanifest/site/public/llms.txt`
- `/Users/grig/work/repo/universalmanifest/site/public/agent/fixture-catalog.json` (top-level metadata block only)
- `/Users/grig/work/repo/universalmanifest/site/public/agent/sandbox-scenarios.json` (top-level metadata block only)
- `/Users/grig/work/repo/universalmanifest/site/scripts/sync-agent-discovery.mjs`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0207-metadata-sync-and-catalog-audit.md`

## Work to perform

1. **`.well-known/universal-manifest.json`:**
   - Update `versions.stable` from `"v0.1"` to `"v0.2"`.
   - Update `versions.draft` to `null` (or remove the key) since there is no draft beyond the published v0.2 yet. If a forward-looking `"v0.3"` draft is intended, document it.
   - Add a top-level `"currentSpecVersion": "v0.2"` field for tooling that wants a single field instead of the nested `versions` block.
   - Update `lastUpdated` to the publication date (today, when this WO runs).
2. **`llms.txt`:**
   - The current file lists both v0.1 and v0.2 artifacts symmetrically. Reorder to list v0.2 first, then v0.1, so an LLM reading top-down picks up v0.2 as primary.
   - Add a one-line "Current published version: v0.2" near the top of the document.
3. **`agent/fixture-catalog.json` and `agent/sandbox-scenarios.json`:**
   - Add a top-level `"currentSpecVersion": "v0.2"` field next to the existing `catalog` / `generatedAt` keys.
   - Bump `generatedAt` to today's run.
   - DO NOT alter the per-fixture / per-scenario `version` fields — those describe the fixture, not the catalog.
4. **`site/scripts/sync-agent-discovery.mjs`:**
   - If this script is the canonical generator (per WO-0207), update its emit logic to include `currentSpecVersion`. Otherwise, document the manual edit so it doesn't get overwritten on the next regeneration.
5. **Run** `node site/scripts/sync-agent-discovery.mjs` (if it exists and is non-destructive) and verify the output matches the expected diff. If WO-0211 has shipped a `--check` mode, run it and confirm green.

## Files to modify

- `site/public/.well-known/universal-manifest.json`
- `site/public/llms.txt`
- `site/public/agent/fixture-catalog.json`
- `site/public/agent/sandbox-scenarios.json`
- `site/scripts/sync-agent-discovery.mjs` (only if it generates the catalogs)

## Constraints

- **Do not change route URLs.** Only metadata and version-pointer fields move.
- **Per-fixture `version` fields stay as-is.** A v0.1 fixture is still a v0.1 fixture.
- **JSON validity:** `jq . <each-file>` must exit 0 after the edit.
- **Idempotency:** Running the WO a second time on a clean tree should be a no-op.

## Acceptance criteria

- `.well-known/universal-manifest.json` declares v0.2 as `stable` and includes `currentSpecVersion: "v0.2"`.
- `llms.txt` lists v0.2 artifacts before v0.1 and includes a "Current published version" line.
- Both agent catalogs include `currentSpecVersion: "v0.2"` at the top level.
- `jq . <file>` exits 0 for all three JSON files.
- If `sync-agent-discovery.mjs` was modified, regenerating the catalogs produces no further diff.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0222-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0222-BLOCKED.md`
