# universalmanifest.net — Deployment Notes (static)

This repo contains two related deployment runtimes:

- Standards/docs host: `universalmanifest.net`
  - Spec artifacts and docs site
- Resolver host: `myum.net/{UMID}`
  - Runtime resolution service (separate; see `services/myum-resolver/`)

Staging + promotion runbook:

- `/Users/grig/work/repo/universalmanifest/docs/site/STAGING-PROMOTION-RUNBOOK.md`

## 1) Publish spec artifacts (`/ns/...`)

Build:

- `node /Users/grig/work/repo/universalmanifest/deploy/universalmanifest.net/build.mjs`

Output:

- `/Users/grig/work/repo/universalmanifest/deploy/universalmanifest.net/dist/`

Deploy:

- Publish that `dist/` directory to your static host (Cloudflare Pages suggested).

Cloudflare Pages runbook (deployment-ready):

- `/Users/grig/work/repo/universalmanifest/deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`

## 2) Build the documentation site (site/)

Build:

- `cd /Users/grig/work/repo/universalmanifest/site && npm install`
- `cd /Users/grig/work/repo/universalmanifest/site && npm run build`

Output:

- `/Users/grig/work/repo/universalmanifest/site/dist/`

## 3) Combine site output with `/ns/...` artifacts (recommended final shape)

The recommended final deploy layout for `universalmanifest.net` is one static root that contains:

- docs site output (e.g., `site/dist/`)
- `/ns/universal-manifest/vX.Y/...` spec artifacts
- `/harness/` (quick testing page)

This repo’s `deploy/universalmanifest.net/build.mjs` already supports this combination:

1. Build the docs site (`site/dist/`)
2. Run the publish build script (`deploy/universalmanifest.net/build.mjs`)
3. Deploy `deploy/universalmanifest.net/dist/`
