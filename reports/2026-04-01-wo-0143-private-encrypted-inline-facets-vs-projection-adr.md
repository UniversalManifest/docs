# WO-0143 ADR: Private Data Handling Model (Projection + Encrypted Inline Facets)

Date: 2026-04-01
Status: Accepted
Work order: `docs/workorders/WO-0143-private-encrypted-inline-facets-vs-projection-model-analysis.md`

## Decision

Universal Manifest adopts a dual-path privacy model:

1. Projection remains a normative privacy path for broad interoperability and low operational overhead.
2. Encrypted inline facets are accepted as an optional guidance profile for cryptographic confidentiality at rest.

This is an additive model, not a replacement model. Implementations may use either path or both, based on threat model and operational maturity.

## Why

- Projection is proven and simple, but requires robust lifecycle handling when consumer needs change.
- Encrypted inline facets provide strong confidentiality but introduce key lifecycle complexity.
- A universal specification should not force a single privacy mechanism across all deployment environments.

## Architecture Paths

### Path A: Projection (Normative)

- Issuer mints consumer-specific derived manifests with only allowed facets/claims.
- Every projection is independently signed and independently TTL-bound.
- Projection requests are treated as runtime policy operations owned by the issuer or subject-controlled runtime.

Projection lifecycle requirements:

- Every projection MUST carry explicit `issuedAt` and `expiresAt`.
- Projection regeneration MUST be possible when consumer scope changes.
- Projection distribution and invalidation policy SHOULD be auditable.

### Path B: Encrypted Inline Facets (Optional Guidance Profile)

- Sensitive facets stay in-document but their payloads are encrypted.
- Manifest envelope (`@id`, `subject`, TTL, signature, non-sensitive metadata) remains readable.
- Consumers without keys can still verify signature integrity and process the manifest in partial-visibility mode.

Encrypted facet lifecycle requirements:

- key discovery: via recipient key references (`kid`/`keyRef`) and public key material.
- key rotation: re-encrypt protected facet payload for new recipient key version and re-sign manifest.
- access revocation: remove revoked recipient access, rotate key material, issue new signed manifest version.
- stale copy mitigation: short TTL plus resolver freshness policy.

## Signature and Verification Order

For encrypted inline facets, the recommended operational order is:

1. verify signature over the manifest as received,
2. then decrypt authorized facets.

This keeps manifest integrity verifiable even when consumers cannot decrypt every protected facet.

## Interoperability and Scope Boundaries

- v0.2 core remains encryption-agnostic and does not mandate one cryptosystem.
- Encrypted inline facets are guidance-level and forward-compatible.
- Existing consumers that do not understand encrypted facet payloads should preserve unknown structures and continue processing non-sensitive data.

## Consequences

Positive:

- Supports both low-friction and high-security deployments.
- Avoids premature lock-in to a single privacy mechanism.
- Preserves portability and backward compatibility.

Trade-offs:

- Implementers must choose and document a privacy operating model.
- Encrypted profiles require key lifecycle governance beyond baseline conformance.

## Deliverable Mapping (WO-0143)

- Architectural decision report: this file.
- Core guidance update: `spec/v0.2/README.md`, `spec/v0.2/CONFORMANCE.md`.
- Lifecycle fixtures: `examples/v0.2/encrypted-inline-facets/`.
