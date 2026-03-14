# WO-0044 — Public open-source examples and demos work stream

**Status:** COMPLETED
**Created:** 2026-02-25
**Priority:** HIGH
**Type:** Work stream (multi-phase)

## Vision

When this work stream is complete, a developer who finds Universal Manifest on GitHub should be able to:

1. Run a working code example within 5 minutes of cloning the repo.
2. See concrete, real-world use cases implemented end-to-end, not just JSON fixtures.
3. Understand how to create, validate, sign, resolve, and consume manifests using actual code.
4. Find integration examples for their platform of interest (social, IoT, AR/VR, identity).
5. Copy and adapt a working starter project for their own system.

The examples ecosystem should serve as **proof that Universal Manifest works**, not just documentation that says it works.

## Current state assessment

### What exists now

The project has a solid foundation of **static fixtures** and **internal proof tooling**, but lacks developer-facing runnable examples:

**Fixtures (JSON-LD files only, no runnable code):**
- 4 valid v0.1 manifests: `examples/v0.1/minimal-manifest.jsonld`, `manifest-with-facets.jsonld`, `type-array-manifest.jsonld`, `unknown-fields-manifest.jsonld`
- 16 near-real stub manifests under `examples/v0.1/stubs/` (social, venue, device, OMATrust, metaverse, AR, Chia, personhood, etc.)
- 11 invalid v0.1 fixtures under `examples/v0.1/invalid/`
- 1 valid v0.2 signed manifest: `examples/v0.2/minimal-signed-manifest.jsonld`
- 8 invalid v0.2 fixtures under `examples/v0.2/invalid/`

**TypeScript helper package (`packages/universal-manifest/`):**
- Exports type definitions (`UniversalManifestV01`, `UniversalManifestV02`, facet/signature types)
- Exports assertion functions (`assertUniversalManifestV01`, `assertUniversalManifestV01Fresh`, v0.2 variants)
- Exports `getManifestId` helper
- Includes JCS canonicalization and Ed25519 signature verification for v0.2
- Has a validation script (`scripts/validate-examples.mjs`) that runs against all fixtures
- Has a journey runner (`scripts/run-journeys.mjs`) with 11 executable proof journeys
- Package is `private: true` and not published to npm

**Resolver skeleton (`services/myum-resolver/`):**
- Cloudflare Worker with KV-backed resolution
- Endpoints: `/health`, `/.well-known/myum-resolver.json`, `/{UMID_PATH}`
- Supports `b64u:` encoded UMIDs, ETag/304, redirect records, revocation
- Has one hardcoded dev fixture for testing

**Interactive tools (browser-based):**
- Harness: loads and displays fixture examples at `/harness/index.html`
- Workbench: browser-based create/edit/validate/export tool

**Integration guidance (prose only, no code):**
- 9 integration docs covering social, Chia, OMATrust, metaverse, RP1, smart-glasses, proof-of-personhood, reference runtime, runtime profile

### What is missing

1. **No runnable code examples.** Every example is a static `.jsonld` file. There is no code a developer can run that shows how to create a manifest programmatically, validate one, check its TTL, or verify a signature.

2. **No "hello world" script.** The quick-start guide tells developers what to implement but does not give them a single file they can execute.

3. **No SDK usage examples.** The TS helper package exists but has no usage examples outside of internal validation scripts. A developer looking at `packages/universal-manifest/` would not know how to use it in their own project.

4. **No integration demos with code.** Integration docs describe concepts but include no working code. A developer interested in, e.g., social profile projection or Chia VC integration has no code to start from.

5. **No end-to-end demo application.** There is no complete working app that shows the full lifecycle: create manifest, publish to resolver, fetch by UMID, validate, display.

6. **No resolver interaction examples.** The resolver contract is documented, but there is no example code showing how to publish a manifest to KV or fetch one via the API.

7. **No multi-language examples.** Everything is TypeScript/Node.js. There are no examples for Python, Go, Rust, or browser JavaScript.

## Proposed repo structure

```
examples/
  v0.1/                              # (existing) static JSON-LD fixtures
  v0.2/                              # (existing) static JSON-LD fixtures
  code/                              # NEW: runnable code examples
    01-hello-world/                   # simplest possible example
      create-manifest.mjs
      validate-manifest.mjs
      README.md
    02-validate-and-check-ttl/
      validate-with-ttl.mjs
      README.md
    03-create-signed-manifest-v02/
      sign-manifest.mjs
      verify-manifest.mjs
      README.md
    04-facets-and-pointers/
      compose-manifest-with-facets.mjs
      read-specific-facets.mjs
      README.md
    05-resolve-from-myum/
      publish-to-resolver.mjs
      fetch-by-umid.mjs
      README.md
    06-social-profile-projection/
      create-social-manifest.mjs
      project-to-web-profile.mjs
      README.md
    07-device-registration/
      register-device.mjs
      check-device-enrollment.mjs
      README.md
    08-consent-enforcement/
      create-consent-manifest.mjs
      enforce-consent-rules.mjs
      README.md
    09-unknown-field-tolerance/
      forward-compatible-consumer.mjs
      README.md
    10-multi-manifest-aggregation/
      aggregate-manifests.mjs
      README.md
```

### Naming conventions

- Directory names: `NN-short-description/` where NN is a zero-padded sequence number
- Script files: `verb-noun.mjs` (e.g., `create-manifest.mjs`, `validate-manifest.mjs`)
- Each example directory has its own `README.md` explaining what it demonstrates, how to run it, and what to expect
- All examples use ESM (`*.mjs`) and require only Node.js 18+ with no extra dependencies beyond the TS helper package (where applicable)
- Examples that do not use the TS helper package demonstrate that adoption does not require it

## Phased execution plan

### Phase 1: Quick wins (beginner examples, runnable in minutes)

**Goal:** A developer can clone the repo, run a script, and see Universal Manifest working within 5 minutes.

**Timeline:** Single agent session per example.

| # | Example | What it demonstrates | Complexity | Dependencies |
|---|---------|---------------------|-----------|--------------|
| 1 | `01-hello-world` | Create a minimal v0.1 manifest from scratch in plain JS (no library), print it, validate required fields manually | Beginner | None |
| 2 | `02-validate-and-check-ttl` | Load a fixture, validate it using the TS helper `assertUniversalManifestV01`, check TTL freshness with `assertUniversalManifestV01Fresh`, show what happens with expired manifests | Beginner | TS helper built (`npm run build` in `packages/universal-manifest/`) |
| 3 | `04-facets-and-pointers` | Build a manifest with multiple facets and pointers, then show a consumer reading only the facets it understands and ignoring the rest | Beginner | None |
| 4 | `09-unknown-field-tolerance` | Show a consumer receiving a manifest with fields it does not recognize, proving it processes safely without errors | Beginner | None |

**Deliverables per example:**
- `*.mjs` script(s) that run with `node <script>.mjs`
- `README.md` with: what it demonstrates, prerequisites, how to run, expected output, key takeaways
- No external dependencies beyond Node.js and (optionally) the built TS helper

### Phase 2: Intermediate examples (SDK usage, signatures, resolver)

**Goal:** Developers see how to use the TypeScript helper package and interact with the resolver.

| # | Example | What it demonstrates | Complexity | Dependencies |
|---|---------|---------------------|-----------|--------------|
| 5 | `03-create-signed-manifest-v02` | Generate an Ed25519 keypair, create a v0.2 manifest, sign it using JCS canonicalization, verify the signature using `assertUniversalManifestV02` | Intermediate | TS helper, Node.js crypto |
| 6 | `05-resolve-from-myum` | Publish a manifest to the local resolver (via direct KV simulation or HTTP), then fetch it by UMID, demonstrate ETag caching and 304 responses | Intermediate | Resolver running locally |
| 7 | `08-consent-enforcement` | Create manifests with consent declarations, implement a consumer that checks consent before rendering profile data or sharing information | Intermediate | None |
| 8 | `10-multi-manifest-aggregation` | Fetch multiple manifests for different subjects, aggregate/merge facet data into a unified view (e.g., a venue display combining creator + venue + device manifests) | Intermediate | TS helper |

**Deliverables per example:**
- Same as Phase 1, plus inline comments explaining each step
- Where resolver interaction is needed, include instructions for starting the local dev server

### Phase 3: Integration demos and end-to-end applications

**Goal:** Show Universal Manifest in realistic integration contexts with complete working code.

| # | Example | What it demonstrates | Complexity | Dependencies |
|---|---------|---------------------|-----------|--------------|
| 9 | `06-social-profile-projection` | Create a social profile manifest with `schema:Person` facets, ActivityPub pointers, and profile consent; implement a projection that renders an HTML profile page from the manifest | Intermediate | None |
| 10 | `07-device-registration` | Create a device manifest with hardware metadata, enrollment status, and trust level; show a venue system accepting or rejecting the device based on manifest claims | Intermediate | None |
| 11 | End-to-end demo app (new directory: `examples/demo-app/`) | A complete Node.js application that: (a) creates manifests for a creator and a venue, (b) publishes them to a local resolver, (c) fetches them by UMID, (d) validates and checks TTL, (e) renders a simple web page showing the resolved data | Advanced | TS helper, resolver |

**Deliverables for demo app:**
- Self-contained Node.js project with `package.json`
- Single `npm start` command to run
- Serves a local web page showing resolved manifest data
- README with architecture diagram (text-based), setup instructions, and walkthrough

### Phase 4: Breadth and community framework

**Goal:** Expand language coverage and make it easy for contributors to add new examples.

| # | Example | What it demonstrates | Complexity | Dependencies |
|---|---------|---------------------|-----------|--------------|
| 12 | Python validation example | Validate a UM manifest using only Python stdlib (json module), enforce TTL, ignore unknown fields | Beginner | Python 3.8+ |
| 13 | Browser JavaScript example | Load and validate a manifest entirely in the browser using fetch + manual validation (no Node.js) | Beginner | None (static HTML file) |
| 14 | Contribution guide for examples | Template and guidelines for adding new examples: directory structure, README format, testing requirements, review checklist | N/A | Phase 1-3 complete |

## Detailed example proposals

### Example 1: Hello World (`01-hello-world`)

**What it demonstrates:** The absolute minimum a developer needs to understand: how to construct a valid v0.1 manifest from scratch using plain JavaScript with no libraries.

**Files created:**
- `examples/code/01-hello-world/create-manifest.mjs` — Constructs a manifest object with all required fields, generates a UUID for `@id`, sets `issuedAt` to now and `expiresAt` to 1 hour from now, prints the result as formatted JSON.
- `examples/code/01-hello-world/validate-manifest.mjs` — Reads a manifest from stdin or a file path argument, checks all 7 required fields exist and have correct types, checks `issuedAt <= expiresAt`, prints PASS/FAIL with details.
- `examples/code/01-hello-world/README.md`

**How to run:**
```bash
cd examples/code/01-hello-world
node create-manifest.mjs
node create-manifest.mjs | node validate-manifest.mjs
```

**Key takeaway:** A Universal Manifest is just a JSON-LD document with 7 required fields. You do not need any special library to create one.

### Example 2: Validate and check TTL (`02-validate-and-check-ttl`)

**What it demonstrates:** Using the official TS helper package to validate manifests structurally and check TTL freshness. Shows the difference between structural validation (is this a well-formed manifest?) and freshness validation (is this manifest still valid right now?).

**Files created:**
- `examples/code/02-validate-and-check-ttl/validate-with-ttl.mjs` — Imports `assertUniversalManifestV01` and `assertUniversalManifestV01Fresh` from the built helper package; loads a valid fixture and a freshly created manifest; validates both; demonstrates what happens when a manifest is expired.
- `examples/code/02-validate-and-check-ttl/README.md`

**How to run:**
```bash
cd packages/universal-manifest && npm run build
cd ../../examples/code/02-validate-and-check-ttl
node validate-with-ttl.mjs
```

**Key takeaway:** Consumers MUST check TTL before acting on a manifest. The helper package provides both structural and freshness assertions.

### Example 3: Create and verify a signed manifest (`03-create-signed-manifest-v02`)

**What it demonstrates:** The complete v0.2 signature lifecycle: key generation, manifest construction, JCS canonicalization, Ed25519 signing, and verification using the TS helper.

**Files created:**
- `examples/code/03-create-signed-manifest-v02/sign-manifest.mjs` — Generates an Ed25519 keypair using Node.js `crypto`, constructs a v0.2 manifest without a signature, canonicalizes it using JCS (RFC 8785), signs the canonical form, attaches the signature block, outputs the signed manifest.
- `examples/code/03-create-signed-manifest-v02/verify-manifest.mjs` — Reads a signed v0.2 manifest, calls `assertUniversalManifestV02` which performs structural validation AND signature verification, prints the result.
- `examples/code/03-create-signed-manifest-v02/README.md`

**How to run:**
```bash
node sign-manifest.mjs > signed.jsonld
node verify-manifest.mjs signed.jsonld
```

**Key takeaway:** v0.2 adds cryptographic integrity. The signature is computed over the JCS-canonicalized manifest (excluding the signature block itself).

### Example 4: Facets and pointers (`04-facets-and-pointers`)

**What it demonstrates:** How to compose a manifest using facets (embedded data sections) and pointers (references to authoritative sources). Shows a consumer selectively reading only relevant facets.

**Files created:**
- `examples/code/04-facets-and-pointers/compose-manifest-with-facets.mjs` — Creates a manifest with a `publicProfile` facet, a `deviceRegistration` facet, and two pointers; prints the complete manifest.
- `examples/code/04-facets-and-pointers/read-specific-facets.mjs` — Reads a manifest, extracts only the `publicProfile` facet (simulating a social app), ignores other facets; then extracts only the `deviceRegistration` facet (simulating a device management system), ignores other facets; demonstrates selective consumption.
- `examples/code/04-facets-and-pointers/README.md`

**Key takeaway:** Different systems read different parts of the same manifest. Facets are embedded data; pointers are references to data that lives elsewhere.

### Example 5: Resolve from myum.net (`05-resolve-from-myum`)

**What it demonstrates:** The resolver lifecycle: how to interact with a `myum.net`-compatible resolver to fetch manifests by UMID. Demonstrates HTTP caching with ETag/304.

**Files created:**
- `examples/code/05-resolve-from-myum/fetch-by-umid.mjs` — Fetches the dev fixture from `http://127.0.0.1:8787/{UMID}` (or the production resolver), validates the response, demonstrates ETag-based conditional requests (second fetch returns 304).
- `examples/code/05-resolve-from-myum/README.md`

**Prerequisites:** Local resolver running (`cd services/myum-resolver && npm run dev`).

**Key takeaway:** The resolver is a simple HTTP GET endpoint. Consumers use standard HTTP caching (ETag/If-None-Match) and MUST still enforce the manifest's own TTL (`expiresAt`).

### Example 6: Social profile projection (`06-social-profile-projection`)

**What it demonstrates:** A realistic integration scenario where a social platform consumes a Universal Manifest and projects it into a public profile view.

**Files created:**
- `examples/code/06-social-profile-projection/create-social-manifest.mjs` — Creates a social profile manifest with `schema:Person` facets, ActivityPub pointer, and consent declarations.
- `examples/code/06-social-profile-projection/project-to-web-profile.mjs` — Reads a social manifest, checks the `social.profilePublic` consent, extracts profile fields from facets, generates a simple HTML profile page and writes it to `output/profile.html`.
- `examples/code/06-social-profile-projection/README.md`

**Key takeaway:** The manifest is a container for portable identity state. A social platform reads only the parts it needs and respects consent declarations before rendering.

### Example 7: Device registration (`07-device-registration`)

**What it demonstrates:** How a venue system uses manifests to register and manage display devices, check enrollment status, and enforce trust levels.

**Files created:**
- `examples/code/07-device-registration/register-device.mjs` — Creates a venue manifest with device registration facets, enrollment timestamps, and hardware metadata.
- `examples/code/07-device-registration/check-device-enrollment.mjs` — Reads a venue manifest, looks up a device by `deviceDid`, checks enrollment status and trust level, prints whether the device would be accepted or rejected by the venue.
- `examples/code/07-device-registration/README.md`

**Key takeaway:** Manifests carry device metadata alongside identity and policy information. The venue system acts as a consumer that validates the manifest and applies its own trust rules.

### Example 8: Consent enforcement (`08-consent-enforcement`)

**What it demonstrates:** How a consumer checks consent declarations in a manifest before performing sensitive actions (rendering a public profile, indexing content, sharing data).

**Files created:**
- `examples/code/08-consent-enforcement/create-consent-manifest.mjs` — Creates a manifest with explicit consent declarations (allowed and denied).
- `examples/code/08-consent-enforcement/enforce-consent-rules.mjs` — Implements a consent-checking consumer that reads consent keys, defaults to deny when a consent is absent, and gates actions behind consent checks.
- `examples/code/08-consent-enforcement/README.md`

**Key takeaway:** Consumers must default to deny for any action not explicitly consented to. The manifest carries the subject's permissions as portable state.

### Example 9: Unknown field tolerance (`09-unknown-field-tolerance`)

**What it demonstrates:** The forward-compatibility guarantee: a v0.1 consumer safely processes a manifest that contains fields from a hypothetical future version.

**Files created:**
- `examples/code/09-unknown-field-tolerance/forward-compatible-consumer.mjs` — Loads a manifest with extra unknown fields (simulating a newer spec version), validates required fields, processes known fields, explicitly demonstrates that unknown fields do not cause errors or data loss.
- `examples/code/09-unknown-field-tolerance/README.md`

**Key takeaway:** Unknown field tolerance is what makes Universal Manifest forward-compatible. This is a hard requirement, not a suggestion.

### Example 10: Multi-manifest aggregation (`10-multi-manifest-aggregation`)

**What it demonstrates:** A venue display system that fetches manifests from multiple subjects (creator, venue, device) and aggregates them into a unified view.

**Files created:**
- `examples/code/10-multi-manifest-aggregation/aggregate-manifests.mjs` — Loads three manifests (venue, creator, device), validates each, extracts relevant facets from each, combines them into a display-ready data structure, prints the aggregated view.
- `examples/code/10-multi-manifest-aggregation/README.md`

**Key takeaway:** In a multi-party environment, each participant provides their own manifest. The consuming system aggregates data from multiple manifests to build a complete picture.

## Success criteria

### Developer experience

- [ ] A developer can clone the repo and run `node examples/code/01-hello-world/create-manifest.mjs` with no setup beyond Node.js 18+.
- [ ] Each example produces meaningful, self-explanatory console output (not just "OK" or silence).
- [ ] Each example's README answers: what is this, what does it demonstrate, how do I run it, what should I see, what should I learn.
- [ ] No example requires npm install (except those that explicitly use the TS helper package, where the install step is documented).

### Coverage

- [ ] At least one example covers each core concept: UMID, TTL, unknown field tolerance, facets, pointers.
- [ ] At least one example shows the v0.2 signature lifecycle (create, sign, verify).
- [ ] At least one example demonstrates resolver interaction.
- [ ] At least one example shows a realistic integration scenario (not just validation).
- [ ] At least one example demonstrates consent enforcement.

### Quality

- [ ] Every `*.mjs` file runs without errors on Node.js 18+ (tested by `node <file>`).
- [ ] Every example that uses fixture files includes the fixture or creates it programmatically (no dangling references).
- [ ] Console output from each example is clear enough to understand without reading the code.
- [ ] Examples do not duplicate the TS helper's internal logic unnecessarily; they import and use the package where appropriate.

### Integration with existing project

- [ ] The site's quick-start guide links to the code examples.
- [ ] The concepts page references relevant examples for each concept.
- [ ] The stub manifests page links to code examples that use those stubs.
- [ ] The TS helper README references examples that demonstrate its API.

## Dependencies and sequencing

**Phase 1 depends on:**
- Nothing. All Phase 1 examples use only Node.js stdlib and/or existing fixtures.

**Phase 2 depends on:**
- TS helper package buildable (`packages/universal-manifest/` must `npm run build` successfully). Already true.
- For resolver examples: local resolver dev server must be startable. Already true.

**Phase 3 depends on:**
- Phase 1 and Phase 2 complete (so integration examples can reference simpler examples for prerequisites).

**Phase 4 depends on:**
- Phase 1-3 patterns established (so the contribution guide reflects actual conventions).

## Validation commands

After each phase, run:

```bash
# Verify all example scripts execute without errors
for f in $(find examples/code -name '*.mjs' -not -path '*/node_modules/*'); do
  echo "Running: $f"
  node "$f" || echo "FAILED: $f"
done

# Existing test suite still passes
cd packages/universal-manifest && npm test

# Site build still passes
cd site && npm run build:clean
```

## Relationship to existing work orders

- **WO-0005** (TS helper package): Phase 2 examples exercise the helper API and provide evidence of its usability.
- **WO-0012** (user journeys): The existing journey runner is internal proof tooling. These examples serve a different audience (external developers) but the journeys provide patterns to draw from.
- **WO-0014** (workbench): The browser-based workbench is complementary; these examples are code-first rather than GUI-first.
- **WO-0039** (onboarding rewrite): The quick-start guide should link to these examples once they exist.

## Notes

- Examples should be buildable by an agent in a single session. Each Phase 1 example is scoped to produce 2-3 files.
- All examples use `.mjs` (ES modules) for consistency and to avoid TypeScript compilation steps in the examples themselves.
- The TS helper package import path in examples should use a relative path to the built package (e.g., `../../../packages/universal-manifest/dist/index.js`) rather than requiring npm publication.
- Examples should not contain placeholder signatures (`BASE64URL_SIGNATURE_PLACEHOLDER`). Either generate real signatures (v0.2 examples) or use v0.1 (where signature is optional).

## Execution Evidence

### Phase 1 (Beginner) — COMPLETED 2026-02-26

All 4 examples created and verified:

- `examples/code/01-hello-world/` — create-manifest.mjs, validate-manifest.mjs, README.md
- `examples/code/02-validate-and-check-ttl/` — validate-with-ttl.mjs, README.md
- `examples/code/04-facets-and-pointers/` — compose-manifest-with-facets.mjs, read-specific-facets.mjs, README.md
- `examples/code/09-unknown-field-tolerance/` — forward-compatible-consumer.mjs, README.md

### Phase 2 (Intermediate) — COMPLETED 2026-02-26

All 4 examples created and verified:

- `examples/code/03-create-signed-manifest-v02/` — sign-manifest.mjs, verify-manifest.mjs, README.md
- `examples/code/05-resolve-from-myum/` — fetch-by-umid.mjs, README.md
- `examples/code/08-consent-enforcement/` — create-consent-manifest.mjs, enforce-consent-rules.mjs, README.md
- `examples/code/10-multi-manifest-aggregation/` — aggregate-manifests.mjs, README.md

### Phase 3 (Integration) — COMPLETED 2026-02-26

All 3 deliverables created and verified:

- `examples/code/06-social-profile-projection/` — create-social-manifest.mjs, project-to-web-profile.mjs, README.md
- `examples/code/07-device-registration/` — register-device.mjs, check-device-enrollment.mjs, README.md
- `examples/demo-app/` — Full lifecycle demo (server.mjs + lib/, package.json, README.md)

### Phase 4 (Breadth) — COMPLETED 2026-02-26

- `examples/code/python-validate/` — Python 3.8+ validation (stdlib only)
- `examples/code/browser-validate/` — Browser-native validation (single HTML file)
- `examples/code/CONTRIBUTING.md` — Contribution guide for new examples

### Verification sweep

- All 10 numbered examples: PASS (exit code 0)
- Piped workflows: PASS
- Existing test suite: PASS (21 valid, 19 invalid, 0 failures)
- Demo app: PASS (lifecycle completes, dashboard renders)

### Integration

- examples/code/README.md — Index of all examples
- packages/universal-manifest/README.md — Updated with example links
- README.md (project root) — Updated with code examples section
- Quick-start guide — Updated with example links
