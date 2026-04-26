# WO-0225: Governance + RFC-Mechanism Cross-Link from Published Spec

**Status:** NOT_STARTED
**Priority:** P1 (publication completeness)
**Depends on:** WO-0221
**Unblocks:** none
**Derived from:** 2026-04-26 v0.2 publication push plan, items 8 and 4 (governance trigger surfacing); WO-0051 (RFC mechanism, if separate WO exists), WO-0059 (governance completion)

## Objective

Make the RFC mechanism, breaking-change policy, deprecation policy, and incident-response policy reachable in one click from the published spec page. Replace the `RFC_HREF` and `BREAKING_CHANGE_HREF` placeholders left by WO-0221.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/docs/governance/RFC-TEMPLATE.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/SPEC-IMPROVEMENT-QUEUE.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/BREAKING-CHANGE-POLICY.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/DEPRECATION-POLICY.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/INCIDENT-RESPONSE.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/governance/` (mirror set)
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0059-governance-completion-breaking-change-deprecation-incident.md`
- `/Users/grig/work/repo/universalmanifest/docs/W3C-STYLE-SPEC.html` (placeholders from WO-0221)

## Work to perform

1. **Replace the WO-0221 placeholders** in the spec page Status-of-This-Document section:
   - `RFC_HREF` → `https://universalmanifest.net/governance/spec-improvement-queue/` (or RFC-TEMPLATE if that is the canonical adopter entry — verify with the existing site mirror)
   - `BREAKING_CHANGE_HREF` → `https://universalmanifest.net/governance/breaking-change-policy/`
2. **Add a Normative References subsection** in the spec body (or extend the existing one) listing:
   - Breaking-Change Policy (`/governance/breaking-change-policy/`)
   - Deprecation Policy (`/governance/deprecation-policy/`)
   - Incident Response (`/governance/incident-response/`)
   - Release Cadence (`/governance/release-cadence/`)
   - Spec Improvement Queue (`/governance/spec-improvement-queue/`)
3. **Verify the governance mirror is current.** Each `site/src/content/docs/governance/*.md` should match its `docs/governance/` source-of-truth markdown. Note any drift in the result report; do not fix here.
4. **Confirm the RFC mechanism's adopter-facing URL is one click from the spec page.** If it is not currently linked from any reading path, add a single link from the published spec.

## Files to modify

- `docs/W3C-STYLE-SPEC.html` (replace placeholders + extend Normative References section)
- Optional: `site/src/content/docs/governance/index.md` if a governance landing page does not exist and one is needed for the cross-link target

## Constraints

- **Do not change governance content.** Linking only.
- **Do not introduce new policies.** All policies referenced exist (per WO-0059).
- **No spec-body normative requirement changes.**

## Acceptance criteria

- No `RFC_HREF` or `BREAKING_CHANGE_HREF` placeholders remain in `docs/W3C-STYLE-SPEC.html`.
- A reader on `/spec/v0.2/` can click into the breaking-change policy, deprecation policy, incident response, release cadence, and spec-improvement queue (RFC) directly.
- Any governance-mirror drift between `docs/governance/` and `site/src/content/docs/governance/` is documented in the result report (not necessarily fixed).
- `npm run build` passes.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0225-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0225-BLOCKED.md`
