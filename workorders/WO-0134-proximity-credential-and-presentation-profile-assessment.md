# WO-0134 — Proximity Credential and Presentation Profile Assessment

**Status:** COMPLETED  
**Created:** 2026-03-06  
**Updated:** 2026-03-06  
**Priority:** P1  
**Owner:** Research-First Identity and Runtime  
**Source:** `docs/reports/2026-03-06-protocol-volatility-proximity-and-federation-research-first-decision-package.md`

## Objective

Define what belongs in Universal Manifest versus what belongs in external presentation protocols for proximity-triggered credential exchange.

## Problem Statement

UM has consent, pointer, and runtime concepts that are relevant to proximity-based proof exchange, but it currently lacks an implementation-safe boundary profile covering same-device, cross-device, and device-to-device presentation patterns.

## Scope

In scope:

- Compare proximity-triggered presentation models at the boundary level.
- Define what UM can safely carry for a proximity flow: policy pointers, consent scope, freshness expectations, and proof-result references.
- Produce a promotion recommendation for future integration guidance, if justified.

Out of scope:

- Selecting one mandatory proximity transport.
- Adding proximity semantics to the UM core schema.
- Implementing fixtures or journeys before the boundary profile is accepted.

## Deliverables

- A new report under `docs/reports/`
- Follow-on implementation work orders only if the boundary profile is promotion-ready

## Acceptance Criteria

- [x] The report clearly separates UM document semantics from live presentation transport semantics.
- [x] Same-device and cross-device flows are both addressed.
- [x] Privacy and anti-correlation risks are documented.
- [x] The result explicitly states whether a UM integration lane should be created, deferred, or limited to examples.

## Dependencies

- `docs/workorders/WO-0132-research-first-protocol-volatility-proximity-and-federation-gaps.md`

## Execution Notes

- Completed on 2026-03-06.
- Delivered report: `docs/reports/2026-03-06-proximity-credential-and-presentation-profile-assessment.md`
- Outcome:
  - UM core schema change is not justified.
  - Public proximity integration guidance should remain deferred.
  - Limited internal examples are acceptable, but promotion to a public integration lane still requires executable same-device and cross-device proof.
- Follow-on implementation work orders were not created in this work order because the repo's existing promotion gate is not yet met.
