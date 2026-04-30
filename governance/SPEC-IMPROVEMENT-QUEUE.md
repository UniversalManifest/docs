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

## Phase 19 Planning Queue

Phase 19 uses the published v0.2 surface as the baseline for adopter feedback and v0.3 input triage. These entries are planning stubs, not active adopter-submitted queue items, because they originate from the 2026-04-24 publication-readiness scan rather than from external issues.

Use the normal queue model above when an adopter issue, RFC, or accepted implementation report turns one of these stubs into a concrete spec-change candidate.

- `WO-0243` — Post-publication external-human reader validation activation: promotes `WO-0214` after publication and captures comprehension evidence against the published Home cluster and v0.2 spec.
- `WO-0244` — Adopter-feedback loop activation against published v0.2: reactivates the `WO-0056` feedback/SLA/spec-improvement path for real post-publication reports.
- `WO-0245` — Tier 2 cryptographic identity-binding research package: evaluates promotion criteria for v0.3+ cryptographic binding.
- `WO-0246` — Tier 3 multi-party ceremony research package: defines evidence requirements before ceremony support can become a spec candidate.
- `WO-0247` — Data Integrity / RDF profile decision package: follows the future path described in `spec/v0.2/SIGNATURE-PROFILE.md` section 8.
- `WO-0248` — Additional integrity-profile registry decision package: covers integrity profiles beyond the v0.2 JCS + Ed25519 baseline.
- `WO-0249` — Revocation-as-normative decision package: determines whether revocation/status metadata remains optional or becomes conformance-bound.
- `WO-0250` — Encrypted inline facet promotion decision: decides whether guidance-only encrypted facets need normative lifecycle and fixture coverage.
- `WO-0251` — Broader cross-DID binding tier scope decision: evaluates cross-DID binding expansion beyond the v0.2 Tier 1 baseline.

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
