# WO-0058 — v0.1-to-v0.2 Migration Guide

**Status:** COMPLETED
**Created:** 2026-02-27
**Priority:** HIGH
**Blocks:** Gate G6 (Governance and change control — migration policy required)
**Dependencies:** WO-0053 (Conformance Test Suite — needed for migration verification), WO-0057 (Spec-vs-Implementation Clarity — messaging must be correct)
**Estimated effort:** 1 week

## Objective

Document the complete migration path from v0.1 consumer/issuer to v0.2 signed manifests. This includes code examples, breaking changes, compatibility considerations, and a verification checklist. Required by Gate G6 (deprecation and migration policy).

## Why this work matters

v0.2 introduces mandatory cryptographic signatures (JCS + Ed25519), which is a significant change from v0.1's permissive signature placeholder. Existing v0.1 adopters need a clear, actionable migration path. Without this:

1. Adopters cannot plan their upgrade timeline.
2. Breaking changes are discovered at runtime instead of during planning.
3. Gate G6 (governance and change control) cannot be satisfied — it explicitly requires a deprecation and migration policy.
4. The project appears unserious about backward compatibility.

## Scope

In scope:

- Comprehensive migration guide document.
- Breaking changes catalog with impact assessment.
- Compatibility matrix (what v0.1 consumers do with v0.2 manifests and vice versa).
- Code examples for common migration scenarios in multiple languages.
- Migration verification checklist.
- Deprecation timeline and support policy for v0.1.

Out of scope:

- Automated migration tooling (can be a future WO).
- Changing v0.1 or v0.2 spec semantics.
- Migrating internal tooling (that is part of WO-0054).

## Execution phases

### Phase 1 — Breaking changes catalog

- [x] Document all differences between v0.1 and v0.2:
  - **Breaking**: `signature` field goes from optional/permissive to required/profiled.
  - **Breaking**: `manifestVersion` changes from `"0.1"` to `"0.2"`.
  - **Breaking**: v0.2 consumers MUST verify signatures (cannot just ignore them).
  - **Non-breaking**: All v0.1 required fields remain required in v0.2.
  - **Non-breaking**: Unknown-field tolerance is preserved.
  - **Non-breaking**: TTL enforcement rules are unchanged.
  - **Additive**: `signature.algorithm`, `signature.canonicalization`, `signature.publicKeySpkiB64`, `signature.keyRef`, `signature.created` are new required signature fields.
  - **Additive**: Revocation metadata (`signature.statusRef`, `signature.revocationCursor`) are optional extensions.
- [x] Classify each change as: breaking-consumer, breaking-issuer, additive, unchanged.
- [x] Assess impact: what breaks if an adopter does nothing.

### Phase 2 — Compatibility matrix

- [x] Create a compatibility matrix table:

  | Scenario | Behavior | Action Required |
  |---|---|---|
  | v0.1 consumer receives v0.2 manifest | Consumer sees unknown `signature` fields, ignores them per unknown-field rule. Manifest is structurally valid but unverified. | Upgrade to v0.2 consumer for security. |
  | v0.2 consumer receives v0.1 manifest | Consumer rejects: missing required signature. | Issue v0.2 manifests or configure consumer for dual-version support. |
  | v0.1 issuer sends to v0.2 consumer | Rejected: no valid signature. | Upgrade issuer to v0.2 signing. |
  | v0.2 issuer sends to v0.1 consumer | Accepted: v0.1 consumer ignores signature. | No action needed (graceful degradation). |
  | Mixed v0.1/v0.2 environment | Depends on consumer strictness policy. | Document dual-version support strategy. |

- [x] Document recommended dual-version support strategy:
  - Consumer checks `manifestVersion` and applies appropriate validation.
  - Define sunset timeline for v0.1 acceptance.

### Phase 3 — Step-by-step migration walkthrough

- [x] Create `docs/guides/MIGRATION-V01-V02.md`:
  ```
  1. Understand What Changed
     - Summary of breaking vs. non-breaking changes
     - Compatibility matrix
  2. Migrate Your Consumer
     Step 1: Add signature verification capability
     Step 2: Add JCS canonicalization dependency
     Step 3: Add Ed25519 verification capability
     Step 4: Update validation logic for manifestVersion "0.2"
     Step 5: Update conformance tests
  3. Migrate Your Issuer
     Step 1: Generate or obtain Ed25519 signing key pair
     Step 2: Add JCS canonicalization dependency
     Step 3: Implement signing logic
     Step 4: Update manifest creation to include signature
     Step 5: Update conformance tests
  4. Handle Mixed Environments
     - Dual-version consumer strategy
     - Rollout recommendations
  5. Verify Your Migration
     - Run v0.2 conformance suite
     - Verify backward compatibility with v0.1 fixtures
  6. Deprecation Timeline
     - When v0.1 support will end
     - What "end of support" means
  ```

### Phase 4 — Code examples

- [x] Provide migration code examples for:
  - **TypeScript**: Before (v0.1 validation) -> After (v0.2 validation with signature verification).
  - **Python pseudocode**: Key generation, signing, verification steps.
  - **Go pseudocode**: Key generation, signing, verification steps.
- [x] Each example should be self-contained and runnable (TypeScript) or clearly annotated (pseudocode).
- [x] Include key generation guidance:
  - How to generate Ed25519 key pairs.
  - How to publish public keys at stable URLs (`signature.keyRef`).
  - Key rotation recommendations.

### Phase 5 — Deprecation timeline and support policy

- [x] Document in `docs/governance/DEPRECATION-POLICY.md`:
  - v0.1 remains supported for [N months] after v0.2 reaches stable status.
  - During the overlap period, the conformance suite includes both v0.1 and v0.2 fixtures.
  - After deprecation, v0.1 fixtures remain in the suite for historical testing but are marked as "legacy."
  - New features and security fixes apply only to v0.2+.
- [x] Define what "supported" means: conformance suite includes it, issues are triaged, docs are maintained.
- [x] Define what "deprecated" means: no new features, security-critical fixes only, docs marked as legacy.

### Phase 6 — Publish to docs site

- [x] Add migration guide to the Starlight docs site.
- [x] Cross-link from:
  - v0.1 spec page (with "upgrade to v0.2" callout).
  - v0.2 spec page (with "migrating from v0.1?" link).
  - Getting started pages.
  - Implementation guide (WO-0055).

## Key file paths (created/modified)

New files:
- `docs/guides/MIGRATION-V01-V02.md`
- `docs/governance/DEPRECATION-POLICY.md`
- `site/src/content/docs/guides/migration-v01-v02.md` (Starlight page)

Modified files:
- `spec/v0.1/README.md` (add migration callout)
- `spec/v0.2/README.md` (add "migrating from v0.1?" link)
- `site/src/content/docs/getting-started/` (cross-links)
- `docs/governance/GOVERNANCE.md` (link to deprecation policy)

## Acceptance criteria

- [x] Breaking changes catalog is complete and accurate (verified against spec diffs).
- [x] Compatibility matrix covers all consumer/issuer version combinations.
- [x] Step-by-step migration walkthrough exists for both consumer and issuer roles.
- [x] Code examples are provided for TypeScript (runnable) and at least one pseudocode language.
- [x] Deprecation timeline is defined with specific support durations.
- [x] Deprecation policy document exists in governance docs.
- [x] Migration guide is published on the docs site with cross-links from spec pages.
- [x] A v0.1 adopter reading the guide can produce a migration plan without additional context.
- [x] Guide explicitly states that v0.1 consumers can gracefully degrade when receiving v0.2 manifests (unknown-field tolerance).

## Validation commands

- `cd site && npm run build:clean` (docs site builds with new pages)
- Manual review of breaking changes catalog against actual spec diffs between `spec/v0.1/` and `spec/v0.2/`.
- Verify code examples compile/run (TypeScript examples).

## Dependencies and sequencing notes

- Depends on WO-0053 (conformance suite) for the "verify your migration" section.
- Depends on WO-0057 (spec-vs-implementation clarity) to ensure migration guide is spec-level, not TypeScript-specific.
- Contributes directly to Gate G6 (governance and change control) closure.
- The deprecation policy from Phase 5 should be coordinated with WO-0059 (governance completion).

## Execution summary (2026-03-02)

Completed with migration documentation and publishing links:

- `docs/guides/MIGRATION-V01-V02.md`
- `docs/governance/DEPRECATION-POLICY.md`
- `site/src/content/docs/guides/migration-v01-v02.md`
- Cross-links in spec and getting-started pages

Evidence:

- Site build success including migration route generation.
- Agent Task ID preserved: `e0a7fe60_1772165606`
