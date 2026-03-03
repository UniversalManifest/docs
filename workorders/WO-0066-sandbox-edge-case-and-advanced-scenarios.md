# WO-0066 -- Sandbox Edge Case and Advanced Scenarios

**Status:** COMPLETED
**Created:** 2026-02-27
**Priority:** HIGHEST
**Blocks:** WO-0067 (visual polish)
**Dependencies:** WO-0064 (trust and verification scenarios -- confirms crypto works in browser)
**Estimated effort:** 4-5 days
**Mandate:** [MANDATE-interactive-implementation-sandbox.md](/docs/MANDATE-interactive-implementation-sandbox.md)
**Proposal:** [PROPOSAL-interactive-implementation-sandbox.md](/.dev/ai/proposals/PROPOSAL-interactive-implementation-sandbox.md)

## Objective

Implement the 4 "Edge Cases" scenarios (EC-01 through EC-04) and the 4 "Advanced" scenarios (AD-01 through AD-04). Edge cases demonstrate specific failure modes. Advanced scenarios demonstrate sophisticated multi-consumer and multi-feature flows.

## Why this work matters

Edge cases prove the validation logic catches real attacks and mistakes. Advanced scenarios demonstrate the full power of Universal Manifest: cross-system projection, pointer resolution, revocation awareness, and signed manifests with complex data. These are what convince technical evaluators that the spec is production-ready.

## Scope

Implement 8 scenario definition files. This includes creating one new composite fixture for AD-01 (cross-system projection).

## Edge Case Scenarios

### EC-01: Issued After Expires (4 steps)

- **Fixture:** `examples/v0.1/invalid/issued-after-expires.jsonld`
- **Key point:** Temporal inconsistency caught by `issuedAt <= expiresAt` check

### EC-02: Missing Signature v0.2 (4 steps)

- **Fixture:** `examples/v0.2/invalid/missing-signature.jsonld`
- **Key point:** v0.2 requires signature; prevents signature stripping attacks

### EC-03: Clock Skew Detection (5 steps)

- **Fixture:** `examples/v0.2/invalid/clock-skew-future-issuedAt.jsonld`
- **Key point:** SHOULD-level check for future `issuedAt`

### EC-04: Shard Type Violation (4 steps)

- **Fixture:** `examples/v0.1/invalid/shard-wrong-type.jsonld`
- **Key point:** Every shard must include `um:Shard` in `@type`

## Advanced Scenarios

### AD-01: Cross-System Projection (8 steps)

- **Fixture:** New composite fixture to be created
- **Key point:** Same manifest projected by 3 different consumers (social, AR, metaverse)
- **Consumer panel:** Three consumer cards stacked showing different projections
- **New fixture needed:** Combine elements from social-profile, smart-glasses, and metaverse stubs into one manifest

### AD-02: Manifest with Pointers (7 steps)

- **Fixture:** `examples/v0.2/manifest-with-pointers-signed.jsonld`
- **Key point:** Pointers reference external resources; manifest is lightweight; signed

### AD-03: Revocation-Aware Verification (8 steps)

- **Fixture:** `examples/v0.2/manifest-with-revocation-metadata.jsonld`
- **Key point:** Extended verification flow including revocation status check (simulated endpoint)
- **Consumer panel:** Shows revocation check as an additional step after signature verification

### AD-04: v0.2 Full Integration (8 steps)

- **Fixture:** `examples/v0.2/manifest-with-shards-signed.jsonld`
- **Key point:** Four-layer validation (structure + shards + signature + Ed25519 verify)
- **Demonstrates:** The full power of v0.2

## Execution tasks

### Edge case scenarios

- [ ] Create `site/src/scripts/sandbox/scenarios/edge-cases/ec-01-issued-after-expires.ts`
- [ ] Create `site/src/scripts/sandbox/scenarios/edge-cases/ec-02-missing-signature.ts`
- [ ] Create `site/src/scripts/sandbox/scenarios/edge-cases/ec-03-clock-skew.ts`
- [ ] Create `site/src/scripts/sandbox/scenarios/edge-cases/ec-04-shard-type-violation.ts`

### Advanced scenarios

- [ ] Create the composite fixture for AD-01:
  - File: `examples/v0.1/stubs/cross-system-projection-manifest.jsonld`
  - Contents: combine social profile shard + AR consent keys + metaverse cross-world shard + metaverse/AR/social pointers + multiple consent keys
  - Must pass `assertUniversalManifestV01` validation
- [ ] Create `site/src/scripts/sandbox/scenarios/advanced/ad-01-cross-system-projection.ts`
- [ ] Create `site/src/scripts/sandbox/scenarios/advanced/ad-02-pointers-signed.ts`
- [ ] Create `site/src/scripts/sandbox/scenarios/advanced/ad-03-revocation-aware.ts`
- [ ] Create `site/src/scripts/sandbox/scenarios/advanced/ad-04-full-v02-integration.ts`

### Registration and integration

- [ ] Register all 8 in scenario registry
- [ ] Add placeholder illustrations
- [ ] Verify each scenario runs end-to-end
- [ ] Verify edge case scenarios correctly show failure states
- [ ] Verify AD-01 shows three different consumer projections from one manifest
- [ ] Verify AD-03 shows simulated revocation check
- [ ] Verify AD-04 performs real Ed25519 verification

## Key file paths (created)

- `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/cross-system-projection-manifest.jsonld` (new fixture)
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/edge-cases/ec-01-issued-after-expires.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/edge-cases/ec-02-missing-signature.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/edge-cases/ec-03-clock-skew.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/edge-cases/ec-04-shard-type-violation.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/advanced/ad-01-cross-system-projection.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/advanced/ad-02-pointers-signed.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/advanced/ad-03-revocation-aware.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/advanced/ad-04-full-v02-integration.ts`

## Acceptance criteria

- [ ] EC-01 through EC-04 run end-to-end, each showing the correct failure at the correct step
- [ ] AD-01 shows three consumer projections from one manifest, each extracting different data
- [ ] AD-02 demonstrates pointer-only manifests with real signature verification
- [ ] AD-03 demonstrates revocation-aware verification with simulated status endpoint
- [ ] AD-04 demonstrates four-layer validation with real Ed25519 verification
- [ ] New composite fixture for AD-01 passes `assertUniversalManifestV01` validation
- [ ] All 8 appear in the modal under their respective categories
- [ ] `npm run build:clean` succeeds

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test` (verify new fixture passes)
- `cd /Users/grig/work/repo/universalmanifest/site && npm run dev` (test each scenario)
