# WO-0144 — myum Consumer Provenance and Example-State Hardening

**Status:** COMPLETED
**Created:** 2026-03-10
**Updated:** 2026-03-10
**Priority:** P0
**Owner:** Platform / Runtime UX
**Source:** Live production QA pass after WO-0124 closeout

## Objective

Remove remaining live-vs-stub ambiguity from the `myum` consumer resolver experience and make production example states representative enough to exercise the real contract surface.

## Problem Statement

Live production QA found that the main successful resolver example is served by a built-in fallback fixture in the Worker, but the consumer page presents it as a generic live resolver response and gives a plain safe-to-use verdict without calling out its demo provenance. Production also lacks public redirect and revoked demo records, so the consumer page cannot exercise all advertised response states against the live runtime.

## Scope

In scope:
- add explicit runtime provenance signaling for resolver responses
- surface provenance in the consumer resolver UI
- reduce misleading verdict language for fallback-fixture responses
- seed and verify live demo redirect/revoked records if remote KV access allows it
- add quick example entry points for available live contract states

Out of scope:
- private/authenticated resolver profiles
- write/registration APIs
- non-resolver frontend redesign work

## Acceptance Criteria

- [x] Resolver responses distinguish built-in fallback fixture responses from KV-backed responses.
- [x] Consumer resolver UI visibly labels response provenance and does not present fallback fixture data as ordinary authoritative live publisher data.
- [x] Production consumer flow can exercise at least `200`, `404`, and, if seeding succeeds, `307` and `410` against live runtime.
- [x] Browser verification completed on production resolver page after changes.

## Completion Summary

This work order is complete.

Delivered:
- runtime provenance labeling via `x-um-resolver-source` for `runtime`, `kv`, and `fallback_fixture`
- consumer resolver provenance pill, diagnostics row, example-state buttons, and fallback-fixture verdict downgrade
- live production redirect and revoked demo records in remote KV
- redirect-safe consumer lookup path using a same-origin Pages Function probe on `universalmanifest.net`
- Pages deployment hardening so `functions/` is shipped in CI and manual deploys

## Final Findings

During live production QA on 2026-03-10, the redirect demo state exposed a real consumer defect:

- direct browser `fetch(..., { redirect: 'manual' })` against `https://myum.net/...` returned an opaque cross-origin redirect
- the consumer UI collapsed that response to `status 0`
- the resolver contract header, provenance header, and `Location` header were therefore lost in-browser
- the page incorrectly rendered the redirect example as a generic failed response instead of a contract-visible `307`

The root cause was not the resolver runtime. It was the browser-side inspection path.

## Implementation

Code and deploy changes completed:

- Added a Pages Function probe at:
  - `deploy/universalmanifest.net/functions/api/resolver-probe.js`
- Updated the consumer page at:
  - `site/public/resolver/index.html`

Behavior after the fix:

- normal resolver responses still use direct browser fetches
- if the consumer hits a cross-origin opaque/`status 0` resolver response on an allowed resolver base, it falls back to `/api/resolver-probe`
- the probe performs the resolver request server-side on the docs host, preserving:
  - HTTP status
  - `Location`
  - `X-UM-Resolver-Contract`
  - `X-UM-Resolver-Source`
- the follow-redirect action now uses the same probe path and records the redirect target in trace output

Deployment hardening completed:

- `.github/workflows/deploy-gated.yml` now uploads/downloads the whole Pages bundle directory, not just `dist/`
- staging and production Pages deploy steps now run from the bundle root and deploy `dist/`, allowing sibling `functions/` to ship
- Pages runbook updated to require deploys from:
  - `deploy/universalmanifest.net`

## Deployment Evidence

Production Pages deploy executed manually on 2026-03-10 from:

- `deploy/universalmanifest.net`

Command used:

```bash
CLOUDFLARE_ACCOUNT_ID=62421a9019bd0761655214e1160bcad0 \
  npx wrangler pages deploy dist --project-name universalmanifest-net --branch main
```

Deployment URL returned by Cloudflare:

- `https://a9af2af1.universalmanifest-net.pages.dev`

## Verification Evidence

Server-side probe verified live on production:

- `https://universalmanifest.net/api/resolver-probe?...bbbb...`
  - returned `307`
  - preserved `Location`
  - preserved `X-UM-Resolver-Contract: myum-resolver/v0.1`
  - preserved `X-UM-Resolver-Source: kv`
- `https://universalmanifest.net/api/resolver-probe?...bbbb...&follow=1`
  - followed redirect target successfully
  - returned final `404` from `example.com`

Browser verification completed against:

- `https://universalmanifest.net/resolver/?v=20260310c`

Verified production states:

- fixture demo:
  - provenance pill: `Built-in demo fixture`
  - status: `200`
  - source: `fallback_fixture`
  - verdict correctly warns that payload is built-in demo data, not authoritative live publisher data
- redirect demo:
  - provenance pill: `KV-backed resolver record`
  - status: `307 Temporary Redirect`
  - source: `kv`
  - contract header visible
  - redirect action strip visible
  - verdict: manual review / follow target before use
- revoked demo:
  - status: `410`
  - source: `kv`
  - verdict: do not use
- unknown demo:
  - status: `404`
  - source: `runtime`
  - verdict: do not use
- mobile check:
  - no horizontal overflow at `390px` viewport
  - example buttons remained visible

Follow-redirect action also verified on production:

- final response: `404 Not Found`
- trace now records the concrete redirect target URL rather than dropping it

## Reporting

Closeout report:

- `.dev/ai/reports/operations/2026-03-10-myum-consumer-redirect-probe-production-fix.md`
