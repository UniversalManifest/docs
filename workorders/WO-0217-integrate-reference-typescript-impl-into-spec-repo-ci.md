# WO-0217: Integrate Reference TypeScript Implementation Into Spec Repo CI

**Status:** COMPLETED — um-typescript-conformance.yml workflow live (PR-gate + Monday cron); resolver-agnostic J04b variant created (J04 untouched for back-compat); IMPLEMENTING-UM.md ships; README + for-agents.md cross-linked
**Priority:** HIGH (P1)
**Depends on:** none
**Unblocks:** WO-0054 sustained closure (keeps external impl in sync, prevents silent divergence)
**Derived from:** 2026-04-26 resolver runtime drift scan, finding 3 (HIGH)

## Objective

`WO-0054` shipped an external public TypeScript reference implementation at `https://github.com/grigb/um-typescript` and `WO-0050` published the npm package contract. Today, the spec repo's CI does not exercise that implementation against its own contract — meaning the external impl can drift from the spec without anyone noticing until an adopter complains. Wire `um-typescript` into spec-repo CI as a conformance gate; provide a resolver-agnostic journey variant that any conformant implementation can satisfy; and update README/docs so external implementers know how to participate.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0054-reference-implementation-repository-typescript.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0050-*.md` (any file matching — npm/Lan→Um rename + package.json)
- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/CONTRACT.md`
- `/Users/grig/work/repo/universalmanifest/docs/journeys/J04-*.md` (or whatever the resolver journey is called)
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/ci.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/verify.yml`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-resolver-runtime-drift-scan.md`
- README of `https://github.com/grigb/um-typescript` (fetch via `gh repo view` or read remotely; no clone required)

## Work to perform

1. **Choose CI integration model** — three viable options: (a) git submodule, (b) `npm install grigb/um-typescript` in a CI job, (c) scheduled job that clones the external repo and runs its conformance tests against the spec repo's resolver. Pick (b) or (c); avoid (a) unless there's a strong reason.
2. **Add a CI job** — new job in `phase-9-gate.yml` or `verify.yml` (your call with rationale) that runs `um-typescript`'s conformance tests against the spec repo's contract. Fail the job if any conformance test fails.
3. **Resolver-agnostic journey** — `J04` (the resolver journey) is currently coupled to Cloudflare Worker tooling. Add a J04-variant or generalize J04 so any HTTP resolver implementation can run it. Adopters building Node.js/Go/Rust resolvers can then run J04 against their own server and prove conformance.
4. **Weekly conformance report** — add a scheduled CI job that runs the conformance tests and writes a summary report to `docs/reports/{date}-um-typescript-conformance.md`. Status visible at a glance.
5. **README cross-link** — at the top of the spec repo README, add a "Reference implementations" section listing `um-typescript` as "implementation #1" with a link and a note that more are welcome. Same on `for-agents/`.
6. **Documentation: how to fork and conform** — short doc at `docs/IMPLEMENTING-UM.md` (or similar) describing the steps to fork `um-typescript` as a starting point and run the conformance tests in CI.

## Files to modify / create

- `.github/workflows/phase-9-gate.yml` OR `.github/workflows/verify.yml` (new conformance job + scheduled job)
- `docs/journeys/J04-*.md` (resolver-agnostic variant or generalization)
- `docs/IMPLEMENTING-UM.md` (new) — how to fork & conform
- `README.md` (add "Reference implementations" section)
- `docs/reports/` (scheduled job writes here; nothing to commit by hand)
- `site/src/content/docs/for-agents.md` (cross-link)

## Constraints

- **Do not introduce circular dependencies.** `um-typescript` consumes the spec repo's contract; the spec repo must not consume `um-typescript`'s implementation. Conformance tests run in one direction only.
- **Keep the journey backwards-compatible.** J04's existing Cloudflare path stays runnable; the WO adds a generalization layer, not a replacement.
- Do not commit, push, stage, or branch. Sibling commit agent owns git mutations.
- Run `git status --short` first; respect their diff.
- Do not modify the external `um-typescript` repo as part of this WO. If changes are needed there, draft a follow-on WO targeted at that repo.

## Acceptance criteria

- New CI job runs `um-typescript` conformance tests against the spec repo's contract on every PR; fails loudly if conformance breaks.
- A scheduled job writes weekly conformance reports under `docs/reports/`.
- `J04` (or its resolver-agnostic sibling) can be pointed at any HTTP base URL via a flag/env var.
- README cross-links the reference implementation.
- `docs/IMPLEMENTING-UM.md` exists and describes the fork-and-conform path.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0217-result.md`
Blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0217-BLOCKED.md`

Report must include: chosen CI integration model with rationale, conformance job + scheduled job diffs, J04 generalization summary, README + IMPLEMENTING-UM.md content excerpts, "what would have caught WO-0054 drift earlier" analysis.
