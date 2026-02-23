# Publishing Runbook: universalmanifest.net (Static Site)

Date: 2026-02-13  
Work Order: `WO-reference implementation-universal-manifest-professional-docs-site-and-publishing`  
Status: COMPLETE

## 1) Build Artifact

Source app:

- `/Users/grig/work/repo/reference-platform/packages/site-client/`

Build command:

```bash
cd /Users/grig/work/repo/reference-platform
npm run build -w site-client
```

Output directory:

- `/Users/grig/work/repo/reference-platform/packages/site-client/dist/`

## 2) Static Hosting Contract

Files included for deployment behavior:

- `/Users/grig/work/repo/reference-platform/packages/site-client/public/_headers`
- `/Users/grig/work/repo/reference-platform/packages/site-client/public/_redirects`
- `/Users/grig/work/repo/reference-platform/packages/site-client/public/robots.txt`
- `/Users/grig/work/repo/reference-platform/packages/site-client/public/sitemap.xml`

Behavior:

- SPA routes under `/universal-manifest/*` resolve to `index.html`.
- static assets are immutable cached.
- `index.html` is revalidated on each request.
- baseline security headers are emitted by host supporting `_headers`.

## 3) Cloudflare Pages Baseline Deployment

Recommended setup:

- Framework preset: Vite
- Build command: `npm run build -w site-client`
- Build output: `packages/site-client/dist`

Environment:

- production domain: `universalmanifest.net`
- preview domain: `<project>.pages.dev`

## 4) Cutover Checklist

1. Build site and verify route resolution for:
   - `/universal-manifest`
   - `/universal-manifest/spec`
   - `/universal-manifest/integrations`
   - `/universal-manifest/governance`
   - `/universal-manifest/roadmap`
2. Verify headers and redirects are active on deployed host.
3. Validate `robots.txt` and `sitemap.xml` served from root.
4. Confirm content references still map to current spec/docs paths.

## 5) Rollback

- Re-deploy previous successful artifact build.
- Keep DNS unchanged if rollback is content-level only.
- If route-level breakage occurs, temporarily redirect root to `/universal-manifest`.
