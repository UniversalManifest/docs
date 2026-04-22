# 2026-04-22 Conformance Suite TTL, Replay, and Security Expansion

## Purpose

This report closes `WO-0192` by capturing a bounded conformance expansion that fills the missing TTL, replay, and security gaps in the current v0.2 validator-capable suite.

## Scope of the slice

The slice stayed inside the existing verifier/conformance surface:

- no new networked revocation machinery
- no schema-breaking changes
- no shared queue/status file changes

Instead, it targeted the missing negative fixtures that exercise the already-implemented freshness and signature checks.

## Changes made

### New fixtures

Added to `examples/v0.2/invalid/`:

- `expired-for-use.jsonld`
- `invalid-issuedAt-format.jsonld`
- `invalid-expiresAt-format.jsonld`

### Conformance matrix

Updated `conformance/v0.2/expected.json` to include the new invalid expectations and categorize them as baseline TTL/security coverage.

### Spec documentation

Updated `spec/v0.2/CONFORMANCE.md` to explicitly call out:

- expired manifests as invalid replay/freshness cases
- malformed `issuedAt` and `expiresAt` timestamps as required rejection cases

### Work order

Updated `docs/workorders/WO-0192-conformance-suite-ttl-replay-and-security-expansion.md` to `COMPLETED`.

## Verification

Focused verification for this slice:

- `npm --prefix /Users/grig/work/repo/universalmanifest/packages/universal-manifest run validate:examples`
  - Result: the three newly added v0.2 invalid fixtures were rejected as expected:
    - `examples/v0.2/invalid/expired-for-use.jsonld`
    - `examples/v0.2/invalid/invalid-issuedAt-format.jsonld`
    - `examples/v0.2/invalid/invalid-expiresAt-format.jsonld`
  - Note: the broader example-validation run still reports pre-existing unrelated failures in older fixture lanes; those were not introduced by this slice.
- `npm --prefix /Users/grig/work/repo/universalmanifest/site run build`
  - Result: passed
  - The build also generated the published harness/sandbox mirrors for the new invalid fixtures and updated the public fixture catalog counts accordingly.

## Outcome

`WO-0192` is now complete.

The missing TTL/replay/security gaps now have explicit v0.2 fixture coverage and expected outcomes, the published fixture mirrors include the new invalid cases, and the change stays within the current conformance capability.
