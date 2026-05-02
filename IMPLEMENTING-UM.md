# Implementing Universal Manifest

This document is the **adopter-facing** entry point for building a conformant Universal Manifest implementation. It assumes you have read the spec (`spec/v0.1/README.md`, `spec/v0.2/README.md`) and now want to ship code.

You have two paths:

- **Path A — Fork the TypeScript reference implementation.** Start from a working artifact, replace internals to match your runtime. Fastest to a green conformance run.
- **Path B — Build from scratch in any language.** Use the published spec artifacts and the standalone conformance suite as the only inputs. No language constraint.

Both paths converge on the same gate: **a passing conformance report against the spec repo's standalone suite.**

---

## Reference implementation #1

`https://github.com/grigb/um-typescript` (npm: `@universalmanifest/typescript`)

This is the spec maintainer's TypeScript reference. It is treated as **implementation #1**, not "the official implementation." Multiple implementations from multiple organizations are the goal (Gate G4 — Interoperability proof).

The spec repo's CI exercises this implementation against the spec contract on every PR via `.github/workflows/um-typescript-conformance.yml` and writes weekly conformance reports under `docs/reports/`. If the reference impl drifts from the contract, the spec repo's PR builds fail loudly.

---

## Path A — Fork-and-conform

### 1. Fork

Click "Fork" on `https://github.com/grigb/um-typescript`, or:

```bash
gh repo fork grigb/um-typescript --clone --remote
cd um-typescript
```

### 2. Adapt internals to your runtime

The repository is intentionally small. The shape you must preserve is the public API surface (so the conformance adapter keeps working):

```
src/
  index.ts          # public exports: create, validate, sign, verify, resolve
  manifest.ts       # create + structural validation
  signer.ts         # JCS canonicalization + Ed25519 signing
  verifier.ts       # signature verification
  resolver.ts       # HTTP UMID resolution client (default: myum.net)
  types.ts          # v0.1 + v0.2 type definitions
tests/
  conformance/
    adapter.mjs           # contract-mode adapter — KEEP COMPATIBLE
    run-conformance.mjs   # wrapper that points at conformance suite
  unit/                   # your implementation-specific tests
```

You MAY rewrite any internal file. You MUST keep:

- `src/index.ts` exports (`create`, `validate`, `sign`, `verify`, `resolve`).
- `tests/conformance/adapter.mjs` invocation contract (stdin/stdout JSON-RPC-ish handshake the standalone runner expects).

### 3. Run conformance against the spec

The fastest path is to point the bundled wrapper at the spec repo's authoritative fixture matrix:

```bash
git clone https://github.com/grigb/universal-manifest.git ../universalmanifest
UM_CONFORMANCE_ROOT=../universalmanifest/conformance npm run conformance
```

A successful run writes `tests/conformance/conformance-report.json`. Attach this to your release or publish under `<your-repo>/docs/reports/`.

### 4. Wire CI

Copy `.github/workflows/conformance.yml` from the upstream `um-typescript` repository into your fork. Update the schedule cron and the `UM_CONFORMANCE_ROOT` resolution if your CI environment differs.

### 5. Declare conformance

Add a `Conformance` section to your README pointing to your latest report. Optionally consume one of the published badges from `https://github.com/grigb/universal-manifest/tree/main/conformance/badges`.

---

## Path B — Build from scratch (any language)

Conformance is **language-agnostic**. The spec repo treats the standalone conformance suite as the contract.

### 1. Read the spec

- `spec/v0.1/README.md` and `spec/v0.1/CONFORMANCE.md`
- `spec/v0.2/README.md`, `spec/v0.2/CONFORMANCE.md`, `spec/v0.2/SIGNATURE-PROFILE.md`
- `services/myum-resolver/CONTRACT.md` (if you are also building a resolver)

### 2. Implement against the fixture matrix

Pull `examples/v0.1/` and `examples/v0.2/`. These are the manifests every conformant implementation MUST round-trip correctly. Invalid fixtures under `examples/v0.{1,2}/invalid/` MUST be rejected.

### 3. Build a conformance adapter

The standalone runner (`conformance/runner/cli.mjs`) speaks two adapter modes:

- **Command mode** — the runner spawns your adapter as a subprocess and exchanges JSON over stdin/stdout. See `conformance/adapters/typescript/adapter.mjs` for the canonical example.
- **HTTP mode** — your adapter exposes an HTTP endpoint (e.g., `POST /validate`). Useful when your impl is in a language whose subprocess spawning is awkward from Node.

Either is acceptable. Once your adapter handshakes correctly, run:

```bash
cd <spec-repo>/conformance/runner
node ./cli.mjs \
  --mode command \
  --adapter-command "<command to launch your adapter>" \
  --versions 0.1,0.2 \
  --baseline \
  --report ./conformance-report-<your-impl>.json
```

### 4. Wire CI

Run the conformance suite on every PR in your repo. The grade-A pattern is:

- PR job — runs full conformance, fails the build on any regression.
- Weekly scheduled job — re-runs against the spec repo's `main` branch (so you catch upstream contract changes within seven days).

Mirror `.github/workflows/um-typescript-conformance.yml` from the spec repo as a template.

### 5. (Optional) Build a resolver

If your implementation includes a UMID resolver (an HTTP server that returns manifests by UMID), it MUST satisfy:

- `services/myum-resolver/CONTRACT.md` — the public contract.
- `docs/journeys/journey-04b-umid-resolution-resolver-agnostic.md` — the resolver-agnostic conformance journey. This journey can be pointed at any HTTP base URL.

Run J04b against your resolver:

```bash
UM_RESOLVER_BASE_URL=https://your-resolver.example \
  npm --prefix services/myum-resolver run test:contract -- --base-url=$UM_RESOLVER_BASE_URL
```

The Cloudflare-targeted J04 (`docs/journeys/journey-04-umid-resolution-myum.md`) is preserved for the spec repo's own runtime; new resolver implementations should target J04b.

---

## Get listed as a reference implementation

The spec repo's README has a "Reference implementations" section. To get listed:

1. Open a PR against `https://github.com/grigb/universal-manifest` modifying `README.md`.
2. Include:
   - Repository URL.
   - Language and runtime.
   - Latest passing `conformance-report.json` (link or attach).
   - Maintainer contact.
3. The spec maintainer reviews — pass conformance + active maintenance + permissive license = listed.

Listing is editorial, not adversarial. The point is to lower the bar for adopters discovering your implementation, not to gatekeep.

---

## Frequently asked questions

**Q: Do I have to use TypeScript?**
No. Path B explicitly exists for any language. The reference impl just happens to be in TypeScript because the spec maintainer wrote it.

**Q: Can I use the standalone runner from my own language?**
Yes. The runner is Node.js, but it talks to your adapter over a process boundary (command or HTTP). Your adapter can be Go, Rust, Python, anything that can read stdin and write stdout (or serve HTTP).

**Q: How do I know my implementation is in sync with the spec?**
Run conformance against the spec repo's `main` branch on a weekly schedule. The `um-typescript` reference implementation does this (see `.github/workflows/conformance.yml` in that repo); the spec repo's own `.github/workflows/um-typescript-conformance.yml` does the inverse — it tests `um-typescript@main` against the spec on every PR. Two-way drift catching.

**Q: What is "drift"?**
Spec and implementation getting out of sync without anyone noticing. WO-0217 (which created this document) was specifically about wiring drift detection so the spec maintainer learns about a regression in seven days, not at adopter-complaint time.

**Q: Can I publish my implementation under a different package name?**
Yes. The reference impl uses `@universalmanifest/typescript` (a maintainer-controlled scope); you publish under your own scope.

---

## See also

- `README.md` — top-level project README, "Reference implementations" section.
- `site/src/content/docs/for-agents.md` — agent-discovery entry, lists reference implementations for machine consumption.
- `docs/journeys/journey-04b-umid-resolution-resolver-agnostic.md` — resolver-agnostic conformance journey.
- `services/myum-resolver/CONTRACT.md` — resolver public contract.
- `conformance/runner/README.md` — standalone conformance runner usage.
- `docs/workorders/WO-0054-reference-implementation-repository-typescript.md` — origin WO for the reference impl.
- `docs/workorders/WO-0217-integrate-reference-typescript-impl-into-spec-repo-ci.md` — origin WO for this doc and the conformance workflow.
