# WO-0190 -- Additional Integrity Profile Decision Package

**Status:** PLANNED
**Priority:** P2
**Created:** 2026-04-13

## Objective

Decide whether and when Universal Manifest should add integrity-profile guidance beyond the current v0.2 JCS + Ed25519 baseline.

## Context

The current state explicitly lists additional integrity profiles such as Data Integrity / RDF canonicalization as not yet finalized. That question should live as a formal decision package, not just a footnote.

## Scope

In scope:

1. Evaluate candidate integrity-profile directions beyond the v0.2 baseline.
2. Clarify whether they should be normative, optional, deferred, or out of scope.
3. Record the decision and rationale in the architecture/governance layer.

Out of scope:

- shipping a full second integrity profile without prior decision closure

## Deliverables

- Integrity-profile decision package and recommendation.
- Follow-on implementation requirements if a profile is adopted.

## Dependencies

- Existing v0.2 signature profile and decision history.

## Acceptance Criteria

- [ ] Additional integrity-profile options are evaluated explicitly.
- [ ] The repo has a clear decision on defer/adopt/reject.
- [ ] The outcome is recorded in canonical docs.
