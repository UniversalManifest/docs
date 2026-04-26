# WO-0218: Parametrize Dev Fixture TTL and Add Expiration Test

**Status:** COMPLETED — UM_FIXTURE_EXPIRY_OFFSET_SECONDS env var wired; 13/13 contract tests pass
**Priority:** MEDIUM (P2)
**Depends on:** none
**Unblocks:** —
**Derived from:** 2026-04-26 resolver runtime drift scan, finding 6 (MEDIUM)

## Objective

The dev fixture set hardcodes a TTL roughly 10 years in the future, which means TTL-expiration paths are never exercised in normal runs. Make the offset parametrizable via env var (default still 10 years to preserve current behavior), and add a test case that verifies the resolver returns a manifest while the smoke script's TTL validation flags it as expired when the offset is set negative.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/` (find the fixture TTL constant)
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/smoke-endpoints.mjs`
- Wherever the dev fixture set is generated/seeded (search `fixture` + `ttl` + `expiry`)
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0116-expand-resolver-test-suite-for-contract-coverage.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-resolver-runtime-drift-scan.md`

## Work to perform

1. Locate the hardcoded TTL value.
2. Replace with `process.env.UM_FIXTURE_EXPIRY_OFFSET_SECONDS ?? <current 10-year value>`.
3. Add a test case in `contract-tests.mjs` (or whichever file `WO-0116` established) that:
   - Sets `UM_FIXTURE_EXPIRY_OFFSET_SECONDS=-3600`
   - Verifies resolver returns 200 with the manifest
   - Verifies smoke-endpoints' TTL validation reports the manifest as expired
4. Document the env var in `services/myum-resolver/README.md` (or the resolver-doc location).

## Files to modify

- Wherever the TTL is hardcoded in `services/myum-resolver/`
- `packages/universal-manifest/scripts/smoke-endpoints.mjs` or `contract-tests.mjs` (test case)
- `services/myum-resolver/README.md` (document env var)

## Constraints

- Default value MUST preserve current behavior (10 years). No behavior change for unset env.
- Do not commit, push, stage, or branch.
- Run `git status --short` first; respect sibling commit agent's diff.

## Acceptance criteria

- `UM_FIXTURE_EXPIRY_OFFSET_SECONDS` env var works; unset = current behavior.
- Test case demonstrates expiration detection.
- Resolver README documents the var.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0218-result.md`
Blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0218-BLOCKED.md`
