# Universal Manifest Quick Reference

Use this as a one-page implementation card.

UM is a specification. The TypeScript helper/reference repo is an example implementation path, not a normative dependency.

## Required Fields (v0.1 and v0.2)

| Field | Presence | Type | Notes |
| --- | --- | --- | --- |
| `@context` | Required | string | Context URL for target spec version |
| `@id` | Required | string (URI) | Recommended `urn:uuid:<uuidv4>` |
| `@type` | Required | string or array | Must include `um:Manifest` |
| `manifestVersion` | Required | string | `"0.1"` or `"0.2"` |
| `subject` | Required | string (URI) | Stable subject identifier |
| `issuedAt` | Required | string | RFC 3339 / ISO 8601 timestamp |
| `expiresAt` | Required | string | RFC 3339 / ISO 8601 timestamp |
| `signature` | Required for v0.2 | object | v0.2 profile: Ed25519 + JCS |

## Validation Rules Summary

1. Parse as JSON object.
2. Ensure all required fields exist and are non-empty.
3. Ensure `@type` includes `um:Manifest`.
4. Parse `issuedAt` and `expiresAt` timestamps.
5. Enforce `issuedAt <= expiresAt`.
6. Reject for use if `now > expiresAt`.
7. Ignore unknown fields safely.

## Signature Verification (v0.2) in 5 Steps

1. Confirm profile: `signature.algorithm == "Ed25519"` and `signature.canonicalization == "JCS-RFC8785"`.
2. Remove `signature` from the manifest payload.
3. Canonicalize remaining JSON bytes with JCS (RFC 8785).
4. Obtain verification key from `signature.publicKeySpkiB64` or `signature.keyRef`.
5. Verify Ed25519 signature; reject if verification fails.

## Conformance Levels at a Glance

- `v0.1-baseline`: required fields + TTL + unknown-field tolerance.
- `v0.2-baseline`: v0.1-baseline + signature profile verification/signing.
- `v0.2-extended`: v0.2-baseline + revocation-aware verification policy.

Decision tree text fallback:

1. Consume only -> `v0.1-baseline` consumer.
2. Produce manifests -> include `v0.1-baseline` issuer behavior.
3. Need tamper protection -> `v0.2-baseline`.
4. Need revocation checks -> `v0.2-extended`.

## Key URLs

- Spec v0.1: `https://universalmanifest.net/spec/v01/`
- Spec v0.2: `https://universalmanifest.net/spec/v02/`
- Conformance v0.1: `https://universalmanifest.net/conformance/v01/`
- Conformance v0.2: `https://universalmanifest.net/conformance/v02/`
- Standalone suite guide: `https://universalmanifest.net/conformance/standalone-suite/`
- Reference implementation (TypeScript): `https://github.com/grigb/um-typescript`
- This implementation guide: `/Users/grig/work/repo/universalmanifest/docs/guides/IMPLEMENTATION-GUIDE.md`
- Agent handoff companion: `/Users/grig/work/repo/universalmanifest/docs/guides/AGENT-HANDOFF.md`
