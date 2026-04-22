# WO-0191 -- Revocation Cursor and Status Contract

**Status:** COMPLETED
**Priority:** P1
**Created:** 2026-04-13

## Objective

Define whether revocation cursors, status references, and related status signaling become normative parts of the Universal Manifest contract.

## Context

The current state explicitly calls out revocation cursor/events as not finalized as a normative part of the contract. That is too important to remain as an untracked design gap.

## Scope

In scope:

1. Define the revocation/status problem precisely.
2. Decide the normative versus optional contract boundary.
3. Specify the schema, behavior, and interoperability consequences if adopted.

Out of scope:

- implementing a full revocation network without first defining the contract

## Deliverables

- Revocation/status contract proposal and decision package.
- Schema and conformance implications if adopted.

## Dependencies

- v0.2 draft work and security/threat-model decisions.

## Acceptance Criteria

- [x] The revocation/status problem is formally specified.
- [x] The repo has a clear normative-boundary decision.
- [x] Any resulting schema/conformance deltas are identified.

## Completion Notes

- The decision package is recorded in `docs/reports/2026-04-22-revocation-cursor-and-status-contract.md`.
- The base v0.2 contract keeps revocation/status metadata optional and non-normative for ordinary verifiers.
- Revocation-aware verification remains an opt-in conformance lane with explicit status resolution and cursor freshness rules.
