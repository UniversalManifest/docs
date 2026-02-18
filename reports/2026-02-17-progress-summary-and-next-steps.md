# Universal Manifest — Progress Summary and Next Steps

Date: 2026-02-17  
Repo: `/Users/grig/work/repo/universalmanifest`

This report is an action-oriented summary of what exists in the Universal Manifest project right now, what we verified today, and the next critical path items to move toward broad adoption.

## 1) Current state (what exists)

Spec and fixtures:

- v0.1 draft spec: `spec/v0.1/`
- v0.1 fixtures (valid + invalid + near-real stubs): `examples/v0.1/`
- Stub manifest index with “vision drivers”: `docs/STUB-MANIFESTS.md`

Interop hardening (draft direction):

- v0.2 signature profile artifacts: `spec/v0.2/`
- v0.2 fixtures: `examples/v0.2/`

Tooling:

- TypeScript types + runtime assertion + verifier: `packages/universal-manifest/`
- Example validation runner: `packages/universal-manifest/scripts/validate-examples.mjs`

Proof/verification:

- User journeys → executable proof suite: `docs/journeys/README.md`
- Runner writes evidence JSON: `docs/journeys/_artifacts/`
- Endpoint smoke (docs + resolver contract): `packages/universal-manifest/scripts/smoke-endpoints.mjs`
- CI workflow (repeatable verification): `.github/workflows/verify.yml`

Publishing + hosting skeletons:

- Standards site (static): `site/` + `deploy/universalmanifest.net/`
- Resolver skeleton (Cloudflare Worker + KV): `services/myum-resolver/`

## 2) Verified today (commands that passed)

TypeScript + fixtures validation + signature verification:

- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test`

Journeys proof suite:

- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`
  - Evidence written under: `docs/journeys/_artifacts/`
  - Includes a non-LAN adopter proof (public profile projection)

Endpoint smoke (docs + resolver contract; local dev):

- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run smoke:endpoints:dev`

Docs site build and deploy bundle:

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build`
- `node /Users/grig/work/repo/universalmanifest/deploy/universalmanifest.net/build.mjs`
  - Output: `deploy/universalmanifest.net/dist/`

Local UI smoke via reserved port:

- Dev server running at: `http://127.0.0.1:4300/`
- Screenshots captured:
  - `/Users/grig/work/repo/universalmanifest/site/.agent-browser-home.png`
  - `/Users/grig/work/repo/universalmanifest/site/.agent-browser-harness-autorun-2026-02-17T09-32-02Z.png`
  - `/Users/grig/work/repo/universalmanifest/site/.agent-browser-conformance-resolver-2026-02-17T09-33-07Z.png`
  - `/Users/grig/work/repo/universalmanifest/site/.agent-browser-stub-manifests-2026-02-17T09-45-59Z.png`
  - `/Users/grig/work/repo/universalmanifest/site/.agent-browser-proof-smoke-2026-02-17T09-45-59Z.png`
  - `/Users/grig/work/repo/universalmanifest/site/.agent-browser-quick-start-2026-02-17T09-59-55Z.png`
  - `/Users/grig/work/repo/universalmanifest/site/.agent-browser-harness-autorun-2026-02-17T10-01-19Z.png`

## 3) Key decisions (current stance)

Domain split (authoritative):

- `universalmanifest.net` is the professional standards/spec/docs site.
- `myum.net/{UMID}` is the resolution path for stored manifests by ID.
- Reference: `docs/DOMAIN-ARCHITECTURE.md`.

IDs:

- UMIDs are currently **issuer-minted** `@id` values (example: `urn:uuid:<uuidv4>`).
- This is intentional: maximize adoptability before locking registry/governance.

Integrity vs adaptability:

- This is **additive**, not an either/or decision.
- Baseline interop profile exists in v0.2 (JCS + Ed25519 + base64url), while future Data Integrity paths remain possible.

LAN/Shield storage/logging:

- Cache full manifest payloads only while “in use”.
- Persist only `@id` references in logs for now (future restore remains optional).

## 4) What “done done” means (where to read)

Official definition and gates:

- `docs/DONE-DONE-DEFINITION.md`
- `docs/DONE-DONE-CHECKLIST.md`
- `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`

## 5) Critical path (what to do next)

Read the plan:

- `docs/CRITICAL-PATH.md`

The next execution-critical items (in order):

1. Decide what it means to “publish” v0.2 as a stable profile (URLs + immutability + versioning guarantees).
2. Expand conformance fixtures to cover TTL misuse/adversarial cases (v0.1.x and v0.2.x).
3. Make the resolver contract concrete for real adopters (error codes, caching headers, privacy posture, example requests/responses).
4. Add at least one non-LAN adopter journey (profile projection) as proof that UM is not LAN-only.
5. Create governance/public-facing docs required for serious external adoption (contrib/security/release discipline).

## 6) “World-ready” disclaimer

This work is **not** a completed universal standard for “the entire world” yet. The repo currently supports early-adopter validation and iteration, and it includes a formal “done done” framework to avoid making premature completion claims.
