# WO-0256: External Reader Validation Execution

**Status:** BLOCKED — requires WO-0253, WO-0254, WO-0255, and a real external-reader cohort/process
**Priority:** P1 (post-publication quality evidence; not a v0.2 release gate)
**Depends on:** WO-0214, WO-0243, WO-0253, WO-0254, WO-0255
**Unblocks:** follow-on comprehension/copy/IA WOs from real reader evidence
**Derived from:** WO-0214; WO-0243 Phase 19 stub; 2026-05-02 objective realignment

## Problem

Post-publication external-reader evidence does not exist. `WO-0214` correctly blocks on a real cohort and forbids simulated readers.

Reader validation also should not run until the redesigned homepage cluster is implemented and production routes are verified, otherwise the cohort would be testing a known-rejected or broken public experience.

## Objective

Execute real first-time-reader validation against the redesigned, production-verified Universal Manifest public reader path.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0214-post-publication-external-human-reader-validation.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0253-homepage-cluster-design-direction-package.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0254-implement-approved-homepage-cluster-redesign.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0255-public-route-and-deployment-verification-v0-2-reader-path.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-04-30-v0-2-publication-evidence-pack.md`
- The delivered `WO-0255` production verification report.

## Work to perform

1. Confirm prerequisites:
   - approved design report exists
   - redesigned homepage cluster is implemented
   - production routes are verified
   - real reader cohort and consent/process are available
2. Recruit or receive 3 to 5 external readers covering as many of these modes as possible:
   - first-time curious reader
   - product/platform decision-maker
   - developer or standards reader
   - ecosystem-specific reader
3. Run the read-and-comment protocol:
   - enter at the homepage
   - inspect the homepage cluster
   - find the current spec
   - answer comprehension questions about what UM is, what it carries, and where adoption would begin
4. Capture notes, timings, friction points, and verbatim confusion quotes.
5. Synthesize findings into a report and create follow-on WOs for confirmed high-severity comprehension failures.

## Files to modify / create

- Create `/Users/grig/work/repo/universalmanifest/docs/reports/{date}-external-human-reader-validation-v0-2.md`
- Optional follow-on WO files for confirmed copy, IA, design, or route issues.

## Constraints

- Do not simulate external readers.
- Do not fabricate transcripts, quotes, timings, or consent.
- Do not silently rewrite the site from findings; create follow-on WOs.
- Do not claim reader-validation completion with fewer than 3 real external readers unless the report explicitly marks the evidence as incomplete.

## Acceptance criteria

- Evidence report exists with cohort composition, protocol, notes/transcripts, friction points, and recommendations.
- At least 3 real external-reader sessions are represented.
- Findings distinguish what the redesign clarified from what remains confusing.
- High-severity comprehension failures are converted into follow-on WOs.
- The report explicitly compares real reader findings against the earlier AI-simulated validation assumptions from WO-0194/WO-0214.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0256-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0256-BLOCKED.md`
