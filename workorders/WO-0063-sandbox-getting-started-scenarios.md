# WO-0063 -- Sandbox Getting Started Scenarios

**Status:** COMPLETED
**Created:** 2026-02-27
**Priority:** HIGHEST
**Blocks:** WO-0067 (visual polish)
**Dependencies:** WO-0062 (scenario modal and navigation)
**Estimated effort:** 3-4 days
**Mandate:** [MANDATE-interactive-implementation-sandbox.md](/docs/MANDATE-interactive-implementation-sandbox.md)
**Proposal:** [PROPOSAL-interactive-implementation-sandbox.md](/.dev/ai/proposals/PROPOSAL-interactive-implementation-sandbox.md)

## Objective

Implement the 4 "Getting Started" scenarios (GS-01 through GS-04) that introduce first-time users to Universal Manifest. These are the most important scenarios -- the mandate says "someone who has never heard of Universal Manifest should understand what it does and why it matters after stepping through 2-3 scenarios."

## Why this work matters

Getting Started scenarios are the first demo-able milestone. When GS-01 through GS-04 are complete, the sandbox can be shown to stakeholders and potential adopters. These scenarios demonstrate core concepts (validation, facets, forward compatibility, resolution) without requiring cryptographic features.

## Scope

Implement 4 scenario definition files with full step definitions, panel states, bubble text, and action callbacks.

## Scenarios

### GS-01: Your First Manifest (7 steps)

- **Fixture:** `examples/v0.1/minimal-manifest.jsonld`
- **Steps:** Parse -> check @context -> check @id + @type -> check manifestVersion + subject -> check issuedAt + expiresAt -> TTL freshness -> all passed
- **Actions:** Steps 3-6 call `assertUniversalManifestV01` field-by-field logic; step 6 calls `assertUniversalManifestV01Fresh`
- **Modifiable:** Yes -- user can remove fields or change dates to see validation fail

### GS-02: Manifest with Facets (6 steps)

- **Fixture:** `examples/v0.1/manifest-with-facets.jsonld`
- **Steps:** Show manifest -> structural validation -> facet type checks -> read profile facet -> read device facet -> summary
- **Actions:** Step 2 calls `assertUniversalManifestV01`; step 3 validates each facet's `@type`
- **Modifiable:** Yes -- user can change facet types or change `facets` to non-array

### GS-03: Forward Compatibility (5 steps)

- **Fixture:** `examples/v0.1/unknown-fields-manifest.jsonld`
- **Steps:** Show manifest with unknown fields -> validation passes -> consumer reads known fields -> unknown fields grayed out -> summary
- **Actions:** Step 2 calls `assertUniversalManifestV01` (must pass despite unknown fields)
- **Modifiable:** Yes -- user can add more unknown fields (still passes) or remove required fields (fails)

### GS-04: Resolver Lookup (6 steps)

- **Fixture:** `examples/v0.1/minimal-manifest.jsonld` (simulated resolver response)
- **Steps:** Consumer has only UMID -> construct resolver URL -> resolver responds -> structural validation -> freshness check -> accepted
- **Actions:** Step 4 calls `assertUniversalManifestV01`; step 5 calls `assertUniversalManifestV01Fresh`
- **Note:** Resolver response is simulated (not a real HTTP call). The scenario shows the concept and validates the returned manifest.

## Execution tasks

- [ ] Create `site/src/scripts/sandbox/scenarios/getting-started/gs-01-first-manifest.ts`
- [ ] Create `site/src/scripts/sandbox/scenarios/getting-started/gs-02-manifest-with-facets.ts`
- [ ] Create `site/src/scripts/sandbox/scenarios/getting-started/gs-03-forward-compatibility.ts`
- [ ] Create `site/src/scripts/sandbox/scenarios/getting-started/gs-04-resolver-lookup.ts`
- [ ] Register all 4 in `site/src/scripts/sandbox/scenarios/index.ts`
- [ ] Add placeholder illustrations for each scenario card
- [ ] Verify each scenario runs end-to-end in the sandbox layout:
  - All steps navigate correctly
  - Validation actions produce correct pass/fail results
  - Modifying the manifest and re-running produces different results
  - Bubbles display correct text at each step
  - Panel content updates correctly at each step

## Acceptance criteria

- [ ] GS-01 runs end-to-end: 7 steps, validation passes, bubble text explains each step
- [ ] GS-02 runs end-to-end: 6 steps, facet validation works, profile facet is rendered
- [ ] GS-03 runs end-to-end: 5 steps, unknown fields are shown and ignored
- [ ] GS-04 runs end-to-end: 6 steps, simulated resolver flow with real validation
- [ ] Editing the manifest in GS-01 and removing `@context` produces "Missing @context" error at the correct step
- [ ] Editing the manifest in GS-01 and changing `expiresAt` to a past date produces "Manifest expired" at the freshness step
- [ ] All 4 scenarios appear in the scenario modal under "Getting Started"
- [ ] `npm run build:clean` succeeds

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
- `cd /Users/grig/work/repo/universalmanifest/site && npm run dev` (test each scenario)
