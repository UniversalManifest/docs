# WO-0134 — Proximity Credential and Presentation Profile Assessment

**Status:** NOT_STARTED  
**Created:** 2026-03-06  
**Updated:** 2026-03-06  
**Priority:** P1  
**Owner:** Research-First Identity and Runtime  
**Source:** `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-protocol-volatility-proximity-and-federation-research-first-decision-package.md`

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

- A new report under `/Users/grig/work/repo/universalmanifest/docs/reports/`
- Follow-on implementation work orders only if the boundary profile is promotion-ready

## Acceptance Criteria

- [ ] The report clearly separates UM document semantics from live presentation transport semantics.
- [ ] Same-device and cross-device flows are both addressed.
- [ ] Privacy and anti-correlation risks are documented.
- [ ] The result explicitly states whether a UM integration lane should be created, deferred, or limited to examples.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0132-research-first-protocol-volatility-proximity-and-federation-gaps.md`
