# WO-0002 — Signature profiles (v0.2) + Data Integrity path

**Status:** COMPLETED  
**Created:** 2026-02-12

## Objective

Define an interoperable signature profile for Universal Manifest (v0.2), while keeping a clear path to add **Data Integrity** later without breaking adopters.

## Why this matters

Signatures are the largest remaining “interop hardening” gap:

- without a shared canonicalization + verification checklist, implementations will diverge

## Scope

In scope:

- Choose a baseline v0.2 verification profile (recommendation currently: JCS (RFC 8785) + Ed25519)
- Explicitly document how other profiles (e.g., Data Integrity / URDNA2015) can be added later
- Add v0.2 schema/context and update the TS helper types accordingly
- Add conformance fixtures for signature verification once the profile is locked

Out of scope:

- Implementing DID resolution libraries or a full cryptography toolkit

## Acceptance criteria

- [x] v0.2 profile decision recorded in `docs/DECISIONS.md`
- [x] `spec/v0.2/schema.jsonld` + `spec/v0.2/schema.json` added
- [x] `packages/universal-manifest` updated to represent v0.2 signature fields
- [x] Conformance fixtures exist for “valid signature” and “invalid signature” (post-decision)

## References

- `spec/v0.2/SIGNATURE-PROFILE.md`
- `docs/PUBLISHING-AND-VERSIONING.md`
