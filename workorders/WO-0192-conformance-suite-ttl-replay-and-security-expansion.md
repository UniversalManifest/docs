# WO-0192 -- Conformance Suite TTL, Replay, and Security Expansion

**Status:** COMPLETED
**Priority:** P1
**Created:** 2026-04-13

## Objective

Expand the conformance suite to cover the broader TTL, replay, and security cases that are still identified as incomplete.

## Context

The current state says the project has baseline valid/invalid fixtures plus non-normative GPC proof coverage, but broader TTL/replay/security cases remain. That gap should be tracked as a concrete suite-expansion work order.

## Scope

In scope:

1. Identify missing TTL/replay/security conformance coverage.
2. Add fixtures and expected-behavior coverage for those cases.
3. Update conformance docs and validation packaging accordingly.

Out of scope:

- unrelated UI or site work

## Deliverables

- Expanded fixture corpus for TTL/replay/security cases.
- Updated conformance documentation and execution coverage.

## Dependencies

- Outputs of WO-0190 and WO-0191 where integrity-profile and revocation/status decisions affect expected conformance behavior.
- Existing `examples/`, `spec/`, and `conformance/` baselines.

## Acceptance Criteria

- [x] Missing TTL/replay/security gaps are explicitly covered.
- [x] New fixtures and expected behaviors are documented.
- [x] Conformance coverage is materially broader than the current baseline.

## Completion Notes

- Added explicit v0.2 invalid fixtures for expired-for-use replay/freshness rejection and malformed `issuedAt`/`expiresAt` timestamps.
- Updated `spec/v0.2/CONFORMANCE.md` and `conformance/v0.2/expected.json` to name the new cases.
- Kept the slice bounded to validator-capable TTL/security checks and avoided new revocation transport machinery.
