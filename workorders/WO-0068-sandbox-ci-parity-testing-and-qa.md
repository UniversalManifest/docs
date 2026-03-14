# WO-0068 -- Sandbox CI Parity Testing and QA

**Status:** COMPLETED
**Owner Approval:** 2026-03-02 (explicit closure approval)
**Created:** 2026-02-27
**Priority:** HIGH
**Blocks:** None (final quality gate)
**Dependencies:** WO-0060 (browser validator), WO-0063, WO-0064, WO-0065, WO-0066 (all scenarios)
**Estimated effort:** 2-3 days
**Mandate:** [MANDATE-interactive-implementation-sandbox.md](/docs/MANDATE-interactive-implementation-sandbox.md)
**Proposal:** [PROPOSAL-interactive-implementation-sandbox.md](/.dev/ai/proposals/PROPOSAL-interactive-implementation-sandbox.md)

## Objective

Ensure the browser validator produces identical results to the Node validator for all fixtures, automate this check in CI, and perform end-to-end QA on all 25 scenarios.

## Why this work matters

The mandate is explicit: "The logic must use the same validation logic used by our actual validators (not a simulation of validation -- real validation)." Parity testing in CI guarantees that any future changes to the Node validator are detected if they would cause the browser validator to diverge.

## Scope

In scope:
- Automated parity test: Node validator vs browser validator for all fixtures
- CI integration: add parity test to `.github/workflows/ci.yml`
- End-to-end scenario smoke tests (Playwright or similar)
- Accessibility audit (keyboard navigation, screen reader compatibility)
- Performance audit (bundle size, load time, step transition speed)

Out of scope:
- Changing validation logic (WO-0060)
- Changing scenarios (WO-0063 through WO-0066)

## Execution phases

### Phase 1 -- Parity test script

- [x] Create `site/scripts/test-validator-parity.mjs`:
  - Load all fixtures from `examples/v0.1/`, `examples/v0.1/invalid/`, `examples/v0.2/`, `examples/v0.2/invalid/`
  - Run each through the Node validator (`packages/universal-manifest/src/index.ts`)
  - Run each through the browser validator (`site/src/scripts/sandbox/validator-browser.ts`, loaded via a Node-compatible entry point or bundled for Playwright)
  - Compare results: same pass/fail, same error messages
  - Report any mismatches with fixture name, expected result, and actual result
  - Exit with non-zero code if any mismatch

### Phase 2 -- CI integration

- [x] Add a `parity-test` job to `.github/workflows/ci.yml`:
  - Runs after the existing `test` job
  - Depends on `build` job (site must build first)
  - Executes `site/scripts/test-validator-parity.mjs`
  - Fails the pipeline if any mismatch is detected
- [x] Verify the CI pipeline passes with current code

### Phase 3 -- Scenario smoke tests

- [x] Create `site/scripts/test-scenarios-smoke.mjs` (or use Playwright):
  - For each of the 25 scenarios:
    - Navigate to `/sandbox/{scenario-id}/`
    - Verify the page loads without errors
    - Click "Next" through all steps
    - Verify no console errors at any step
    - Verify the final step reaches the expected outcome (pass or fail)
  - For at least 3 scenarios (GS-01, TV-01, TV-02):
    - Open the JSON editor
    - Modify a value
    - Click "Run"
    - Verify the outcome changes
- [x] Add to CI as a `smoke-test` job (runs after `build`)

### Phase 4 -- Accessibility audit

- [x] Keyboard navigation: verify all controls are reachable with Tab, usable with Enter/Space
- [x] Arrow key navigation: verify step prev/next, card selection
- [x] Screen reader: verify all panels have ARIA labels, bubbles are announced
- [x] Focus management: verify focus moves correctly when:
  - Opening/closing modal
  - Navigating between steps
  - Opening/closing the JSON editor
- [x] Color contrast: verify all text meets WCAG 2.1 AA contrast ratios
- [x] Document accessibility findings and fix critical issues

### Phase 5 -- Performance audit

- [x] Measure and document:
  - Total JS bundle size for sandbox (target: <50KB gzipped for engine + validator + one scenario)
  - Time to interactive for `/sandbox/` (target: <2 seconds on 4G)
  - Step transition latency (target: <100ms perceived)
  - Ed25519 verification latency in browser (target: <500ms)
- [x] Identify and fix any performance issues:
  - Lazy loading: verify scenario definitions are not all loaded upfront
  - Code splitting: verify Vite splits per scenario category
  - Fixture caching: verify fixtures are fetched once per scenario, not per step

## Key file paths (created)

- `site/scripts/test-validator-parity.mjs`
- `site/scripts/test-scenarios-smoke.mjs` (or Playwright config)
- Updated: `.github/workflows/ci.yml`

## Acceptance criteria

- [x] Parity test passes: Node and browser validators produce identical results for all fixtures (v0.1 valid, v0.1 invalid, v0.2 valid, v0.2 invalid)
- [x] CI pipeline includes parity test and it passes
- [x] Scenario smoke tests pass: all 25 scenarios load and complete without errors
- [x] Modification smoke tests pass: editing JSON in GS-01, TV-01, TV-02 changes the outcome
- [x] No WCAG 2.1 AA accessibility violations in critical paths
- [x] JS bundle size is <50KB gzipped (engine + validator + one scenario)
- [x] Time to interactive is <2 seconds on simulated 4G
- [x] Ed25519 verification completes in <500ms in browser

## Validation commands

- `cd site && node scripts/test-validator-parity.mjs`
- `cd site && node scripts/test-scenarios-smoke.mjs` (or Playwright equivalent)
- `cd  && npm run build && npm test` (CI equivalent)
- Lighthouse audit on `/sandbox/` page
