# WO-0214: Post-Publication External-Human First-Time-Reader Validation

**Status:** NOT_STARTED — DEFERRED to post-v0.2 publication
**Priority:** MEDIUM (quality evidence; intentionally not a release gate per WO-0194)
**Depends on:** v0.2 publication push (whatever WO sequence the publication wave produces)
**Unblocks:** —
**Derived from:** 2026-04-24 v0.2 publication readiness scan, nit #2; WO-0194 evidence-pack scope

## Objective

WO-0194 packaged AI-simulated first-time-reader validation evidence and explicitly chose NOT to make external-human reader testing a release gate. Now that the Home-cluster rollout (WO-0195–WO-0205) has reshaped the public reader path, a real external-human pass — performed AFTER v0.2 publication — should validate the published reader experience and surface any comprehension drift the AI simulation didn't catch.

## Trigger condition

Do NOT execute this WO until v0.2 publication has shipped. Watch for:
- v0.2 release tag pushed and visible
- `/spec/latest/` banner reflecting v0.2 as published-not-draft (or whatever surface change accompanies publication)
- Public announcement copy visible

Once those are in place, this WO is unblocked.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0194-first-time-reader-validation-evidence-pack.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0035-human-reader-testing-policy-and-onboarding-evidence-alignment.md` (policy precedent)
- `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md` (Home-cluster post-rollout reader path)
- The current published `/spec/latest/`, `/`, and Home-cluster routes (read site source under `site/src/pages/` and `site/src/data/home-cluster.ts`)
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-v0-2-publication-readiness-scan.md`

## Work to perform

1. **Define a small reader cohort** (3–5 external readers) covering at least: a developer with no prior UM context, a privacy/identity practitioner, and a non-technical adopter (e.g., creator/owner persona). User can supply candidates.
2. **Define the read-and-comment protocol** — minimal: enter at `/`, read forward through the Home cluster, attempt to find the v0.2 spec, read enough to answer 3 comprehension questions (TBD: e.g., "what is a manifest?" / "what does v0.2 add over v0.1?" / "where would you start to integrate?"). Capture timings, friction points, and verbatim confusion quotes.
3. **Run the cohort** — coordinate with the user; do not assume agents-only execution. This WO produces an evidence pack but the actual reading is human.
4. **Synthesize findings** — create `docs/reports/{date}-external-human-reader-validation-v0-2.md` with: cohort composition, transcript excerpts, ranked friction points, recommendations.
5. **Open follow-on WOs** for any comprehension drift severe enough to warrant copy or IA changes. Do NOT silently rewrite without proposing first.

## Files to modify / create

- `docs/reports/{date}-external-human-reader-validation-v0-2.md` (new)
- Optionally: WO files for follow-on copy/IA work, named `WO-02xx-*`, in `docs/workorders/`

## Constraints

- This is **not** a release gate. v0.2 ships before this WO runs. Do not block publication on it.
- Do not pre-suppose findings. The AI-simulated evidence in WO-0194 is a hypothesis; this WO tests the hypothesis.
- Do not commit, push, stage, or branch. Reports are working-tree artifacts.
- If the cohort cannot be assembled, mark BLOCKED and document what's missing.

## Acceptance criteria

- An evidence-pack report exists at `docs/reports/{date}-external-human-reader-validation-v0-2.md` with at least 3 external-reader transcripts.
- Friction points are ranked by severity with verbatim quotes.
- Any recommended copy/IA changes are captured as follow-on WO drafts, not silent edits.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0214-result.md`
Blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0214-BLOCKED.md`

Report must include: cohort summary, evidence-pack file path, list of follow-on WO drafts (with files), and a "what AI simulation missed vs. caught" comparison against WO-0194's evidence.
