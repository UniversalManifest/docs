# WO-0190 -- Additional Integrity Profile Decision Package

**Status:** COMPLETED
**Priority:** P2
**Created:** 2026-04-13
**Closed:** 2026-04-22

## Objective

Decide whether and when Universal Manifest should add integrity-profile guidance beyond the current v0.2 JCS + Ed25519 baseline.

## Context

The current state explicitly lists additional integrity profiles such as Data Integrity / RDF canonicalization as not yet finalized. That question should live as a formal decision package, not just a footnote.

## Scope

In scope:

1. Evaluate candidate integrity-profile directions beyond the v0.2 baseline.
2. Clarify whether they should be normative, optional, deferred, or out of scope.
3. Record the decision and rationale in the architecture/governance layer.

Out of scope:

- shipping a full second integrity profile without prior decision closure

## Deliverables

- Integrity-profile decision package and recommendation.
- Follow-on implementation requirements if a profile is adopted.

## Dependencies

- Existing v0.2 signature profile and decision history.

## Acceptance Criteria

- [x] Additional integrity-profile options are evaluated explicitly.
- [x] The repo has a clear decision on defer/adopt/reject.
- [x] The outcome is recorded in canonical docs.

## Decision

Defer any additional integrity-profile guidance beyond the current v0.2 baseline.

The current baseline remains:

- canonicalization: `JCS (RFC 8785)`
- signature: `Ed25519`
- signature encoding: `base64url`

Additional profiles are not adopted now as normative or optional v0.2 requirements. They remain future additive work if a separate use case justifies them.

## Evaluated Directions

### Data Integrity / RDF canonicalization

Decision: defer.

Reason: it is a valid future additive profile, but it is not needed to preserve the current interoperability contract, and it would expand the conformance surface into JSON-LD/RDF semantics before the current baseline is fully matured.

### JOSE / JWS-style JSON envelope signing

Decision: reject as a replacement for the current baseline.

Reason: it does not improve the current contract enough to justify a profile switch, and it would split the ecosystem away from the already-selected JCS + Ed25519 path.

### Multiple simultaneous proof attachments

Decision: optional future extension only.

Reason: this is useful only after there is a second profile to carry, so it is downstream of a separate adoption decision rather than part of this closure.

## Rationale

The repo already records the baseline choice in `docs/DECISIONS.md` and the v0.2 spec artifacts already treat Data Integrity as a future path, not a current requirement. That means the honest decision here is not to reopen the baseline, but to confirm the current direction and keep the extension space additive.

The practical reasons for deferral are:

- the current v0.2 contract is already implementable and testable with JCS + Ed25519
- Data Integrity introduces a materially different processing model and would need its own canonicalization and verifier rules
- there is no present repo-level acceptance need that requires a second normative integrity profile
- forcing a second profile now would increase divergence risk without improving current interoperability

## Follow-On Requirements

No implementation work is required for this closure.

If a future work order chooses to adopt Data Integrity or another additional profile, it must include:

1. A separate profile document with explicit canonicalization and verification rules.
2. Conformance fixtures for valid, invalid, and profile-mismatch cases.
3. Consumer and issuer compatibility guidance for profile selection and rejection behavior.
4. Migration notes explaining how the new profile coexists with the v0.2 baseline.
5. Updated decision history in the governance layer.

## Blockers

None for this work order. The baseline and the future-path language are already present in the existing spec and decision records.
