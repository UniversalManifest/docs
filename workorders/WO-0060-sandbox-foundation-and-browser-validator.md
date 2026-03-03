# WO-0060 -- Sandbox Foundation and Browser Validator

**Status:** COMPLETED
**Created:** 2026-02-27
**Priority:** HIGHEST (per CEO mandate)
**Blocks:** WO-0061, WO-0062, WO-0063, WO-0064, WO-0065, WO-0066, WO-0067, WO-0068
**Dependencies:** None (foundational work order for the sandbox)
**Estimated effort:** 1 week
**Mandate:** [MANDATE-interactive-implementation-sandbox.md](/docs/MANDATE-interactive-implementation-sandbox.md)
**Proposal:** [PROPOSAL-interactive-implementation-sandbox.md](/.dev/ai/proposals/PROPOSAL-interactive-implementation-sandbox.md)

## Objective

Build the browser-compatible validation module that runs the same logic as `packages/universal-manifest/src/index.ts` but uses the Web Crypto API instead of `node:crypto`. This is the foundation that all sandbox scenarios depend on. Without real validation running in the browser, the sandbox is a mockup, not a proof.

## Why this work matters

The CEO mandate is explicit: "not a simulation of validation -- real validation." The existing validation logic uses Node.js `crypto` for Ed25519 signature verification. This work order extracts the platform-independent logic and provides a Web Crypto adapter so the same validation functions run in the browser with identical results.

## Scope

In scope:
- Extract pure-JS validation functions from `packages/universal-manifest/src/index.ts` into browser-compatible modules
- Create a Web Crypto API adapter for Ed25519 signature verification
- Create the JCS canonicalization module (already pure JS, just needs extraction)
- Create the sandbox TypeScript type definitions (`SandboxStep`, `ScenarioDefinition`, etc.)
- Create the fixture serving pipeline (copy/symlink fixtures to `site/public/sandbox/fixtures/`)
- Set up the Astro page routes for `/sandbox/` and `/sandbox/[scenario]/`
- Verify that all existing fixtures produce identical pass/fail results in both Node and browser

Out of scope:
- Three-panel layout (WO-0061)
- Scenario definitions (WO-0063 through WO-0066)
- Visual polish (WO-0067)

## Execution phases

### Phase 1 -- Extract platform-independent validation logic

- [ ] Create `site/src/scripts/sandbox/validator-browser.ts`:
  - Copy `assertUniversalManifestV01`, `assertUniversalManifestV01Fresh` (pure JS, no changes needed)
  - Copy `assertSignatureV02` (pure JS structural checks, no changes)
  - Copy `assertIsoDateTime`, `jsonLdTypeIncludes` (pure JS helpers)
  - Create `assertUniversalManifestV02` that uses the async Web Crypto adapter instead of `node:crypto`
  - Export the same function signatures as the Node package (with `assertUniversalManifestV02` becoming async)
- [ ] Create `site/src/scripts/sandbox/canonicalize.ts`:
  - Extract `canonicalizeJson` function (already pure JS)
- [ ] Create `site/src/scripts/sandbox/crypto-browser.ts`:
  - Implement `verifyEd25519Signature(publicKeySpkiB64, canonicalPayload, signatureBase64url)` using Web Crypto API
  - Implement `base64Decode` and `base64urlDecode` utility functions
  - Handle browser compatibility (Ed25519 requires Chrome 113+, Safari 17+, Firefox 129+)
  - Provide a clear error message if the browser does not support Ed25519

### Phase 2 -- Type definitions and scenario framework

- [ ] Create `site/src/scripts/sandbox/types.ts` with:
  - `ScenarioDefinition` interface
  - `SandboxStep` interface
  - `ScenarioCategory` type
  - `StepResult` interface
  - `PanelAnnotation` interface
  - `ConsumerRendering` interface
  - `EntityPanelState`, `ConsumerPanelState`, `ProtocolPanelState` interfaces
- [ ] Create `site/src/scripts/sandbox/scenarios/index.ts` (empty registry scaffold)

### Phase 3 -- Fixture serving pipeline

- [ ] Create `site/public/sandbox/fixtures/` directory
- [ ] Add a build-time script (or extend `sync:harness-fixtures`) to copy fixtures from:
  - `examples/v0.1/*.jsonld` -> `site/public/sandbox/fixtures/v0.1/`
  - `examples/v0.1/stubs/*.jsonld` -> `site/public/sandbox/fixtures/v0.1/stubs/`
  - `examples/v0.1/invalid/*.jsonld` -> `site/public/sandbox/fixtures/v0.1/invalid/`
  - `examples/v0.2/*.jsonld` -> `site/public/sandbox/fixtures/v0.2/`
  - `examples/v0.2/invalid/*.jsonld` -> `site/public/sandbox/fixtures/v0.2/invalid/`
- [ ] Update `site/package.json` scripts to include fixture sync in `dev` and `build` commands

### Phase 4 -- Astro page scaffolds

- [ ] Create `site/src/pages/sandbox/index.astro` (minimal scaffold -- will be filled in WO-0062)
- [ ] Create `site/src/pages/sandbox/[...scenario].astro` (dynamic route scaffold)
- [ ] Update `site/astro.config.mjs` to add sandbox link in the sidebar Tools section
- [ ] Verify `npm run build:clean` succeeds with the new pages

### Phase 5 -- Parity verification

- [ ] Create a test script that runs all fixtures through both:
  - Node validator (`packages/universal-manifest/src/index.ts`)
  - Browser validator (via a simple Node script that imports the browser module with `node:crypto` polyfill OR via Playwright headless)
- [ ] Assert identical pass/fail results for every fixture
- [ ] Document any intentional differences (e.g., v0.2 verification is async in browser)

## Key file paths (created)

- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/validator-browser.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/crypto-browser.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/canonicalize.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/types.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/index.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/sandbox/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/sandbox/[...scenario].astro`
- `/Users/grig/work/repo/universalmanifest/site/public/sandbox/fixtures/` (directory)

## Acceptance criteria

- [ ] `assertUniversalManifestV01` runs in the browser and produces identical results to the Node version for all v0.1 fixtures (valid and invalid)
- [ ] `assertUniversalManifestV02` runs in the browser with Web Crypto and produces identical results to the Node version for all v0.2 fixtures (valid and invalid)
- [ ] `canonicalizeJson` produces byte-identical output in browser and Node
- [ ] Type definitions compile without errors
- [ ] `/sandbox/` and `/sandbox/test/` routes are accessible in dev server
- [ ] `npm run build:clean` succeeds with sandbox pages
- [ ] Fixture files are served at `/sandbox/fixtures/v0.1/minimal-manifest.jsonld` etc.
- [ ] Parity test script passes with zero mismatches

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
- `cd /Users/grig/work/repo/universalmanifest/site && npm run dev` (verify /sandbox/ route)
- Parity test script (created in Phase 5)
