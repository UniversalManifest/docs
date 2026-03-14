# WO-0064 -- Sandbox Trust and Verification Scenarios

**Status:** COMPLETED
**Created:** 2026-02-27
**Priority:** HIGHEST
**Blocks:** WO-0067 (visual polish)
**Dependencies:** WO-0063 (getting started scenarios -- confirms the framework works end-to-end)
**Estimated effort:** 4-5 days
**Mandate:** [MANDATE-interactive-implementation-sandbox.md](/docs/MANDATE-interactive-implementation-sandbox.md)
**Proposal:** [PROPOSAL-interactive-implementation-sandbox.md](/.dev/ai/proposals/PROPOSAL-interactive-implementation-sandbox.md)

## Objective

Implement the 5 "Trust & Verification" scenarios (TV-01 through TV-05) that demonstrate v0.2 cryptographic signature verification, tamper detection, TTL enforcement, required field validation, and downgrade attack prevention. These scenarios use the browser Ed25519 verification from WO-0060.

## Why this work matters

v0.2 signature verification is the most technically impressive feature of Universal Manifest. Showing real Ed25519 verification running in the browser, with the ability to tamper with a field and watch verification fail, is the strongest possible proof that the spec works. This is what converts skeptical adopters.

## Scope

Implement 5 scenario definition files. TV-01 is the most complex (8 steps with full crypto flow). TV-02 through TV-05 are failure cases that demonstrate specific rejection behaviors.

## Scenarios

### TV-01: Signed Manifest (Ed25519 Verification) (8 steps)

- **Fixture:** `examples/v0.2/minimal-signed-manifest.jsonld`
- **Steps:** Show manifest -> read version 0.2 -> validate signature -> extract public key -> remove signature + create signing input -> JCS canonicalization -> Ed25519 verify -> accepted
- **Actions:** Steps 3-7 call the individual parts of `assertUniversalManifestV02`; step 7 calls Web Crypto `verify()`
- **Key visual:** Lock icon transitions from open to closed on success
- **Modifiable:** Yes -- changing ANY field causes step 7 to fail ("Signature verification failed")

### TV-02: Tampered Manifest Detection (7 steps)

- **Fixture:** `examples/v0.2/invalid/tampering-modified-after-signing.jsonld`
- **Steps:** Show tampered manifest -> structural validation passes -> signature OK -> public key extraction -> canonicalize modified data -> Ed25519 verify FAILS -> rejected
- **Actions:** Steps 2-6 proceed normally; step 6 calls Web Crypto `verify()` which returns false
- **Key visual:** Shield icon transitions to red X on failure
- **Modifiable:** Yes -- but this fixture is constructed to always fail regardless of edits

### TV-03: Expired Manifest Rejection (5 steps)

- **Fixture:** `examples/v0.1/invalid/expired-for-use.jsonld`
- **Steps:** Show expired manifest -> structural validation passes -> freshness check: now > expiresAt -> EXPIRED -> consumer rejects
- **Actions:** Step 2 calls `assertUniversalManifestV01` (passes); step 3 calls `assertUniversalManifestV01Fresh` (fails)
- **Key visual:** Clock icon with expired state
- **Modifiable:** Yes -- changing `expiresAt` to a future date makes it pass

### TV-04: Missing Required Fields (4 steps)

- **Fixture:** `examples/v0.1/invalid/missing-context.jsonld`
- **Steps:** Show invalid manifest -> validation begins -> @context check FAILS -> rejected
- **Actions:** Step 2 calls `assertUniversalManifestV01` which throws "Missing @context"
- **Key visual:** Red gap where the missing field should be
- **Modifiable:** Yes -- adding `@context` moves to the next check (may find other issues)

### TV-05: Invalid Signature Algorithm (5 steps)

- **Fixture:** `examples/v0.2/invalid/invalid-signature-algorithm.jsonld`
- **Steps:** Show manifest with wrong algorithm -> read version 0.2 -> algorithm check FAILS -> error -> rejected
- **Actions:** Step 3 calls `assertSignatureV02` which throws "signature.algorithm must be Ed25519"
- **Key visual:** Algorithm field highlighted in red
- **Modifiable:** Yes -- changing algorithm to "Ed25519" passes this check (but full verification may still fail)

## Execution tasks

- [ ] Create `site/src/scripts/sandbox/scenarios/trust-verification/tv-01-signed-manifest.ts`
- [ ] Create `site/src/scripts/sandbox/scenarios/trust-verification/tv-02-tampered-manifest.ts`
- [ ] Create `site/src/scripts/sandbox/scenarios/trust-verification/tv-03-expired-manifest.ts`
- [ ] Create `site/src/scripts/sandbox/scenarios/trust-verification/tv-04-missing-fields.ts`
- [ ] Create `site/src/scripts/sandbox/scenarios/trust-verification/tv-05-invalid-algorithm.ts`
- [ ] Register all 5 in scenario registry
- [ ] Add placeholder illustrations
- [ ] Create reusable consumer panel components for TV scenarios:
  - Lock icon component with open/closed/error states
  - Shield icon component with OK/error states
  - Clock icon component with active/expired states
- [ ] Verify TV-01 performs real Ed25519 verification in the browser:
  - Passes with the unmodified fixture
  - Fails when the user changes any manifest field
- [ ] Verify TV-02 shows verification failure with the tampered fixture

## Acceptance criteria

- [ ] TV-01 runs end-to-end: 8 steps, real Ed25519 verification passes in browser
- [ ] TV-01 modification test: changing `subject` field causes verification failure at step 7
- [ ] TV-02 runs end-to-end: 7 steps, tampered manifest is detected and rejected
- [ ] TV-03 runs end-to-end: 5 steps, expired manifest is rejected with correct error
- [ ] TV-04 runs end-to-end: 4 steps, missing @context is caught immediately
- [ ] TV-05 runs end-to-end: 5 steps, wrong algorithm is rejected
- [ ] All 5 scenarios appear in the modal under "Trust & Verification"
- [ ] Real Web Crypto Ed25519 verification is used (not simulated)
- [ ] `npm run build:clean` succeeds

## Validation commands

- `cd site && npm run build:clean`
- `cd site && npm run dev` (test each scenario)
- Browser DevTools console: verify no simulation warnings, real crypto.subtle calls
