# Domain Architecture — Universal Manifest

This project uses two public domains with distinct responsibilities.

## 1) Standards domain: `universalmanifest.net`

Purpose:

- Public website for learning, governance, and adoption
- Versioned spec artifacts (`schema.jsonld`, `schema.json`, conformance docs)

Expected URL shape:

- `https://universalmanifest.net/` (docs + overview)
- `https://universalmanifest.net/ns/universal-manifest/v0.1/schema.jsonld`
- `https://universalmanifest.net/ns/universal-manifest/v0.1/schema.json`

Operational model:

- Static hosting/CDN (immutable versioned paths)
- CORS enabled for tooling
- Correct content types for JSON-LD/JSON Schema

## 2) Resolver domain: `myum.net`

Purpose:

- UMID resolution and manifest retrieval
- Optional metadata/redirect behavior for clients

Expected URL shape:

- `https://myum.net/{UMID}`

Resolver behavior (recommended baseline):

1. Resolve UMID to manifest storage location (or directly to manifest payload).
2. Return either:
   - `200` with manifest JSON/JSON-LD, or
   - `302/307` redirect to canonical manifest URL.
3. Include integrity metadata when available (hash, signature profile, issued/expires).

Minimal response requirements:

- Deterministic lookup for the same UMID
- Clear error semantics (`404` unknown UMID, `410` revoked/removed if policy requires)
- No requirement to centralize authoring: resolver can index externally hosted manifests

## 3) Why this split exists

- Keeps the specification neutral and professional (`universalmanifest.net`)
- Keeps runtime document lookup concerns isolated (`myum.net`)
- Makes Linux Foundation style adoption paths cleaner (spec governance != app/runtime service)

## 4) Compatibility + migration

Current repo history contains `localartist.network` namespace references in v0.1 artifacts.

Migration policy:

- Keep `localartist.network/ns/universal-manifest/...` resolvable as compatibility aliases.
- Publish new canonical artifacts on `universalmanifest.net/ns/universal-manifest/...`.
- Do not break old references once published.

## 5) Next implementation steps

1. Stand up static hosting for `universalmanifest.net` spec artifacts.
2. Stand up resolver service for `myum.net/{UMID}`.
3. Add operational runbook for resolver ingestion, caching, and revocation handling.
4. Add conformance fixtures that exercise `myum.net` pointer patterns.

