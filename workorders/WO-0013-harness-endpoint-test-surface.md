# WO-0013 — Harness endpoint test surface (docs + resolver)

**Status:** COMPLETED  
**Created:** 2026-02-17

## Objective

Make the Universal Manifest harness a **real pass/fail test surface** that:

- runs in the `universalmanifest.net` static site output
- calls real backend endpoints (at least the resolver skeleton)
- can be used for quick manual debugging and for agent-browser verification

This does **not** replace the executable proof suite (`npm run journeys`). It complements it.

## Scope

In scope:

- Add a `site/public/harness/` UI that works in `astro dev` and in static deploy output.
- Sync a minimal set of fixtures into the site so the harness can load “near-real” examples.
- Extend harness to test:
  - resolver `/health`
  - resolver `/.well-known/myum-resolver.json`
  - resolver `GET /{UMID}` resolution for a known UMID
  - basic manifest validation + optional signature verification (when possible)
- Add minimal “autorun” support (query string) so automated browser checks can screenshot a completed test run.

Out of scope:

- Full conformance suite in the browser (that remains the journeys runner).
- Write endpoints for production resolver (writes are not part of the public contract).
- DID key resolution (browser verifier uses `publicKeySpkiB64` only).

## Deliverables

- Harness UI:
  - `site/public/harness/index.html`
- Fixture copies (generated/synced):
  - `site/public/harness/fixtures/v0.1/stubs/*.jsonld`
  - `site/public/harness/fixtures/v0.2/minimal-signed-manifest.jsonld`
- Doc link/update:
  - `site/src/content/docs/proof/harness.md`
- Resolver dev convenience:
  - A deterministic dev fallback so `GET /{UMID}` can succeed for at least one known fixture UMID.

## Verification

- Start resolver dev:
  - `cd services/myum-resolver && npm run dev`
- Start site dev:
  - `cd site && npm run dev -- --host 127.0.0.1 --port 4300`
- Visit:
  - `http://127.0.0.1:4300/harness/index.html?autorun=1`
- Agent verification:
  - Use `agent-browser` to load the URL above and capture pass/fail output + screenshot.

## Completion record (2026-02-17)

- Harness UI:
  - `site/public/harness/index.html`
- Fixture sync:
  - `site/scripts/sync-harness-fixtures.mjs`
  - `site/package.json` runs sync on `dev` + `build`
- Resolver dev fixture fallback:
  - `services/myum-resolver/src/index.ts` resolves `urn:uuid:11111111-1111-4111-8111-111111111111`
- Verified:
  - Harness autorun PASS screenshot: `site/.agent-browser-harness-autorun-4.png`
