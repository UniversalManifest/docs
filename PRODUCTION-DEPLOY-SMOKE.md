# Production deploy smoke (universalmanifest.net + myum.net)

This runbook is the fastest way to validate that the two-domain architecture is correctly deployed:

- `https://universalmanifest.net` (standards/spec/docs)
- `https://myum.net/{UMID}` (resolver contract)

It uses the repo’s endpoint smoke script so verification is **repeatable and automatable**.

## Prereqs

- `universalmanifest.net` is deployed (Cloudflare Pages):
  - Runbook: `/Users/grig/work/repo/universalmanifest/deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`
- `myum.net` resolver is deployed (Cloudflare Worker + KV):
  - Runbook: `/Users/grig/work/repo/universalmanifest/services/myum-resolver/CLOUDFLARE-DEPLOY.md`

## One command (recommended)

From the TS helper package:

- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run smoke:endpoints:prod`

This checks:

- docs site endpoints + `/404.html`
- published spec artifact URL(s), e.g. `/ns/universal-manifest/v0.1/schema.jsonld`
- resolver `/health` and `/.well-known`
- resolver `ETag` + 304 revalidate semantics
- resolver headers per contract (incl. exposed headers for browser tooling)

## If production doesn’t have the default UMID seeded

The smoke script defaults to:

- `urn:uuid:11111111-1111-4111-8111-111111111111`

If your production resolver does not serve that UMID, pass a known UMID:

- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && node scripts/smoke-endpoints.mjs --mode prod --docs-base https://universalmanifest.net --resolver-base https://myum.net --umid 'urn:uuid:YOUR-UMID-HERE'`

## Troubleshooting

If the smoke fails:

1. Confirm DNS + HTTPS are live:
   - `curl -fsSI https://universalmanifest.net/ | head`
   - `curl -fsSI https://myum.net/health | head`
2. Confirm spec artifacts resolve:
   - `curl -fsSI https://universalmanifest.net/ns/universal-manifest/v0.1/schema.jsonld | rg -i '^(http/|content-type:|cache-control:|access-control-allow-origin:)'`
3. Confirm resolver headers:
   - `curl -fsSI "https://myum.net/urn%3Auuid%3A11111111-1111-4111-8111-111111111111" | rg -i 'etag:|cache-control:|x-um-resolver-contract|access-control-expose-headers'`

