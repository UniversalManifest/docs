# Legacy compatibility: `localartist.network` namespace URLs

This repo’s early v0.1 artifacts contain **namespace references** rooted at `https://localartist.network/`:

- `spec/v0.1/schema.json` uses:
  - `$id: https://localartist.network/ns/universal-manifest/v0.1/schema.json`
- `spec/v0.1/schema.jsonld` uses:
  - `lan: https://localartist.network/ns/universal-manifest/v0.1#`

Canonical publishing direction is now:

- `https://universalmanifest.net/ns/universal-manifest/v0.1/schema.jsonld`
- `https://universalmanifest.net/ns/universal-manifest/v0.1/schema.json`

This document defines what “don’t break old references” means and how to implement it without overbuilding.

## What “compatibility” means (practical)

If any third party has adopted v0.1 artifacts or examples that reference `localartist.network`, those references must remain resolvable.

Minimum compatibility requirement:

- Requests to:
  - `https://localartist.network/ns/universal-manifest/v0.1/schema.jsonld`
  - `https://localartist.network/ns/universal-manifest/v0.1/schema.json`
  must still succeed.

Preferred behavior (most robust):

- Return `200` and serve the **same bytes** as `universalmanifest.net` (plus correct CORS + content-type headers).

Acceptable fallback (may work in most tooling):

- Redirect (301/302) those legacy URLs to the canonical `universalmanifest.net` URLs.

## Recommended implementation (Cloudflare Pages)

### Option A (preferred): attach `localartist.network` as an alias domain to the same Pages project

If you control `localartist.network`, the simplest compatibility posture is:

1. Deploy `universalmanifest.net` from:
   - `/Users/grig/work/repo/universalmanifest/deploy/universalmanifest.net/dist/`
2. Attach **both** custom domains to the same Pages project:
   - `universalmanifest.net` (canonical)
   - `localartist.network` (compatibility alias)

Result:

- The legacy URLs resolve with `200` (because they are served by the same static artifact set).
- No separate build pipeline is required.

### Option B: deploy a minimal `localartist.network` compatibility site

If `localartist.network` must remain a separate site/project, deploy a small static compatibility bundle that:

- serves the two v0.1 schema/context URLs at `/ns/universal-manifest/v0.1/...`
- redirects everything else to `https://universalmanifest.net/`

This repo includes a deployment-ready skeleton for that:

- `/Users/grig/work/repo/universalmanifest/deploy/localartist.network/`

## Policy going forward

- v0.2+ artifacts should use `universalmanifest.net` as their canonical namespace roots.
- v0.1 remains “frozen” with compatibility handling provided at the hosting layer.

