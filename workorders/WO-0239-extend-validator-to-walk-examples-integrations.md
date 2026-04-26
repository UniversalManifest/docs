# WO-0239: Extend Validator to Walk `examples/integrations/`

**Status:** COMPLETED 2026-04-26 — validate-examples.mjs +70/-1; third walk pass added; 6 integration-lane ok, 0 failed; 49+26 normative baseline preserved; CONFORMANCE.md §7.1 left alone (existing wording remains accurate)
**Priority:** HIGH (P1) — gates remaining WO-0216 batches; without this, all new lane fixtures pass-by-omission rather than pass-by-validation
**Depends on:** none
**Unblocks:** WO-0216 batches 2–5 (xr/runtime, did-vc/personhood, healthcare/education/smart-home, OMATrust/firewall/RP1)
**Derived from:** WO-0216 batch 1 result (`/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0216-batch-1-result.md`) — wiring gap

## Objective

`packages/universal-manifest/scripts/validate-examples.mjs` currently walks only `examples/v0.1/` and `examples/v0.2/`. The integration-lane fixtures live under `examples/integrations/` and are intentionally non-normative per `spec/v0.1/CONFORMANCE.md` §7.1, but they should still be validated for shape correctness so they cannot silently drift. WO-0216 batch 1 added 6 fixtures that are not gated by `npm test`. Extend the validator so future batches actually validate.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/validate-examples.mjs`
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/package.json` (test script)
- `/Users/grig/work/repo/universalmanifest/spec/v0.1/CONFORMANCE.md` (§7.1 for the non-normative status of `examples/integrations/`)
- `/Users/grig/work/repo/universalmanifest/examples/integrations/` (full tree — current state with batch 1)
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0216-batch-1-result.md`

## Work to perform

1. **Inspect the validator** — understand how it currently walks `examples/v0.1/` and `examples/v0.2/`. Note the assertion library (likely `assertUniversalManifestV01` or similar from `packages/universal-manifest/src/`).
2. **Add a third walk pass** for `examples/integrations/**/*.jsonld` (and `*.json` if applicable). Validate against the v0.1 contract (per CONFORMANCE.md, integration fixtures are v0.1-baseline).
3. **Distinguish counts in output** — `npm test` should report `valid` / `invalid` / `integration-lane` separately so future readers understand what each set proves. Don't conflate integration-lane validity with normative spec validity.
4. **Update the package's test summary** — current baseline reads `49 valid + 26 invalid + 6 GPC runtime + 4 support-resource + 1 GPC projection`. After this WO + batch 1's 6 fixtures, expect a new line like `12 integration-lane ok` (or whatever count is current). Document the expected post-WO baseline in the result report.
5. **Verify zero regressions** — existing 49 valid + 26 invalid pass counts must not change. Integration-lane is additive only.
6. **Update `spec/v0.1/CONFORMANCE.md` §7.1** if the existing wording implies "integration fixtures are not validated" — revise to "integration fixtures are validated for shape correctness against v0.1 baseline; they remain non-normative for conformance claims." Be careful: this is a normative-document edit; if the wording is load-bearing, escalate as a follow-on rather than rewriting.

## Files to modify

- `packages/universal-manifest/scripts/validate-examples.mjs` (primary)
- `packages/universal-manifest/package.json` (only if a new script entry is needed)
- `spec/v0.1/CONFORMANCE.md` §7.1 (only if wording requires update; otherwise leave alone and flag as follow-on)

## Constraints

- **No new validation rules.** Use existing `assertUniversalManifestV01` (or whatever the v0.1 assertion library is). Do not invent new constraints.
- **Existing 49 + 26 baseline must not change.** Integration-lane counts are reported separately.
- Run `git status --short` first; do NOT touch any file in the sibling commit agent's diff. Confirm `validate-examples.mjs`, `package.json`, and `CONFORMANCE.md` are not in their diff.
- Read-only git commands only. No commit/push/stage/branch.
- Do not regenerate fixtures. The 6 batch-1 fixtures must validate as-is. If any fail, that is a real bug to surface, not to mask.
- If extending the validator surfaces fixtures that fail, write to BLOCKED with the failing fixtures listed.

## Acceptance criteria

- `npm test` walks `examples/integrations/**/*.jsonld` and reports a separate count.
- Existing 49 valid + 26 invalid pass counts unchanged.
- Batch 1's 6 fixtures all pass via the new walk.
- Output messaging is clear about normative vs. integration-lane distinction.
- WO-0216's "count grows" prediction is now actually achievable in future batches.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0239-result.md`
Blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0239-BLOCKED.md`

Report must include: validator diff, new test output sample (full `npm test` summary post-WO), integration-lane count after batch 1, CONFORMANCE.md disposition (edited / left alone with reason), confirmation of zero regression in existing counts.
