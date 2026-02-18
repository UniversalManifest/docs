# Publishing & Versioning Plan — Universal Manifest

This document describes how the Universal Manifest spec artifacts should be published so external systems can adopt them reliably.

For the repo release workflow, see:

- `docs/RELEASING.md`

## 1) What must be publicly stable

For broad adoption, these artifacts need stable, HTTPS-hosted URLs:

- JSON-LD context (per spec version)
  - `spec/v0.1/schema.jsonld`
- JSON Schema (per spec version)
  - `spec/v0.1/schema.json`

Current repository history includes `localartist.network` namespace references in v0.1 files. Canonical hosting direction is now:

- `https://universalmanifest.net/ns/universal-manifest/v0.1/schema.jsonld`
- `https://universalmanifest.net/ns/universal-manifest/v0.1/schema.json`

Compatibility requirement:

- Keep legacy `localartist.network/ns/universal-manifest/...` URLs resolvable once published.
  - Implementation note: `docs/LEGACY-LOCALARTIST-NETWORK-COMPATIBILITY.md`

## 2) URL layout (recommended)

Use versioned, immutable paths:

- `https://universalmanifest.net/ns/universal-manifest/v0.1/schema.jsonld`
- `https://universalmanifest.net/ns/universal-manifest/v0.1/schema.json`

Optional convenience aliases (non-normative):

- `https://universalmanifest.net/ns/universal-manifest/latest/schema.jsonld`
- `https://universalmanifest.net/ns/universal-manifest/latest/schema.json`

If `latest/` exists, it MUST redirect (301/302) to a concrete version and MUST NOT serve mutable content directly.

## 3) Hosting options (implementation choice)

Any static hosting that supports correct headers is fine. Examples:

- Cloudflare Pages (custom domain)
- Cloudflare R2 + CDN
- GitHub Pages (with custom domain + correct MIME types)

The only hard requirement is that the URLs above resolve over HTTPS consistently.

Deployment-ready skeleton (in this repo):

- Static publishing config + build output layout:
  - `deploy/universalmanifest.net/README.md`
  - `deploy/universalmanifest.net/build.mjs` (writes `deploy/universalmanifest.net/dist/`)

Resolver note:

- Runtime UMID resolution belongs on `https://myum.net/{UMID}` and is intentionally separate from spec hosting.

## 4) Required HTTP headers

### 4.1 Content types

- `schema.jsonld` SHOULD be served as `application/ld+json`
- `schema.json` SHOULD be served as `application/schema+json` (or `application/json` if needed)

### 4.2 CORS

To allow browser-based tooling:

- `Access-Control-Allow-Origin: *` (or a permissive subset)

### 4.3 Caching

Because versioned paths are immutable:

- `Cache-Control: public, max-age=31536000, immutable`

If `latest/` redirects:

- keep redirect responses short-cacheable (or uncached), since it may change when a new version is released

## 5) Versioning rules (repo + network)

### 5.1 Immutable versions

Once a version is released (even v0.x):

- Do not modify previously published artifacts in-place.
- Create a new `spec/vX.Y/` folder for changes.

### 5.2 v0.x policy

During v0.x:

- breaking changes are allowed, but MUST be reflected by a new version folder (`v0.1` → `v0.2`)
- provide a short migration note in the newer version docs

### 5.3 v1.0 policy (future)

At v1.0:

- breaking changes require `v2.0` (major bump)
- minor versions may add optional fields, registry entries, and new fixtures

## 6) Registry + examples as adoption surface

External implementers typically start from:

- fixtures (`examples/`)
- conformance (`spec/v0.1/CONFORMANCE.md`)
- well-known names (`spec/v0.1/REGISTRY.md`)

We should treat these as “developer experience” artifacts:

- add stubs when they clarify intent
- add invalid fixtures when they clarify rejection behavior
- keep tests runnable (`packages/universal-manifest/` → `npm test`)

## 7) Distribution beyond HTTP (optional)

For ecosystems that prefer package managers:

- the TypeScript helper package (`packages/universal-manifest/`) can be published later
- the primary interoperability mechanism remains the HTTPS-hosted context/schema URLs

## 8) Checklist (release readiness)

Before calling a version “adoptable”:

- [ ] URLs resolve over HTTPS on `universalmanifest.net`
- [ ] Correct `Content-Type` headers for `.jsonld` and `.json`
- [ ] CORS enabled for tooling
- [ ] Versioned artifacts are immutable
- [ ] Conformance fixtures (valid + invalid) exist and are referenced
- [ ] A signature profile exists (v0.1 may defer; v0.2+ should specify)
- [ ] `myum.net/{UMID}` resolver behavior is documented and reachable for runtime usage
