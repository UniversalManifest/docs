# WO-0233: Add Spec Publication Automation Workflow

**Status:** OBSOLETE 2026-04-28 — `.github/workflows/publish-spec.yml` was removed in revert commit `e493b3e` due to unauthorized creation. Original landing date was 2026-04-26; reverted along with the rest of the unauthorized CI infrastructure.
**Priority:** CRITICAL (P0)
**Depends on:** WO-0232 (production deploy must be correct before publication push); operationally, can be drafted in parallel
**Unblocks:** WO-0220 (tag publish path becomes auditable)
**Derived from:** 2026-04-26 deployment pipeline drift scan, finding 2 (CRITICAL)

## Objective

The publication wave (WO-0220 → WO-0231) cuts a tag and publishes spec artifacts, but no automation enforces the post-publication assertions documented in `docs/PUBLISHING-AND-VERSIONING.md` §8. Add a tag-triggered workflow that runs the entire publication-correctness checklist on every `spec-v*` tag and fails loudly on any drift.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/docs/PUBLISHING-AND-VERSIONING.md` (especially §8 — the assertion list)
- `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml` (precedent for tag-trigger / push-to-main patterns)
- `/Users/grig/work/repo/universalmanifest/.github/workflows/synthetic-monitoring.yml` (precedent for HTTP assertion patterns; WO-0215 just expanded this)
- `/Users/grig/work/repo/universalmanifest/.github/workflows/phase-9-gate.yml`
- `/Users/grig/work/repo/universalmanifest/site/public/.well-known/universal-manifest.json`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0220-v0-2-release-tag-and-immutable-artifact-hash-pinning.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0227-post-publish-smoke-ci-runnable-harness.md` (what the publication smoke harness will look like; this WO consumes that smoke contract from CI)
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-deployment-pipeline-drift-scan.md` (finding 2)

## Work to perform

1. **Create `.github/workflows/publish-spec.yml`** triggered on `push: tags: ['spec-v*']` plus `workflow_dispatch` for re-runs.
2. **Implement the §8 assertion list**:
   - `/spec/latest/` returns 200; body contains "Published Specification" (not "Draft").
   - `/spec/v0.2/` returns 200.
   - `https://universalmanifest.net/ns/universal-manifest/v0.2/schema.jsonld` served as `application/ld+json` with `Cache-Control: public, max-age=31536000, immutable`.
   - `https://universalmanifest.net/ns/universal-manifest/v0.2/schema.json` served as `application/schema+json` or `application/json` with the same immutability header.
   - CORS header present on both schema URLs.
   - `.well-known/universal-manifest.json` declares the freshly tagged `versions.stable` (e.g., `"v0.2"` after this push).
   - Migration guide URL returns 200.
   - All governance pages (RFC, breaking-change, deprecation, incident) return 200.
3. **Hash verification** — re-fetch the canonical schema URLs and compare to the SHA-256 hashes recorded in WO-0220's changelog edit. Fail on mismatch.
4. **Result report** — write to `.dev/ai/reports/publish/{date}-spec-publication.md` (tracked dir, not `.dev/ai/subtask-comms/`).
5. **Failure semantics** — no `continue-on-error`. Any assertion failure fails the workflow loudly. Surface the failure to the same alerting channel as `synthetic-monitoring.yml` if a webhook is configured.

## Files to modify / create

- `.github/workflows/publish-spec.yml` (new)
- `docs/reports/publish/` (new directory; commit a `.gitkeep` if the publication report mechanism needs it)
- `docs/CRITICAL-PATH.md` Phase 9 section may want a one-line note pointing at the new workflow (low priority; orchestrator can absorb later)

## Constraints

- Do not change `docs/PUBLISHING-AND-VERSIONING.md` content. Read-only.
- Do not include any secret literals. If alerting needs a webhook, reuse the synthetic-monitoring secret name pattern; document it.
- Do not commit, push, stage, or branch.
- Run `git status --short` first; respect sibling commit agent's diff.
- The workflow must be syntactically valid YAML; run `actionlint` if available.
- Do not deploy anything from the workflow.

## Acceptance criteria

- New `publish-spec.yml` exists and triggers on `spec-v*` tags.
- All 8 PUBLISHING-AND-VERSIONING §8 assertions covered.
- Hash verification step compares against WO-0220 changelog hashes (handle the case where WO-0220 hasn't run yet — fail with a clear message).
- `actionlint` clean.
- No `continue-on-error`.
- Result-report path matches the WO's contract and is gitkeep-friendly.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0233-result.md`
Blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0233-BLOCKED.md`

Report must include: workflow YAML diff, per-assertion implementation summary, hash-verification logic, actionlint output, "what would have caught WO-0156 / WO-0205 / WO-0206 publication-readiness drift earlier" analysis.
