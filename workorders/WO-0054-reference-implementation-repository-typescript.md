# WO-0054 — Reference Implementation Repository (TypeScript)

**Status:** NOT_STARTED
**Created:** 2026-02-27
**Priority:** CRITICAL
**Blocks:** Gate G4 (Interoperability proof — first of 3+ implementations)
**Dependencies:** WO-0053 (Standalone Conformance Test Suite)
**Estimated effort:** 2-3 weeks

## Objective

Create a separate, public repository containing a minimal but complete TypeScript reference implementation of Universal Manifest. This serves as the first publicly verifiable implementation and as a template for other organizations building their own implementations.

## Why this work matters

The current TypeScript helper lives inside the spec repo at `packages/universal-manifest/`. This conflates the specification with one particular implementation, which:

1. Makes it harder for external adopters to see the spec as implementation-neutral.
2. Prevents the implementation from being the first "external-style" conformance proof.
3. Violates the principle that the spec repo should contain normative artifacts, not implementation code.

Gate G4 requires 3+ independent implementations from 3+ organizations, with 2+ external. The reference implementation in a separate repo becomes implementation #1 and provides the template that lowers the barrier for implementations #2 and #3.

## Scope

In scope:

- Create a new public GitHub repository (e.g., `universalmanifest/um-typescript`) containing a complete UM implementation.
- Implement: create, validate, sign (v0.2), verify, and resolve manifests.
- Integrate the conformance test suite from WO-0053 as a dependency or submodule.
- Pass all conformance levels (`v0.1-baseline` + `v0.2-baseline`).
- Include clear README, API docs, and "how to use this as a template" guide.
- Produce and publish a conformance report.

Out of scope:

- Removing the existing `packages/universal-manifest/` from the spec repo immediately (can coexist during transition).
- Building a full framework or runtime system.
- Implementing resolver infrastructure (that stays in `services/myum-resolver/`).

## Execution phases

### Phase 1 — Repository scaffold and extraction

- [ ] Create new repository with standard structure:
  ```
  um-typescript/
    src/
      manifest.ts       # create/validate manifests
      signer.ts         # v0.2 JCS+Ed25519 signing
      verifier.ts       # v0.2 signature verification
      resolver.ts       # UMID resolution client
      types.ts          # TypeScript type definitions
      index.ts          # public API surface
    tests/
      conformance/      # conformance suite integration
      unit/             # implementation-specific unit tests
    conformance-report.json  # generated conformance report
    package.json
    tsconfig.json
    README.md
    LICENSE
    CONFORMANCE.md      # how this impl maps to spec conformance
  ```
- [ ] Extract and refactor relevant code from `packages/universal-manifest/src/index.ts`.
- [ ] Ensure clean separation: no spec-repo-internal dependencies.

### Phase 2 — Core implementation

- [ ] `manifest.ts`: Create manifests with required fields, validate structure.
- [ ] `signer.ts`: JCS canonicalization + Ed25519 signing per `spec/v0.2/SIGNATURE-PROFILE.md`.
- [ ] `verifier.ts`: Signature verification including profile validation.
- [ ] `resolver.ts`: HTTP client for `myum.net/{UMID}` resolution.
- [ ] `types.ts`: Full TypeScript type definitions for v0.1 and v0.2 manifest shapes.
- [ ] Export clean public API from `index.ts`.

### Phase 3 — Conformance integration

- [ ] Add conformance test suite from WO-0053 as a dev dependency or git submodule.
- [ ] Build conformance adapter that wraps this implementation.
- [ ] Run conformance suite and verify all fixtures pass.
- [ ] Generate `conformance-report.json` as CI artifact.
- [ ] Add conformance badge to README.

### Phase 4 — Documentation and template guidance

- [ ] Write comprehensive README:
  - What this is (reference implementation of Universal Manifest spec).
  - Quick start (install, create manifest, sign, verify).
  - API reference.
  - How to use this repo as a template for your own implementation.
- [ ] Write `CONFORMANCE.md` explaining which conformance levels are met and how to verify.
- [ ] Add inline JSDoc/TSDoc for all public APIs.
- [ ] Include example scripts:
  - `examples/create-and-sign.ts`
  - `examples/verify-manifest.ts`
  - `examples/resolve-umid.ts`

### Phase 5 — CI and publishing

- [ ] Set up GitHub Actions CI:
  - Build + lint.
  - Unit tests.
  - Conformance suite run.
  - Conformance report generation.
- [ ] Configure npm publish (scoped package, e.g., `@universalmanifest/typescript`).
- [ ] Tag initial release with conformance report attached.

## Key file paths (created/modified)

New repository (external to spec repo):
- `um-typescript/` (new public GitHub repository)

Files modified in spec repo:
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/` (link to reference implementation)
- `/Users/grig/work/repo/universalmanifest/integrations/reference-runtime.md` (update to reference separate repo)
- `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md` (update implementation status)

## Acceptance criteria

- [ ] Separate public repository exists with complete UM TypeScript implementation.
- [ ] Implementation passes all v0.1-baseline conformance fixtures.
- [ ] Implementation passes all v0.2-baseline conformance fixtures (signing + verification).
- [ ] Conformance report is generated and validates against the report schema from WO-0053.
- [ ] README is clear enough for a developer or AI agent to:
  - Install the package.
  - Create a v0.1 manifest.
  - Sign a v0.2 manifest.
  - Verify a v0.2 manifest.
  - Run conformance tests.
- [ ] Repository has CI that runs conformance suite on every push.
- [ ] Repository has no dependencies on spec repo internals (fully standalone).
- [ ] "How to use this as a template" section exists and is actionable.
- [ ] npm package is published or ready to publish.

## Validation commands

- `cd um-typescript && npm test` (unit tests pass)
- `cd um-typescript && npm run conformance` (conformance suite passes)
- `cd um-typescript && npm run build` (clean TypeScript build)
- JSON schema validation of `conformance-report.json`

## Dependencies and sequencing notes

- Depends on WO-0053 (conformance suite must exist before this can integrate it).
- WO-0055 (adopter onboarding docs) should reference this repo as the primary example.
- WO-0057 (spec-vs-implementation clarity) should be coordinated: once this repo exists, update spec repo docs to clearly point to it as ONE implementation.
- The existing `packages/universal-manifest/` can coexist. A future WO can plan the transition to make the separate repo the canonical implementation.
