# Releasing the Spec (Draft)

This repo is designed to be adopted by external systems. Releases should prioritize:

- **immutability** of versioned artifacts
- **stable URLs** for JSON-LD contexts and schemas
- **clear conformance expectations** (fixtures + checklist)

## 1) When to cut a new version

Create a new `spec/vX.Y/` version when:

- you change required fields/semantics
- you change meaning of a well-known registry entry
- you change signature/canonicalization expectations

If changes are purely additive (new optional fields/fixtures/docs), you may stay within the same spec version, but avoid editing already-published artifacts if they are publicly hosted.

## 2) Release steps (repo)

1. Ensure the new spec version folder exists:
   - `spec/vX.Y/README.md`
   - `spec/vX.Y/schema.json`
   - `spec/vX.Y/schema.jsonld`
2. Update identifiers inside artifacts:
   - `$id` in `schema.json`
   - namespace URLs in `schema.jsonld`
3. Update docs pointers:
   - `docs/README.md`
   - `docs/STATE-OF-THE-PROJECT.md`
   - `docs/DECISIONS.md` (record why/what changed)
4. Update conformance:
   - `spec/vX.Y/CONFORMANCE.md` (or add if new)
   - add/adjust fixtures under `examples/vX.Y/`
5. Run tests:
   - from `packages/universal-manifest/`: `npm test`
   - proof suite: `npm run journeys`
   - (optional, local dev servers) endpoint smoke: `npm run smoke:endpoints:dev`
6. Commit and push:
   - `git status` clean
   - `git commit` with a clear message
   - `git push`
7. (Optional) Tag the release:
   - `git tag vX.Y.Z`
   - `git push --tags`

## 2.1) Release steps (conformance suite)

Use this flow when releasing fixture/runner changes under `conformance/`.

1. Determine version bump type:
   - major: breaking expected-result changes
   - minor: additive fixtures
   - patch: bugfixes preserving conformant behavior
2. Update suite metadata:
   - `conformance/package.json` version
   - `conformance/v0.1/expected.json` and/or `conformance/v0.2/expected.json` `suiteVersion`
3. Validate runner and adapter path:
   - `cd conformance/runner && npm test`
   - `cd conformance/runner && node ./cli.mjs --mode command --adapter-command \"node ../adapters/typescript/adapter.mjs\" --versions 0.1,0.2 --report ./conformance-report.json`
4. Confirm no unintended regressions against reference implementation.
5. Commit with explicit suite-version rationale.
6. Tag conformance release (or include in coordinated repo release notes).

## 2.2) Release authority and approvals

1. Patch release:
   - releaser: any maintainer
   - approval: at least one maintainer review
2. Minor release:
   - releaser: maintainer after TSC consensus
   - approval: consensus recorded in review thread / decision log
3. Major release (breaking):
   - releaser: maintainer delegated by TSC
   - approval: TSC consensus, RFC approved, migration and deprecation artifacts published

## 3) Release steps (publishing to `universalmanifest.net`)

Goal: make these resolve over HTTPS with correct headers:

- `https://universalmanifest.net/ns/universal-manifest/vX.Y/schema.jsonld`
- `https://universalmanifest.net/ns/universal-manifest/vX.Y/schema.json`

For current v0.2 draft publication checks:

- `https://universalmanifest.net/ns/universal-manifest/v0.2/schema.jsonld`
- `https://universalmanifest.net/ns/universal-manifest/v0.2/schema.json`
- `https://universalmanifest.net/spec/v02/`
- `https://universalmanifest.net/conformance/v02/`

Required headers are described in:

- `docs/PUBLISHING-AND-VERSIONING.md`

Minimum verification checklist:

1. Fetch both URLs and confirm `200 OK`.
2. Confirm content types:
   - `.jsonld` served as `application/ld+json` (preferred)
   - `.json` served as `application/schema+json` (or `application/json`)
3. Confirm CORS:
   - `Access-Control-Allow-Origin: *` (or an allowlist that includes your tooling origins)
4. Confirm caching headers on versioned paths:
   - long-lived immutable caching is OK because versioned paths must not change
5. Confirm human-facing spec/conformance routes resolve:
   - `/spec/v02/`
   - `/conformance/v02/`

If `latest/` aliases exist, they should redirect to a concrete version and should not be cached long-term.

Compatibility rule:

- Keep any previously published `localartist.network/ns/universal-manifest/...` URLs resolvable as aliases.
- Do not repoint or remove old public URLs once clients depend on them.

## 3.1 Resolver publication (`myum.net`)

Release also includes runtime resolver checks for:

- `https://myum.net/{UMID}`

Minimum validation:

1. Known UMID returns either `200` (manifest payload) or redirect to canonical payload location.
2. Unknown UMID returns deterministic `404`.
3. Resolver does not require spec-site deployment coupling.

## 3.2 Combined production smoke (recommended)

After `universalmanifest.net` and `myum.net` are both deployed, run the combined endpoint smoke:

- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest` → `npm run smoke:endpoints:prod`

Staging-first promotion is the default operating model:

- run staging checks first (`npm run smoke:endpoints:staging` and `npm run verify:postdeploy:staging`)
- promote to production only after staging gates pass
- run production checks after promotion

Runbook:

- `/Users/grig/work/repo/universalmanifest/docs/site/STAGING-PROMOTION-RUNBOOK.md`

Runbook:

- `/Users/grig/work/repo/universalmanifest/docs/PRODUCTION-DEPLOY-SMOKE.md`

## 4) Post-release hygiene

- Add/update a worklog entry (e.g., `docs/WORKLOG-YYYY-MM-DD.md`).
- Update `docs/STATE-OF-THE-PROJECT.md` milestones and links.
- If you added new well-known names, update:
  - `spec/v0.1/REGISTRY.md` (or the versioned equivalent)

## CI verification

This repo includes a GitHub Actions workflow that runs the same core proof steps on every PR:

- `/Users/grig/work/repo/universalmanifest/.github/workflows/verify.yml`
