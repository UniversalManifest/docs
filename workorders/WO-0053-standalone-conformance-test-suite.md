# WO-0053 — Standalone Conformance Test Suite

**Status:** NOT_STARTED
**Created:** 2026-02-27
**Priority:** CRITICAL
**Blocks:** Gate G4 (Interoperability proof), Gate G2 (Conformance testability)
**Dependencies:** None (foundational work order; other WOs in this wave depend on this)
**Estimated effort:** 2-3 weeks

## Objective

Extract Universal Manifest conformance tests into a standalone, publicly consumable test suite that any implementation in any language can run to prove v0.1 and v0.2 conformance. This is the single most critical enabler for Gate G4 (3+ independent implementations from 3+ organizations).

## Why this work matters

Today, conformance fixtures and validation logic are embedded inside the spec repo under `packages/universal-manifest/` and `examples/`. An external adopter building a Python, Rust, Go, or Java implementation has no turnkey way to:

1. Download a self-contained conformance package.
2. Run tests against their implementation.
3. Produce a machine-readable conformance report.
4. Prove to the UM project that they pass.

Without this, Gate G4 cannot be satisfied. Every external adopter would need to reverse-engineer the test expectations from fixture files and spec prose.

## Scope

In scope:

- Design and publish a standalone conformance test suite repository (or publishable package within the spec repo, with clear extraction path to separate repo).
- Language-agnostic test fixtures with machine-readable expected results.
- CLI conformance runner (reference implementation in TypeScript/Node).
- Machine-readable conformance report format (JSON).
- Badge/status mechanism for implementations to display conformance level.
- v0.1 and v0.2 conformance levels.
- Documentation for adopters on how to integrate the suite.

Out of scope:

- Building conformance runners in every language (adopters do this).
- Hosting a conformance certification service (post-1.0).
- Changing normative spec semantics.

## Execution phases

### Phase 1 — Test fixture packaging and expected-results manifest

- [ ] Create a `conformance/` directory structure (or standalone repo scaffold):
  ```
  conformance/
    v0.1/
      valid/          # symlinked or copied from examples/v0.1/
      invalid/        # symlinked or copied from examples/v0.1/invalid/
      expected.json   # machine-readable expected results per fixture
    v0.2/
      valid/
      invalid/
      expected.json
    README.md         # adopter-facing usage instructions
    schema/
      conformance-report.schema.json  # report format schema
  ```
- [ ] Define `expected.json` format: for each fixture file, specify:
  - `filename`: relative path
  - `expectedResult`: `"accept"` or `"reject"`
  - `reason`: human-readable explanation of what is being tested
  - `category`: e.g., `"required-fields"`, `"ttl"`, `"signature"`, `"adversarial"`
  - `specVersion`: `"0.1"` or `"0.2"`
  - `conformanceLevel`: `"baseline"` or `"extended"` (e.g., revocation-aware)

### Phase 2 — CLI conformance runner (reference)

- [ ] Build a CLI tool that:
  - Takes a path to an implementation's "adapter" (stdin/stdout protocol or HTTP endpoint).
  - Feeds each fixture to the adapter.
  - Collects accept/reject results.
  - Compares against `expected.json`.
  - Produces a conformance report.
- [ ] Adapter protocol specification:
  - Input: JSON fixture on stdin (or HTTP POST body).
  - Output: JSON result on stdout (or HTTP response):
    ```json
    {
      "fixture": "v0.1/invalid/missing-context.jsonld",
      "result": "reject",
      "reason": "missing @context field"
    }
    ```
- [ ] Reference adapter wrapping the existing `packages/universal-manifest` validator.

### Phase 3 — Machine-readable conformance report format

- [ ] Define `conformance-report.schema.json`:
  ```json
  {
    "implementation": {
      "name": "my-um-validator",
      "version": "1.0.0",
      "language": "python",
      "organization": "Acme Corp",
      "repository": "https://github.com/acme/my-um-validator"
    },
    "specVersionsTested": ["0.1", "0.2"],
    "testDate": "2026-03-15T10:00:00Z",
    "suiteVersion": "1.0.0",
    "results": {
      "v0.1": {
        "total": 20,
        "passed": 20,
        "failed": 0,
        "skipped": 0,
        "details": [...]
      }
    },
    "conformanceLevel": "v0.1-baseline",
    "pass": true
  }
  ```
- [ ] Validate the report schema against the runner output.

### Phase 4 — Badge and status mechanism

- [ ] Define conformance levels:
  - `v0.1-baseline`: passes all v0.1 valid + invalid fixtures
  - `v0.2-baseline`: passes all v0.2 valid + invalid fixtures (includes signature verification)
  - `v0.2-extended`: passes v0.2 baseline + revocation-aware fixtures
- [ ] Create badge SVG templates for each level.
- [ ] Define a `conformance-status.json` file format implementations can host:
  ```json
  {
    "implementation": "my-um-validator",
    "conformanceLevels": ["v0.1-baseline", "v0.2-baseline"],
    "lastTested": "2026-03-15T10:00:00Z",
    "suiteVersion": "1.0.0",
    "reportUrl": "https://..."
  }
  ```
- [ ] Document how to generate and display badges.

### Phase 5 — Documentation and adopter instructions

- [ ] Write adopter-facing README for the conformance suite.
- [ ] Include step-by-step instructions for:
  - Running the suite against a new implementation.
  - Building a custom adapter for any language.
  - Generating and submitting a conformance report.
- [ ] Add a "Getting Started with Conformance Testing" section to the main UM docs site.

## Key file paths (created/modified)

New files:
- `/Users/grig/work/repo/universalmanifest/conformance/README.md`
- `/Users/grig/work/repo/universalmanifest/conformance/v0.1/expected.json`
- `/Users/grig/work/repo/universalmanifest/conformance/v0.2/expected.json`
- `/Users/grig/work/repo/universalmanifest/conformance/schema/conformance-report.schema.json`
- `/Users/grig/work/repo/universalmanifest/conformance/schema/conformance-status.schema.json`
- `/Users/grig/work/repo/universalmanifest/conformance/runner/` (CLI tool)
- `/Users/grig/work/repo/universalmanifest/conformance/adapters/typescript/` (reference adapter)
- `/Users/grig/work/repo/universalmanifest/conformance/badges/` (SVG templates)

Modified files:
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/` (new conformance testing docs page)
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`

## Acceptance criteria

- [ ] All existing v0.1 fixtures (valid + invalid) are packaged with machine-readable expected results in `expected.json`.
- [ ] All existing v0.2 fixtures (valid + invalid) are packaged with machine-readable expected results in `expected.json`.
- [ ] CLI conformance runner can execute against the reference TypeScript adapter and produce a passing report.
- [ ] Conformance report JSON validates against `conformance-report.schema.json`.
- [ ] An adopter can clone the conformance suite, build a simple adapter in a non-TypeScript language, and run the suite without reading spec repo internals.
- [ ] Badge SVGs exist for each conformance level.
- [ ] Adopter-facing documentation is clear enough for an AI agent or developer to follow without additional context.
- [ ] Suite version is tracked and can be bumped independently of spec versions.

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/conformance/runner && npm test`
- `cd /Users/grig/work/repo/universalmanifest/conformance/runner && node cli.mjs --adapter ../adapters/typescript/ --report report.json`
- JSON schema validation of generated report against `conformance-report.schema.json`
- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`

## Dependencies and sequencing notes

- This is the foundational work order in the adopter verification wave. WO-0054, WO-0055, and WO-0056 all depend on this.
- Coordinate with WO-0057 to ensure conformance docs clearly distinguish spec from implementation.
- Fixtures from `examples/v0.1/` and `examples/v0.2/` are the source of truth; conformance suite references them (symlink or copy with sync mechanism).
