# WO-0059 — Governance Completion (Breaking-Change, Deprecation, Incident)

**Status:** COMPLETED
**Created:** 2026-02-27
**Priority:** CRITICAL
**Blocks:** Gate G6 (Governance and change control), World-ready additional checks (incident/rollback procedures)
**Dependencies:** WO-0058 (Migration Guide — deprecation policy feeds into this)
**Estimated effort:** 2 weeks

## Objective

Complete all remaining governance documentation and operational proof required by Gate G6 and the World-ready checklist: breaking-change handling policy, deprecation and migration policy, incident/rollback procedures. Then simulate and test one incident/rollback cycle with captured evidence.

## Why this work matters

The Done-Done Checklist (Gate G6) explicitly requires:

- "Breaking-change handling is explicit" -- currently not documented.
- "Deprecation and migration policy is explicit" -- partially addressed by WO-0058 but needs broader policy.
- "Incident/rollback procedures are documented and tested" -- World-ready requirement, currently not met.
- "Long-term governance and release cadence are demonstrated" -- partially met, needs operational proof.

The remaining-gaps summary identifies Gate G6 as "partially met" and incident/rollback as "not met." Without closing these gaps, 1.0 World-ready claims cannot be made.

## Scope

In scope:

- Breaking-change handling policy document.
- Deprecation and migration policy document (broader than v0.1-to-v0.2 from WO-0058).
- Incident/rollback procedures document.
- One simulated incident/rollback cycle with evidence.
- Long-term release cadence documentation.
- Update to Done-Done Checklist with Gate G6 evidence paths.

Out of scope:

- Implementing automated incident detection (future operational hardening).
- Defining governance for a multi-organization steering committee (post-1.0).
- Changing the governance framework structure (WO-0051 already established it).

## Execution phases

### Phase 1 — Breaking-change handling policy

- [x] Create `docs/governance/BREAKING-CHANGE-POLICY.md`:
  ```
  1. Definition of a Breaking Change
     - Any change to normative spec text that causes a previously-conformant
       implementation to become non-conformant.
     - Any change to conformance fixtures that causes a previously-passing
       implementation to fail.
     - Any change to required fields, field semantics, or validation rules.
     - NOT a breaking change: adding new optional fields, adding new fixtures,
       clarifying ambiguous text without changing semantics.

  2. Breaking Change Process
     Step 1: File an RFC per docs/governance/RFC-TEMPLATE.md.
     Step 2: RFC MUST include:
       - Backward-compatibility impact assessment.
       - Migration path for affected adopters.
       - Timeline for adoption (minimum 3 months notice).
     Step 3: RFC is reviewed by maintainers.
     Step 4: If approved, breaking change is implemented in the NEXT major
              or minor spec version (never in a patch).
     Step 5: All affected adopters are notified via GitHub Issues and
              the adopter registry (WO-0056).
     Step 6: Old version continues to be supported per deprecation policy.

  3. Emergency Breaking Changes
     - Security vulnerabilities may require expedited breaking changes.
     - Emergency process: 48-hour review, immediate implementation,
       adopter notification within 24 hours.
     - Must still include migration path.

  4. Breaking Change Log
     - All breaking changes are recorded in CHANGELOG.md with:
       - Spec version, date, description, migration path link.
  ```

### Phase 2 — Deprecation and migration policy (general)

- [x] Create `docs/governance/DEPRECATION-POLICY.md` (if not already created by WO-0058, expand it):
  - General deprecation rules for any spec version:
    - Minimum support period after successor version reaches stable: 6 months.
    - Deprecation notice: published in spec docs, announced via GitHub.
    - During deprecation: security fixes only, no new features.
    - After end-of-life: conformance fixtures remain for historical testing, marked as legacy.
  - Version lifecycle states: `draft` -> `stable` -> `deprecated` -> `end-of-life`.
  - Specific timeline for v0.1 deprecation (coordinated with WO-0058).
- [x] Link deprecation policy to breaking-change policy and to the v0.1-to-v0.2 migration guide.

### Phase 3 — Incident/rollback procedures

- [x] Create `docs/governance/INCIDENT-RESPONSE.md`:
  ```
  1. Incident Categories
     a. Spec Defect: normative text is incorrect or ambiguous in a way
        that causes implementation failures.
     b. Conformance Suite Bug: test fixture or expected result is wrong.
     c. Publication Failure: spec artifacts at stable URLs are incorrect
        or unavailable.
     d. Security Vulnerability: spec design enables an attack vector.

  2. Incident Response Process
     Step 1: Detect — via adopter report, CI failure, or manual review.
     Step 2: Triage — assign severity (P0-critical, P1-high, P2-medium).
     Step 3: Communicate — notify affected parties within:
       - P0: 4 hours
       - P1: 24 hours
       - P2: 1 week
     Step 4: Investigate — determine root cause and scope of impact.
     Step 5: Fix — implement correction:
       - Spec defect: publish errata or corrected version.
       - Suite bug: publish corrected fixtures with patch version bump.
       - Publication failure: redeploy correct artifacts.
       - Security: follow emergency breaking-change process.
     Step 6: Verify — run conformance suite, verify production endpoints.
     Step 7: Communicate resolution — update incident report, notify adopters.
     Step 8: Retrospective — document lessons learned, update processes.

  3. Rollback Procedures
     a. Spec Rollback:
        - Revert normative text to previous version.
        - Publish revert at stable URLs.
        - Bump patch version.
        - Notify adopters.
     b. Conformance Suite Rollback:
        - Revert to previous suite version tag.
        - Publish corrected suite.
        - Adopters can pin to known-good version.
     c. Publication Rollback:
        - Redeploy previous artifact set to Cloudflare Pages.
        - Verify stable URLs return correct content.
        - Smoke test production endpoints.

  4. Incident Report Template
     - Incident ID, date, severity, category.
     - Description, root cause, impact assessment.
     - Timeline of response actions.
     - Resolution, verification evidence.
     - Lessons learned, process improvements.
  ```

### Phase 4 — Simulated incident/rollback cycle

- [x] Execute one full incident simulation with evidence capture:
  - **Scenario**: Simulate a "conformance suite bug" incident:
    1. Introduce a deliberate error in one conformance fixture expected result.
    2. Detect: CI pipeline flags the failure.
    3. Triage: Assign P1 severity.
    4. Communicate: Draft adopter notification.
    5. Fix: Correct the fixture, bump suite patch version.
    6. Verify: Run conformance suite, confirm pass.
    7. Rollback verification: Demonstrate that reverting to previous suite version also works.
    8. Retrospective: Document the simulation.
  - Capture evidence:
    - CI failure screenshot/log.
    - Corrected fixture diff.
    - Suite version bump commit.
    - Conformance suite pass after fix.
    - Retrospective report.
- [x] Publish simulation evidence at:
  - `/Users/grig/work/repo/universalmanifest/docs/reports/YYYY-MM-DD-incident-simulation-evidence.md`

### Phase 5 — Release cadence documentation

- [x] Document in `docs/governance/RELEASE-CADENCE.md`:
  - Spec release cadence: new minor/major versions as needed, not on a fixed schedule.
  - Conformance suite release cadence: patch releases for bug fixes, minor for new fixtures.
  - Minimum review period for spec changes: 2 weeks for non-breaking, 3 months for breaking.
  - Release checklist reference: `docs/DONE-DONE-CHECKLIST.md`.
- [x] Document in `docs/RELEASING.md` (if it does not exist, or update if it does):
  - Step-by-step release process for spec versions.
  - Step-by-step release process for conformance suite versions.
  - Who can release, approval requirements.

### Phase 6 — Gate G6 evidence and checklist update

- [x] Update `docs/DONE-DONE-CHECKLIST.md` Gate G6 section with evidence paths:
  - `docs/governance/BREAKING-CHANGE-POLICY.md`
  - `docs/governance/DEPRECATION-POLICY.md`
  - `docs/governance/INCIDENT-RESPONSE.md`
  - `docs/governance/RELEASE-CADENCE.md`
  - `docs/reports/YYYY-MM-DD-incident-simulation-evidence.md`
- [x] Update `docs/STATE-OF-THE-PROJECT.md` to reflect G6 closure.

## Key file paths (created/modified)

New files:
- `/Users/grig/work/repo/universalmanifest/docs/governance/BREAKING-CHANGE-POLICY.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/DEPRECATION-POLICY.md` (or expand if created by WO-0058)
- `/Users/grig/work/repo/universalmanifest/docs/governance/INCIDENT-RESPONSE.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/RELEASE-CADENCE.md`
- `/Users/grig/work/repo/universalmanifest/docs/RELEASING.md` (if not existing)
- `/Users/grig/work/repo/universalmanifest/docs/reports/YYYY-MM-DD-incident-simulation-evidence.md`

Modified files:
- `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-CHECKLIST.md` (G6 evidence paths)
- `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md` (G6 status update)
- `/Users/grig/work/repo/universalmanifest/docs/governance/GOVERNANCE.md` (link to new policies)
- `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md` (record governance decisions)

## Acceptance criteria

- [x] Breaking-change handling policy exists with clear definition, process, emergency process, and change log requirement.
- [x] Deprecation policy exists with version lifecycle states, minimum support periods, and specific v0.1 timeline.
- [x] Incident/rollback procedures exist with categories, response process, rollback procedures, and report template.
- [x] One incident/rollback simulation has been executed with captured evidence (CI failure, fix, verify, retrospective).
- [x] Release cadence is documented for both spec and conformance suite.
- [x] `docs/RELEASING.md` exists with step-by-step release process.
- [x] Done-Done Checklist Gate G6 evidence paths are updated.
- [x] All governance docs are cross-linked from `docs/governance/GOVERNANCE.md`.
- [x] No unresolved policy contradictions across governance docs (verified by manual review).

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean` (site builds)
- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test` (tests pass)
- Manual review of all governance documents for completeness and internal consistency.
- Verify incident simulation evidence report contains all required sections.

## Dependencies and sequencing notes

- Depends on WO-0058 (migration guide) for the deprecation policy foundation specific to v0.1-to-v0.2.
- The incident simulation (Phase 4) depends on WO-0053 (conformance suite) existing so it can be used in the simulation.
- Coordinate with WO-0056 (adopter feedback loop) to ensure incident procedures align with adopter SLA commitments.
- This is the final work order required for Gate G6 closure. Once complete, Gate G6 evidence can be compiled.
- Existing governance framework from WO-0051 (`docs/governance/GOVERNANCE.md`, `docs/governance/RFC-TEMPLATE.md`) provides the foundation; this WO fills the remaining gaps.

## Execution summary (2026-03-02)

Completed with governance policy set and incident simulation evidence:

- `/Users/grig/work/repo/universalmanifest/docs/governance/BREAKING-CHANGE-POLICY.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/DEPRECATION-POLICY.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/INCIDENT-RESPONSE.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/RELEASE-CADENCE.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-02-incident-simulation-evidence.md`
- `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-CHECKLIST.md` updated with Gate G6 evidence paths
- `/Users/grig/work/repo/universalmanifest/docs/RELEASING.md` expanded with conformance-suite release process and approval rules

Evidence:

- Incident simulation logs + reports in runner artifacts and report document.
- Agent Task ID preserved: `e0a7fe60_1772165606`
