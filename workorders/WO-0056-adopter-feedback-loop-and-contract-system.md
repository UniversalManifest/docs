# WO-0056 — Adopter Feedback Loop and Contract System

**Status:** COMPLETED
**Created:** 2026-02-27
**Priority:** HIGH
**Blocks:** Gate G4 (Interoperability proof — sustains adopter relationships), Gate G6 (Governance and change control)
**Dependencies:** WO-0053 (Conformance Test Suite), WO-0055 (Adopter Onboarding Document Package)
**Estimated effort:** 1-2 weeks

## Objective

Establish a structured feedback loop between the UM project and external adopters, including: a feedback submission mechanism, triage and response SLA commitments, adopter progress tracking, a spec improvement queue, and regression prevention gates. This ensures that adopter friction is captured, triaged, and resolved systematically.

## Why this work matters

Gate G4 requires 3+ independent implementations. Getting adopters to start is necessary but not sufficient; the project must also:

1. Capture feedback from adopters encountering spec ambiguity or tooling gaps.
2. Respond to feedback within predictable timelines so adopters do not stall.
3. Track adopter progress toward conformance (machine-readable).
4. Route spec improvements from adopter feedback into the spec update queue.
5. Prevent regressions: ensure spec changes do not break existing adopter implementations.

Without a structured feedback system, adopter relationships degrade into ad-hoc conversations, feedback is lost, and spec improvements are delayed.

## Scope

In scope:

- GitHub Issues templates for adopter feedback (conformance questions, spec ambiguity, tooling bugs).
- Feedback triage labels and response SLA documentation.
- Adopter progress tracker (machine-readable JSON + human-readable dashboard concept).
- Spec improvement queue: process for routing adopter feedback into spec changes.
- Regression prevention: conformance suite version pinning and backward-compatibility gates.

Out of scope:

- Building a full project management system.
- Paid support contracts.
- Automated adopter onboarding (handled by WO-0055).

## Execution phases

### Phase 1 — Feedback submission mechanism (GitHub Issues templates)

- [x] Create structured GitHub Issues templates:
  - **Conformance Question**: "I am implementing UM and the spec is unclear about X."
    - Fields: spec version, conformance level, section reference, question.
  - **Spec Ambiguity Report**: "The spec says X but could be interpreted as Y."
    - Fields: spec version, section, current text, proposed clarification.
  - **Implementation Bug Report**: "The conformance suite or reference implementation has a bug."
    - Fields: suite version, fixture, expected vs. actual, reproduction steps.
  - **Feature Request**: "My use case requires X which is not in the current spec."
    - Fields: use case description, proposed addition, conformance impact.
- [x] Each template includes structured labels for triage automation.

### Phase 2 — Feedback triage and response SLA

- [x] Document SLA commitments in `docs/governance/ADOPTER-SLA.md`:
  - **Conformance questions**: Acknowledged within 48 hours, answered within 1 week.
  - **Spec ambiguity reports**: Acknowledged within 48 hours, resolution (clarification or "wontfix" with rationale) within 2 weeks.
  - **Implementation bug reports**: Acknowledged within 24 hours, fix or workaround within 1 week.
  - **Feature requests**: Acknowledged within 1 week, disposition (accepted/deferred/rejected with rationale) within 1 month.
- [x] Define triage labels:
  - `adopter-feedback`, `conformance-question`, `spec-ambiguity`, `implementation-bug`, `feature-request`
  - Priority: `p0-blocker`, `p1-high`, `p2-medium`, `p3-low`
  - Status: `triage`, `acknowledged`, `in-progress`, `resolved`, `wontfix`
- [x] Document the triage process (who triages, when, escalation path).

### Phase 3 — Adopter progress tracking

- [x] Define `adopters/` directory structure in spec repo:
  ```
  adopters/
    registry.json       # machine-readable adopter registry
    README.md           # how to register as an adopter
  ```
- [x] Define `registry.json` schema:
  ```json
  {
    "adopters": [
      {
        "name": "Acme UM Validator",
        "organization": "Acme Corp",
        "repository": "https://github.com/acme/um-validator",
        "language": "python",
        "targetConformanceLevels": ["v0.1-baseline", "v0.2-baseline"],
        "currentStatus": "in-progress",
        "conformanceReportUrl": null,
        "registeredDate": "2026-03-01T00:00:00Z",
        "lastUpdated": "2026-03-15T00:00:00Z",
        "contact": "adopter-lead@acme.com"
      }
    ]
  }
  ```
- [x] Document how adopters register (pull request to add themselves to `registry.json`).
- [x] Document how adopters update their status (pull request with updated conformance report URL).

### Phase 4 — Spec improvement queue from adopter feedback

- [x] Define the process for routing adopter feedback into spec changes:
  1. Adopter files issue using template.
  2. Maintainer triages and labels.
  3. If spec change needed: create RFC (per `docs/governance/RFC-TEMPLATE.md`).
  4. RFC is reviewed with backward-compatibility impact assessment.
  5. If approved: implement spec change, update conformance fixtures, bump suite version.
  6. Notify affected adopters.
- [x] Create a `docs/governance/SPEC-IMPROVEMENT-QUEUE.md` tracking active RFCs from adopter feedback.
- [x] Link this process to the existing governance framework in `docs/governance/GOVERNANCE.md`.

### Phase 5 — Regression prevention gates

- [x] Define backward-compatibility rules for conformance suite changes:
  - New fixtures may be ADDED without breaking existing adopters.
  - Existing fixture expected results may NOT change without a major version bump.
  - Suite version follows semver: major = breaking, minor = new fixtures, patch = bug fixes.
- [x] Add a CI check to the spec repo that:
  - Runs the conformance suite against the reference implementation on every PR.
  - Flags if any previously-passing fixture now fails.
- [x] Document the regression prevention policy in `docs/governance/REGRESSION-PREVENTION.md`.
- [x] Include in the conformance runner a `--baseline` flag that tests only the fixtures from a specified suite version (allowing adopters to pin to a known-good version while upgrading).

## Key file paths (created/modified)

New files:
- `/Users/grig/work/repo/universalmanifest/.github/ISSUE_TEMPLATE/conformance-question.yml`
- `/Users/grig/work/repo/universalmanifest/.github/ISSUE_TEMPLATE/spec-ambiguity.yml`
- `/Users/grig/work/repo/universalmanifest/.github/ISSUE_TEMPLATE/implementation-bug.yml`
- `/Users/grig/work/repo/universalmanifest/.github/ISSUE_TEMPLATE/feature-request.yml`
- `/Users/grig/work/repo/universalmanifest/docs/governance/ADOPTER-SLA.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/SPEC-IMPROVEMENT-QUEUE.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/REGRESSION-PREVENTION.md`
- `/Users/grig/work/repo/universalmanifest/adopters/registry.json`
- `/Users/grig/work/repo/universalmanifest/adopters/README.md`

Modified files:
- `/Users/grig/work/repo/universalmanifest/.github/ISSUE_TEMPLATE/` (may need to update existing templates)
- `/Users/grig/work/repo/universalmanifest/docs/governance/GOVERNANCE.md` (link to new processes)
- `/Users/grig/work/repo/universalmanifest/conformance/runner/` (add `--baseline` flag, from WO-0053)

## Acceptance criteria

- [x] All four GitHub Issues templates are functional and produce structured, labeled issues.
- [x] SLA document exists with specific timelines for each feedback type.
- [x] Adopter registry schema is defined and an example entry (reference implementation) is populated.
- [x] Spec improvement queue process is documented and linked to existing RFC template.
- [x] Regression prevention policy is documented with clear rules for suite versioning.
- [x] CI check runs conformance suite on spec repo PRs and flags regressions.
- [x] An external adopter can:
  - Register their implementation in the adopter registry via PR.
  - File a conformance question and receive acknowledgment within SLA.
  - See the status of their feedback in the issue tracker.
  - Pin their conformance suite version to avoid unexpected breakage.

## Validation commands

- Verify GitHub Issues templates render correctly in the GitHub UI.
- `jsonschema validate adopters/registry.json` (registry validates against its schema)
- `cd /Users/grig/work/repo/universalmanifest && npm test` (existing tests still pass)
- CI conformance regression check passes on a clean PR.

## Dependencies and sequencing notes

- Depends on WO-0053 (conformance suite must exist for regression prevention and version pinning).
- Depends on WO-0055 (adopter onboarding package defines the first-contact experience; this WO handles ongoing relationship).
- Coordinate with WO-0059 (governance completion) to ensure SLA and regression policies are consistent with broader governance framework.
- Existing GitHub Issues templates in `.github/ISSUE_TEMPLATE/` may need to be reconciled with the new adopter-specific templates.

## Execution summary (2026-03-02)

Completed with deliverables:

- Structured GitHub templates under `/Users/grig/work/repo/universalmanifest/.github/ISSUE_TEMPLATE/`
- Governance docs:
  - `/Users/grig/work/repo/universalmanifest/docs/governance/ADOPTER-SLA.md`
  - `/Users/grig/work/repo/universalmanifest/docs/governance/SPEC-IMPROVEMENT-QUEUE.md`
  - `/Users/grig/work/repo/universalmanifest/docs/governance/REGRESSION-PREVENTION.md`
- Adopter registry:
  - `/Users/grig/work/repo/universalmanifest/adopters/registry.json`
  - `/Users/grig/work/repo/universalmanifest/adopters/README.md`
- Conformance runner baseline support (`--baseline`) in:
  - `/Users/grig/work/repo/universalmanifest/conformance/runner/src/cli.mjs`
  - `/Users/grig/work/repo/universalmanifest/conformance/runner/src/core.mjs`
- CI regression gate in:
  - `/Users/grig/work/repo/universalmanifest/.github/workflows/ci.yml`

Evidence:

- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/2026-03-02-wo-0056-execution-report.md`
- Agent Task ID preserved: `e0a7fe60_1772165606`
