# WO-0065 -- Sandbox Integration Lane Scenarios

**Status:** COMPLETED
**Created:** 2026-02-27
**Priority:** HIGHEST
**Blocks:** WO-0067 (visual polish)
**Dependencies:** WO-0063 (getting started scenarios -- confirms the framework works)
**Estimated effort:** 5-6 days
**Mandate:** [MANDATE-interactive-implementation-sandbox.md](/docs/MANDATE-interactive-implementation-sandbox.md)
**Scenario catalog:** `site/public/agent/sandbox-scenarios.json`

## Objective

Implement the 8 "Integration Lane" scenarios (IL-01 through IL-08) that demonstrate how Universal Manifest works across real-world integration surfaces: social profiles, smart glasses, metaverse worlds, spatial fabric, OMATrust, Chia blockchain, proof-of-personhood, and venue edge nodes.

## Why this work matters

Integration lane scenarios show the breadth of Universal Manifest. They prove this is not a narrow-purpose format but a genuinely portable standard that works across diverse systems. Each scenario demonstrates a different industry use case, making the spec relevant to a wide audience.

## Scope

Implement 8 scenario definition files. Each uses an existing fixture stub from `examples/v0.1/stubs/`. Each has 7 steps showing the flow from manifest receipt to consumer projection. These scenarios emphasize consent checking, facet extraction, and domain-specific rendering.

## Scenarios

### IL-01: Social Profile Projection (7 steps)

- **Fixture:** `examples/v0.1/stubs/social-profile-manifest.jsonld`
- **Consumer:** Social profile rendering service
- **Key concepts:** Consent gating (`social.profilePublic`), facet extraction (`publicProfile`), schema:Person rendering, pointer resolution
- **Modifiable:** Yes -- changing consent to "denied" blocks rendering

### IL-02: Smart Glasses Consent Check (7 steps)

- **Fixture:** `examples/v0.1/stubs/smart-glasses-ar-consent-allowed-manifest.jsonld`
- **Consumer:** Smart glasses AR runtime
- **Key concepts:** Consent matrix evaluation (`ar.recording.*`, `ar.profile.*`), per-capability permission decisions, context-dependent access
- **Modifiable:** Yes -- changing consent keys changes the permission matrix
- **Reusable component:** ConsentMatrix component showing allowed/denied/restricted per capability

### IL-03: Metaverse Cross-World Identity (7 steps)

- **Fixture:** `examples/v0.1/stubs/metaverse-crossworld-profile-manifest.jsonld`
- **Consumer:** Two virtual worlds receiving the same manifest
- **Key concepts:** Cross-system projection, consent per world feature, facet with supported worlds list
- **Modifiable:** Yes -- changing `metaverse.voiceCapture` consent changes voice features

### IL-04: RP1 Spatial Fabric Anchoring (7 steps)

- **Fixture:** `examples/v0.1/stubs/rp1-spatial-fabric-manifest.jsonld`
- **Consumer:** RP1 spatial fabric node
- **Key concepts:** Spatial anchor data, place membership, cross-world linking consent, coordinate data in facets
- **Modifiable:** Yes -- changing `spatial.crossWorldLinking` consent changes cross-world behavior

### IL-05: OMATrust Attestation Lifecycle (7 steps)

- **Fixture:** `examples/v0.1/stubs/oma-trust-lifecycle-edge-service-manifest.jsonld`
- **Consumer:** OMATrust-aware consumer portal
- **Key concepts:** Attestation lifecycle events (active -> revoked -> superseded), trust mode claims, revocation log pointer
- **Modifiable:** Yes -- removing lifecycle events changes the attestation state

### IL-06: Chia DID/VC Credential Binding (7 steps)

- **Fixture:** `examples/v0.1/stubs/chia-credential-lane-manifest.jsonld`
- **Consumer:** Credential verification service
- **Key concepts:** Blockchain DID binding, on-chain proof hash, credential share consent, on-chain publish restriction
- **Modifiable:** Yes -- changing `chia.credentialShare` consent hides credential data

### IL-07: Proof-of-Personhood Multi-Provider (7 steps)

- **Fixture:** `examples/v0.1/stubs/bluesky-personhood-multi-credential-manifest.jsonld`
- **Consumer:** Social platform evaluating Sybil resistance
- **Key concepts:** Multi-provider claims coexistence, trust threshold evaluation, independent provider checking, cross-platform linking consent
- **Modifiable:** Yes -- removing a provider claim reduces the trust signal count

### IL-08: Venue Edge Node Manifest (7 steps)

- **Fixture:** `examples/v0.1/stubs/venue-edge-manifest.jsonld`
- **Consumer:** Edge node + enrolled display device
- **Key concepts:** Venue identity, content policy facets (safe mode, content rules), device enrollment, edge discovery
- **Modifiable:** Yes -- changing policy values changes content rendering rules

## Execution tasks

- [ ] Create all 8 scenario definition files in `site/src/scripts/sandbox/scenarios/integration-lanes/`
- [ ] Register all 8 in scenario registry
- [ ] Add placeholder illustrations for each
- [ ] Create reusable consumer panel components:
  - `ConsentMatrix.astro` -- grid of capability + allowed/denied/restricted (for IL-02, IL-03, IL-04)
  - `ProfileCard.astro` -- rendered profile preview (for IL-01)
  - `AttestationTimeline.astro` -- lifecycle events timeline (for IL-05)
  - `CredentialBadge.astro` -- verified/unverified credential indicator (for IL-06, IL-07)
  - `PolicyCard.astro` -- venue content policy display (for IL-08)
- [ ] Verify each scenario runs end-to-end with correct validation
- [ ] Verify consent modification changes the consumer's behavior in each scenario

## Acceptance criteria

- [ ] All 8 scenarios run end-to-end (7 steps each)
- [ ] Each scenario uses a real fixture from `examples/v0.1/stubs/`
- [ ] Structural validation runs on the real fixture and passes
- [ ] Consent modification tests work:
  - IL-01: changing `social.profilePublic` to "denied" blocks profile rendering
  - IL-02: changing consent keys changes the permission matrix
  - IL-06: changing `chia.credentialShare` to "denied" hides credential data
- [ ] All 8 appear in the modal under "Integration Lanes"
- [ ] Integration-specific consumer components render correctly
- [ ] `npm run build:clean` succeeds

## Validation commands

- `cd site && npm run build:clean`
- `cd site && npm run dev` (test each scenario)
