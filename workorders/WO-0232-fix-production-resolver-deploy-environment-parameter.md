# WO-0232: Fix Production Resolver Deploy Environment Parameter

**Status:** COMPLETED 2026-04-26 — `--env ""` removed entirely (top-level wrangler config IS production); KV-binding assertion added with secret-redaction; OPERATOR ACTION: set repo secrets `PROD_RESOLVER_UMID_KV_ID` (required) and `STAGING_RESOLVER_UMID_KV_ID` (optional negative-assertion) before next prod deploy
**Priority:** CRITICAL (P0) — production data-corruption risk on next deploy
**Depends on:** none
**Unblocks:** WO-0234, WO-0238, the entire publication wave (WO-0220 onward)
**Derived from:** 2026-04-26 deployment pipeline drift scan, finding 1 (CRITICAL)

## Objective

`.github/workflows/deploy-gated.yml` line 463 invokes `npx wrangler@4 deploy --env ""` with an empty-string environment argument when deploying the production resolver Worker. Wrangler's behavior with an empty `--env ""` is non-obvious and may bind to the wrong KV namespace (likely the staging namespace or no namespace), corrupting production resolver state on the next deploy. Fix the parameter and add a CI assertion that prevents recurrence.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml` (lines around 463; also note staging deploy step for the correct comparison)
- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/wrangler.toml` (confirm production env name and KV namespace ID)
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-deployment-pipeline-drift-scan.md` (finding 1 with full evidence)

## Work to perform

1. **Confirm the bug** — read line 463 in context. Verify it's the production deploy step (not staging). Verify the staging step uses `--env "staging"` correctly. Match the wrangler.toml env names.
2. **Apply the fix** — change `--env ""` to `--env "production"` (or omit `--env` entirely if wrangler.toml's default-env behavior is correct for this Worker). Choose with rationale.
3. **Add a CI assertion** — after the deploy step, add a verification step that confirms the deployed Worker is bound to the production KV namespace ID (e.g., grep wrangler output for the expected namespace ID, or call a Worker introspection endpoint). Goal: catch a recurrence of this bug at deploy-time, not in production.
4. **Smoke-check the fix locally** — run `actionlint` on the modified workflow if available.

## Files to modify

- `.github/workflows/deploy-gated.yml` (one line change + assertion step)

## Constraints

- **Do NOT trigger an actual production deploy** as part of this WO. The fix lands in the working tree; the user/operator deploys when ready.
- Run `git status --short` first; do NOT touch any file in the sibling commit agent's diff. Confirm `deploy-gated.yml` isn't in their diff.
- Read-only git commands only.
- Do not change staging step behavior. Production-only fix.
- If WO-0234 has already landed (it modifies the same file), rebase your fix on top of its output without conflict.

## Acceptance criteria

- Line 463 (or wherever the production deploy is) uses `--env "production"` (or no `--env`) with documented rationale.
- A new CI step verifies KV namespace binding post-deploy.
- `actionlint` passes on the modified workflow.
- Existing staging deploy behavior unchanged.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0232-result.md`
Blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0232-BLOCKED.md`

Report must include: line 463 before/after diff, rationale for `--env "production"` vs. omitting, KV-binding assertion implementation, actionlint output, "what would have caught this earlier" analysis.
