# Spec Improvement Queue

**Version**: 1.0  
**Effective Date**: 2026-03-02  
**Status**: Active

## Purpose

This queue tracks specification changes that originate from adopter feedback. It ensures every accepted ambiguity report or feature request has a traceable path from issue intake to spec and fixture updates.

## Intake Sources

Queue candidates come from adopter issues labeled:

- `spec-ambiguity`
- `feature-request`
- `implementation-bug` (only when normative spec change is required)

All candidate issues must also include `adopter-feedback`.

## Routing Workflow

1. Adopter submits issue through a structured issue template.
2. Maintainer triages and labels (`adopter-feedback` + type + priority + status).
3. Maintainer decides whether a normative spec change is required.
4. If yes, create an RFC using [RFC-TEMPLATE.md](./RFC-TEMPLATE.md).
5. RFC review must include backward-compatibility impact.
6. If approved, implement:
   - spec text changes
   - schema/context changes (if applicable)
   - conformance fixture updates
   - suite version bump per [REGRESSION-PREVENTION.md](./REGRESSION-PREVENTION.md)
7. Notify affected adopters and close linked queue item.

## Queue Status Model

- `INTAKE`: triaged issue pending spec-change decision
- `RFC_REQUIRED`: spec change approved for RFC drafting
- `RFC_OPEN`: RFC issue open and under review
- `APPROVED`: RFC approved, implementation scheduled
- `IMPLEMENTING`: code/spec/fixture updates in progress
- `RELEASED`: change merged and released
- `NOTIFIED`: affected adopters notified
- `CLOSED_NO_CHANGE`: no normative change needed

## Active Queue

No active entries yet.

When entries exist, record each item using this format:

```markdown
- Queue ID: SIQ-0001
  - Source Issue: #1234
  - Type: spec-ambiguity | feature-request | implementation-bug
  - Priority: p0-blocker | p1-high | p2-medium | p3-low
  - Status: INTAKE
  - Owner: @maintainer
  - RFC: #5678 (if applicable)
  - Impacted Spec Versions: v0.1 | v0.2
  - Impacted Conformance Levels: v0.1-baseline, v0.2-baseline
  - Target Release: TBD
  - Last Updated: YYYY-MM-DD
```

## Queue Governance Rules

- Every item must link back to its source issue.
- Every approved normative change must have an RFC.
- Every released change must reference fixture updates and suite versioning rationale.
- Every adopter-impacting release must include notification evidence.

## Related Documents

- [Governance](./GOVERNANCE.md)
- [Adopter Feedback SLA](./ADOPTER-SLA.md)
- [Regression Prevention](./REGRESSION-PREVENTION.md)
