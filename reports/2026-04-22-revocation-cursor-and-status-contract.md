# 2026-04-22 Revocation Cursor and Status Contract

## Purpose

This report closes `WO-0191` by defining the revocation/status problem, drawing the normative boundary, and capturing the schema and conformance implications if the project later adopts the revocation lane as a broader contract surface.

## Problem Statement

The contract has two distinct security questions that should not be conflated:

1. **Authenticity and integrity**: is this manifest structurally valid and signed by the expected key?
2. **Freshness and invalidation**: has the issuer later revoked or superseded the manifest, and can a consumer determine that status in time?

`signature.statusRef` and `signature.revocationCursor` solve the second question, not the first. They are out-of-band freshness metadata that support revocation-aware policy, cache revalidation, and stale-status detection. They do not change the signed bytes, and they do not replace signature verification.

The operational failure mode is straightforward:

- a manifest can be correctly signed and still be unsafe to use because it has been revoked
- a consumer can verify the signature correctly but still accept stale status if it does not track revocation freshness
- an offline consumer can authenticate the manifest but cannot honestly claim revocation-aware status

## Decision

The base v0.2 contract keeps revocation/status signaling **optional and non-normative**.

The normative boundary is:

- **Normative for all v0.2 consumers**: validate required fields, enforce TTL, verify the Ed25519/JCS signature profile, and ignore unknown fields safely.
- **Normative only for revocation-aware consumers**: if `signature.statusRef` is present, resolve revocation status; if `signature.revocationCursor` is present, use it to detect stale cached status; fail closed when policy requires active status and status cannot be determined.
- **Optional for ordinary consumers**: revocation metadata may be absent, and the manifest remains valid for signature-based verification as long as the core profile checks pass.

This is the right boundary for v0.2 because it preserves adoption-friendly interoperability while still making a revocation-aware posture explicit for higher-security deployments.

## Contract Meaning

The resulting contract reads as follows:

- `signature.algorithm` and `signature.canonicalization` identify the baseline integrity profile.
- `signature.statusRef` is a pointer to revocation/status material when an issuer elects to publish it.
- `signature.revocationCursor` is a monotonic freshness token that lets consumers detect when cached status is stale.
- Neither field participates in canonicalization or signature input.
- Consumers that do not implement revocation-aware verification MUST report revocation status as `unchecked` rather than implying a stronger guarantee.

## Schema Implications If Adopted

The current schema already requires `signature` and constrains the base signature profile, but it does not yet declare the revocation metadata fields. If the project formally adopts the revocation lane as part of the published contract, `spec/v0.2/schema.json` would need to add optional `signature.statusRef` and `signature.revocationCursor` properties under `signatureV02`.

That schema change would be additive only:

- no new required top-level fields
- no change to the signing input
- no change to the canonicalization rule
- no change to `manifestVersion: "0.2"`

The schema should still keep the fields optional, because revocation awareness is a policy capability, not a universal baseline requirement.

## Conformance Implications If Adopted

If adopted as a broader contract surface, `spec/v0.2/CONFORMANCE.md` would need to make the revocation lane explicit in three places:

1. Consumer conformance:
   - continue to require signature verification and TTL enforcement for all consumers
   - add a separate revocation-aware consumer mode that must evaluate `statusRef` and `revocationCursor` when present
   - preserve the `unchecked` reporting requirement for consumers that do not implement the revocation lane
2. Issuer conformance:
   - make `statusRef` publication and cursor rotation a SHOULD when relying parties require revocation-aware verification
   - keep revocation metadata optional for issuers that do not support the lane
3. Fixture coverage:
   - keep the positive fixture with revocation metadata
   - add or preserve negative cases for stale cursor handling, revoked status, and unavailable status where revocation-aware verification is claimed

In short: adoption expands conformance language, but it does not turn revocation metadata into a universal requirement for all manifests.

## Outcome

`WO-0191` is closed on the docs side.

The project now has a clear answer:

- revocation/status is part of the published v0.2 contract as an optional extension lane
- the universal baseline remains signature + TTL verification
- status resolution and cursor monotonicity are only normative when a consumer claims revocation-aware conformance
- schema and conformance updates, if/when applied, are additive and backward-compatible
