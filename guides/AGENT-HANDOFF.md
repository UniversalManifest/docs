---
work_order: WO-0055
agent_task_id: e0a7fe60_1772165606
spec_versions_covered:
  - "0.1"
  - "0.2"
updated: "2026-03-02"
conformance_suite_version: "0.1.0"
---

# Universal Manifest Agent Handoff

This document is the condensed transfer package for agents implementing UM consumers/issuers.

## 1) Normative Boundary (Do Not Drift)

- UM is the specification; implementations are replaceable.
- Normative sources:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/CONFORMANCE.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md`
- TypeScript references are informative examples:
  - `https://github.com/grigb/um-typescript`

## 2) Conformance Level Decision

Text fallback decision tree:

1. Consume only -> `v0.1-baseline` consumer.
2. Produce manifests -> add `v0.1-baseline` issuer requirements.
3. Need tamper protection -> `v0.2-baseline`.
4. Need revocation checks -> `v0.2-extended`.

## 3) Required Fields and Baseline Validation

Required fields for both versions:

- `@context`
- `@id`
- `@type` includes `um:Manifest`
- `manifestVersion`
- `subject`
- `issuedAt`
- `expiresAt`

Baseline rules:

1. Reject missing required fields.
2. Reject invalid timestamps.
3. Reject `issuedAt > expiresAt`.
4. Reject for use if `now > expiresAt`.
5. Ignore unknown fields safely.

## 4) v0.2 Signing and Verification Contract

Signing (issuer):

1. Remove `signature` from payload.
2. Canonicalize with JCS (RFC 8785).
3. Sign bytes with Ed25519.
4. Attach `signature` object with:
   - `algorithm: "Ed25519"`
   - `canonicalization: "JCS-RFC8785"`
   - `value` (base64url)
   - optional `created`, `keyRef`, `publicKeySpkiB64`, `statusRef`, `revocationCursor`

Verification (consumer):

1. Run baseline checks first.
2. Require profile pair (`Ed25519`, `JCS-RFC8785`).
3. Rebuild signing input (remove signature + JCS).
4. Resolve/read public key.
5. Verify signature; reject on any failure.

## 5) Conformance Suite Execution Path

Suite root:

- `/Users/grig/work/repo/universalmanifest/conformance`
- suite version: `0.1.0`

Runner path:

- `/Users/grig/work/repo/universalmanifest/conformance/runner`

Adapter response shape:

```json
{
  "result": "accept",
  "reason": "validated"
}
```

Expected report schema:

- `/Users/grig/work/repo/universalmanifest/conformance/schema/conformance-report.schema.json`

## 6) Implementation Plan Template (Agent Ready)

1. Implement parser + required-field validator.
2. Implement TTL and unknown-field tolerant consumer flow.
3. Implement issuer flow for `v0.1` manifests.
4. Add `v0.2` JCS + Ed25519 signing.
5. Add `v0.2` signature verification and profile checks.
6. Build adapter and run conformance runner.
7. Emit schema-valid conformance report and attach execution evidence.

## 7) Done Criteria

- Passes all expected fixtures for target versions.
- Produces machine-readable conformance report.
- Clearly documents that UM spec is normative and implementation code is informative.
- Includes reproducible commands for CI/local reruns.

## 8) Companion Docs

- Full guide: `/Users/grig/work/repo/universalmanifest/docs/guides/IMPLEMENTATION-GUIDE.md`
- Quick card: `/Users/grig/work/repo/universalmanifest/docs/guides/QUICK-REFERENCE.md`
- Site implementation guide: `https://universalmanifest.net/guides/implementation-guide/`
