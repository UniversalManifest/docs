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
6. Commit and push:
   - `git status` clean
   - `git commit` with a clear message
   - `git push`
7. (Optional) Tag the release:
   - `git tag vX.Y.Z`
   - `git push --tags`

## 3) Release steps (publishing to `localartist.network`)

Goal: make these resolve over HTTPS with correct headers:

- `https://localartist.network/ns/universal-manifest/vX.Y/schema.jsonld`
- `https://localartist.network/ns/universal-manifest/vX.Y/schema.json`

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

If `latest/` aliases exist, they should redirect to a concrete version and should not be cached long-term.

## 4) Post-release hygiene

- Add/update a worklog entry (e.g., `docs/WORKLOG-YYYY-MM-DD.md`).
- Update `docs/STATE-OF-THE-PROJECT.md` milestones and links.
- If you added new well-known names, update:
  - `spec/v0.1/REGISTRY.md` (or the versioned equivalent)

