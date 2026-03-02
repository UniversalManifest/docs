# Adopter Feedback SLA

**Version**: 1.0  
**Effective Date**: 2026-03-02  
**Status**: Active

## Purpose

This document defines response and resolution commitments for adopter feedback submitted through the Universal Manifest issue templates.

The goal is predictable support for implementers without introducing private support channels or paid support tiers.

## Scope

This SLA applies to public GitHub issues filed with these labels:

- `conformance-question`
- `spec-ambiguity`
- `implementation-bug`
- `feature-request`

All adopter issues must also include `adopter-feedback` and start in `triage`.

## Response Commitments

### Conformance Questions

- Initial acknowledgment: within 48 hours
- Substantive answer: within 1 week
- Required outcome: clarifying guidance and/or link to normative source text

### Spec Ambiguity Reports

- Initial acknowledgment: within 48 hours
- Resolution decision: within 2 weeks
- Required outcome: one of:
  - clarification accepted (with next action)
  - clarification deferred (with rationale)
  - `wontfix` (with rationale)

### Implementation Bug Reports

- Initial acknowledgment: within 24 hours
- Fix or documented workaround: within 1 week
- Required outcome: issue linked to patch, workaround, or tracked follow-up

### Feature Requests

- Initial acknowledgment: within 1 week
- Disposition decision: within 1 month
- Required outcome: accepted, deferred, or rejected with rationale

## Label Contract

Issue type labels:

- `adopter-feedback`
- `conformance-question`
- `spec-ambiguity`
- `implementation-bug`
- `feature-request`

Priority labels:

- `p0-blocker`
- `p1-high`
- `p2-medium`
- `p3-low`

Status labels:

- `triage`
- `acknowledged`
- `in-progress`
- `resolved`
- `wontfix`

## Triage Workflow

1. Intake
   - Maintainer confirms issue template completeness.
   - Missing critical details are requested immediately.
2. Classification
   - Maintainer applies one type label, one priority label, and `acknowledged`.
3. Resolution Path
   - `conformance-question`: maintainer answer and docs/spec pointer.
   - `spec-ambiguity`: route into [SPEC-IMPROVEMENT-QUEUE.md](./SPEC-IMPROVEMENT-QUEUE.md) when spec text change is needed.
   - `implementation-bug`: create implementation task and link fix/workaround.
   - `feature-request`: evaluate fit, conformance impact, and RFC need.
4. Closure
   - Mark `resolved` only when the output is visible and linked.
   - Use `wontfix` only with explicit rationale.

## Escalation

Escalate to maintainers immediately when:

- A `p0-blocker` issue risks blocking a release or conformance claim.
- An issue misses its SLA target by more than 48 hours.
- A spec ambiguity requires a normative decision by the Technical Steering Committee.

## Operating Notes

- SLA clocks begin at issue creation time.
- If maintainer action is blocked waiting for reporter information, status may remain `acknowledged` until required details are provided.
- This SLA is a governance commitment for open-source operations, not a contractual service guarantee.

## Related Documents

- [Governance](./GOVERNANCE.md)
- [Spec Improvement Queue](./SPEC-IMPROVEMENT-QUEUE.md)
- [Regression Prevention](./REGRESSION-PREVENTION.md)
- [RFC Template](./RFC-TEMPLATE.md)
