# WO-0220: v0.2 Release Tag, GitHub Release, and Immutable Artifact Hash Pinning

**Status:** PREP COMPLETE — awaiting operator to run `git tag -a spec-v0.2` + `git push origin spec-v0.2` + `gh release create spec-v0.2` (commands inlined in `.dev/ai/subtask-comms/2026-04-26-wo-0220-result.md`)
**Priority:** P0 (head of publication wave; blocks all downstream WOs)
**Depends on:** none
**Unblocks:** WO-0221 through WO-0231
**Derived from:** 2026-04-26 v0.2 publication push plan, item 1; `docs/PUBLISHING-AND-VERSIONING.md` §5.1 (immutable versions); `docs/RELEASING.md` §2 step 7

## Objective

Cut the v0.2 publication tag in git, create a GitHub release that lists the canonical artifact URLs and their SHA-256 hashes, and pin those hashes in the changelog so any future drift in `site/public/ns/universal-manifest/v0.2/` is detectable.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/docs/PUBLISHING-AND-VERSIONING.md`
- `/Users/grig/work/repo/universalmanifest/docs/RELEASING.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/schema.json`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/schema.jsonld`
- `/Users/grig/work/repo/universalmanifest/site/public/ns/universal-manifest/v0.2/schema.json`
- `/Users/grig/work/repo/universalmanifest/site/public/ns/universal-manifest/v0.2/schema.jsonld`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/publishing/changelog.md`

## Work to perform

1. **Confirm artifact byte-for-byte identity.** Hash both pairs:
   - `shasum -a 256 spec/v0.2/schema.json` vs `shasum -a 256 site/public/ns/universal-manifest/v0.2/schema.json`
   - same for `schema.jsonld`
   If the published mirror diverges from the spec source, STOP and write a BLOCKED report; do not tag drift.
2. **Record canonical hashes.** Add a "v0.2 publication artifact hashes" subsection to `site/src/content/docs/publishing/changelog.md` listing both files' SHA-256 hashes and the canonical URLs (`https://universalmanifest.net/ns/universal-manifest/v0.2/...`).
3. **Cut the git tag** locally:
   - `git tag -a spec-v0.2 -m "Universal Manifest v0.2 published"` (use existing project tag convention; if the repo has no precedent the planner suggests `spec-v0.2` to avoid colliding with future SDK package tags — confirm with operator before pushing).
4. **Create the GitHub release** (manual `gh release create` command — DO NOT execute as the work order; produce the exact command in the result report for the operator to run):
   - Title: "Universal Manifest v0.2"
   - Body: lists artifact URLs, hashes, and links to `/spec/latest/`, `/publishing/changelog/`, `docs/guides/MIGRATION-V01-V02.md`.
5. **Verify the release-cadence governance doc** (`docs/governance/RELEASE-CADENCE.md`) does not contradict this release; if it specifies a different tag convention, adopt that convention and note the deviation.

## Files to modify

- `site/src/content/docs/publishing/changelog.md` — add publication-artifact-hashes subsection under the v0.2 (Draft → Published) heading.
- `docs/RELEASING.md` — only if step 7's tag convention is currently ambiguous (`vX.Y.Z`); pin it to whatever convention this WO adopts.

Do NOT execute `git tag` or `gh release create` from inside the WO. Produce the exact commands; an operator runs them outside the agent boundary so the tag pushes from a credentialed terminal.

## Constraints

- **Read-only on `spec/v0.2/`** — the spec source must not change. This WO is a metadata/release-engineering operation only.
- **No commits, no pushes from the agent.** Operator owns the release cut.
- **Hashes must be reproducible.** If any future agent regenerates the artifacts, the hashes must still match. Confirm by hashing twice with a 30-second gap.

## Acceptance criteria

- `site/src/content/docs/publishing/changelog.md` contains the v0.2 publication-artifact hashes subsection with both SHA-256 hashes and both canonical URLs.
- The result report includes the exact `git tag` and `gh release create` command strings the operator should run, with the body content inlined.
- Hash verification logged in the result report: `spec/v0.2/schema.json` matches `site/public/ns/universal-manifest/v0.2/schema.json` byte-for-byte; same for `schema.jsonld`.
- If `docs/RELEASING.md` was edited, the diff is included in the result report.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0220-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0220-BLOCKED.md`
