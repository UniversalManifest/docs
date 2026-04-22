# WO-0190 Additional Integrity Profile Decision Package

**Date:** 2026-04-22
**Work order:** WO-0190
**Decision:** Defer additional integrity-profile guidance beyond the v0.2 baseline

## Decision Summary

Universal Manifest should keep `spec/v0.2` centered on the existing interoperable baseline:

- canonicalization: `JCS (RFC 8785)`
- signature: `Ed25519`
- signature encoding: `base64url`

Additional integrity-profile work is not adopted now as either a normative or optional v0.2 requirement. The repo already treats Data Integrity as a future additive path, so the correct outcome here is to confirm that position rather than reopen the baseline.

## Options Evaluated

### 1. Data Integrity / RDF canonicalization

Decision: defer.

This is the strongest candidate for a future additive profile, but it is not required to preserve the current interoperability contract. It would introduce JSON-LD/RDF processing semantics, specialized canonicalization rules, and a larger conformance surface before the current v0.2 baseline is fully stabilized.

### 2. JOSE / JWS-style JSON envelope signing

Decision: reject as a baseline replacement.

This path does not materially improve the current contract and would split implementers away from the already-selected JCS + Ed25519 path. It is not the right direction for the current spec lineage.

### 3. Multi-proof attachment as a first-class profile strategy

Decision: optional only, and only after a second profile exists.

This is downstream of a separate adoption decision. It is not a reason to add a new profile now.

## Rationale

The v0.2 spec artifacts already define the current baseline clearly, and `docs/DECISIONS.md` already records the JCS + Ed25519 choice as the interoperability hardening step. The additional-integrity question is therefore a governance question about future extension, not a missing baseline decision.

Deferring additional profiles is the pragmatic choice because:

- the current baseline is already implementable and testable
- Data Integrity changes the signing model enough to deserve its own future profile package
- there is no current repo requirement that depends on a second integrity profile
- adding a second profile now would expand the conformance burden without solving an existing blocker

## Follow-On Requirements If A Future Profile Is Adopted

If the project later adopts Data Integrity or another additional integrity profile, the adoption package must include:

1. A dedicated profile spec with explicit signing and verification rules.
2. Conformance fixtures for valid, invalid, and unsupported-profile cases.
3. Consumer and issuer profile-selection guidance.
4. Migration notes showing coexistence with the v0.2 baseline.
5. A governance update recording the new decision.

## Closure Note

WO-0190 is closable because there are no remaining blockers. The current baseline remains authoritative, and the extension path is already documented as future additive work.
