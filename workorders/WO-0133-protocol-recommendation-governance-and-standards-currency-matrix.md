# WO-0133 — Protocol Recommendation Governance and Standards Currency Matrix

**Status:** COMPLETED  
**Created:** 2026-03-06  
**Updated:** 2026-03-06  
**Priority:** P1  
**Owner:** Research Governance  
**Source:** `docs/reports/2026-03-06-protocol-volatility-proximity-and-federation-research-first-decision-package.md`

## Objective

Create a repeatable governance mechanism for deciding when named protocol families in UM documentation can move from `example only` to `recommended guidance`.

## Problem Statement

UM now correctly warns against lock-in in volatile identity and credential ecosystems, but it still lacks a maintained standards-currency review artifact and promotion rule set. Without that, named examples in integration lanes can drift into accidental recommendations.

## Scope

In scope:

- Create a standards-currency matrix covering the protocol families most likely to appear in UM integration lanes.
- Define promotion and demotion criteria for named protocol examples.
- Identify where current docs should point to the currency matrix instead of embedding unstable judgments.

Out of scope:

- Normative spec changes.
- Selecting one mandatory DID, VC, or proof stack.
- Runtime or fixture implementation changes.

## Deliverables

- A new report under `docs/reports/`
- Governance synchronization if documentation policy changes are adopted

## Acceptance Criteria

- [x] A dated currency matrix exists for volatile protocol families referenced by UM docs.
- [x] Promotion criteria from `example only` to `recommended guidance` are explicit.
- [x] Demotion criteria are explicit when upstream status or ecosystem support weakens.
- [x] No core UM document is made protocol-specific by this work alone.

## Dependencies

- `docs/workorders/WO-0132-research-first-protocol-volatility-proximity-and-federation-gaps.md`

## Execution Progress (2026-03-06)

Completed in this pass:

- Created the dated currency matrix and governance report:
  - `docs/reports/2026-03-06-protocol-recommendation-governance-and-standards-currency-matrix.md`
- Defined recommendation tiers, promotion rules, demotion rules, and review cadence for volatile protocol families.
- Updated standards-positioning surfaces to point to the matrix as the maintenance anchor for time-sensitive protocol-family status language:
  - `docs/STANDARDS-POSITIONING.md`
  - `site/src/content/docs/about/standards-positioning.md`

## Completion notes

- WO-0133 creates governance discipline, not a new protocol recommendation shortlist.
- The next unresolved work in sequence remains WO-0134 (proximity credential and presentation profile assessment).
