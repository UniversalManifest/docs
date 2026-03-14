# WO-0132 — Research-First Protocol Volatility, Proximity, and Federation Gaps

**Status:** COMPLETED  
**Created:** 2026-03-06  
**Updated:** 2026-03-06  
**Priority:** P1  
**Owner:** Research-First Program  
**Source:** `.dev/ai/knowledge-corpus/imports/external-25-user-centric-pointer-protocols-2025-landscape.md`, `.dev/ai/knowledge-corpus/imports/external-26-universal-manifest-architectures-comprehensive-analysis.md`, `.dev/ai/knowledge-corpus/imports/external-27-peermesh-universal-manifest-vision.md`

## Objective

Convert the unresolved gaps surfaced by the newly localized source corpus into an explicit Research-First decision package with promotion gates before any broader implementation claims are made.

## Problem Statement

The new corpus reinforces several still-open topics that should not be resolved by casual documentation edits alone: protocol and vendor volatility in DID/VC-adjacent ecosystems, proximity-aware credential patterns, and multi-protocol bridge/federation strategy for closed and open surfaces. These topics need a bounded Research-First work order instead of implicit drift into integration docs.

## Scope

In scope:

- Produce a Research-First report that classifies each unresolved topic as `covered`, `partial`, or `gap`.
- Define promotion gates for proximity credentials, federation bridge strategy, and volatile protocol recommendations.
- Record which localized sources produce no additional execution work beyond provenance.

Out of scope:

- Implementing runtime or fixture changes.
- Creating normative spec requirements.
- Reopening already completed Go-Now work without new evidence.

## Deliverables

- A new Research-First report under `docs/reports/`
- Governance/status synchronization if new follow-on work orders are required

## Acceptance Criteria

- [x] Every unresolved topic has a documented promotion gate.
- [x] Protocol volatility is treated as a research decision, not an implied recommendation.
- [x] Sources with no further required action are explicitly recorded as such.

## Dependencies

- `docs/workorders/WO-0130-composite-architecture-and-active-runtime-alignment.md`
- `docs/workorders/WO-0131-did-vc-and-metaverse-lane-refresh-from-localized-corpus.md`

## Execution Progress (2026-03-06)

Completed in this pass:

- Created the Research-First decision package:
  - `docs/reports/2026-03-06-protocol-volatility-proximity-and-federation-research-first-decision-package.md`
- Verified current official standards checkpoints for time-volatile protocol families before finalizing the decision package.
- Registered explicit follow-on work orders so unresolved topics remain actionable instead of implicit:
  - `docs/workorders/WO-0133-protocol-recommendation-governance-and-standards-currency-matrix.md`
  - `docs/workorders/WO-0134-proximity-credential-and-presentation-profile-assessment.md`
  - `docs/workorders/WO-0135-federation-and-bridge-strategy-decision-package.md`

## Completion notes

- WO-0132 concluded that no core UM schema change is justified at this stage.
- The correct next path is targeted research and promotion gating, not broader protocol-specific integration claims.
