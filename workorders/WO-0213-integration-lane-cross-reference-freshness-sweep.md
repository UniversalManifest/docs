# WO-0213: Integration-Lane Cross-Reference Freshness Sweep

**Status:** COMPLETED — NO-OP (publication-readiness nit was over-inclusive; 28 dates audited, all intentional vintage citations or filename references; 0 patched)
**Priority:** LOW (documentation hygiene; no spec or runtime impact)
**Depends on:** none
**Unblocks:** —
**Derived from:** 2026-04-24 v0.2 publication readiness scan, nit #3

## Objective

The publication readiness scan flagged that integration-lane docs (`integrations/*.md`) carry slightly stale dates on cross-references to decision artifacts (e.g., dates that predate WO-0190/0191/0192/0206 closures). Sweep all integration-lane and related cross-reference docs and reconcile dates so cited decisions match the canonical decision-artifact dates.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/integrations/` (all `*.md` files)
- `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md` (post-WO-0209 state)
- `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0190-additional-integrity-profile-decision-package.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0191-revocation-cursor-and-status-contract.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0192-conformance-suite-ttl-replay-and-security-expansion.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0206-k2b-drift-governance-artifact-contract-restoration.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-24-v0-2-publication-readiness-scan.md`

## Work to perform

1. **Enumerate cross-references** — grep across `integrations/*.md`, `docs/*.md`, and any other doc directory the readiness scan flagged for: dates (`YYYY-MM-DD`), `WO-0xxx` references, decision-artifact paths, and "as of" / "last updated" markers.
2. **Match each cross-reference against the authoritative date** — for each cited WO or decision-artifact, fetch the actual closure/landing date from `WO-INDEX.md`, the WO file's `**Status:**` block, or the file's git history if needed.
3. **Patch only stale entries** — update only dates that are demonstrably wrong. Do not "refresh" dates that are correctly reflecting an older artifact's intentional vintage.
4. **Do not modify decision content** — only date metadata.

## Files to modify

- Wherever stale dates are found. Most likely: `integrations/*.md`. Possibly: `docs/journeys/*.md`, `docs/reports/*.md` summary headers.

## Constraints

- **Date freshness only.** Do not reword content, restructure sections, or change technical claims.
- If a cross-reference's date can't be unambiguously matched to a canonical source, leave it alone and note it in the report for follow-up.
- Do not commit, push, stage, or branch.
- Do not touch any file in the sibling commit agent's diff. `git status --short` first.

## Acceptance criteria

- Every modified date traces back to a verifiable canonical source (WO closure, file commit date, decision-artifact filename timestamp).
- A single `before/after` table in the result report enumerates each patch.
- No content beyond date metadata is changed.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0213-result.md`
Blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-wo-0213-BLOCKED.md`

Report must include: full before/after date table, list of cross-references left unchanged with rationale, files modified (absolute paths).
