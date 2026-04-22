# 2026-04-22 Latest Spec Surface Strategy and Shell Implementation

## Purpose

This report closes `WO-0185` by deciding the durable architecture for `/spec/latest/`.

The key question was not whether the W3C-style reading surface should survive. It should. The actual problem was that `/spec/latest/` still behaved like a raw injected standalone HTML document, which left the route as a structural exception even after the rest of the public site had clearer shell ownership.

## Decision

The permanent model is a bounded restructuring:

- keep `/spec/latest/` as a dedicated W3C-style standards-reader surface
- keep `docs/W3C-STYLE-SPEC.html` as the source of truth for the spec body, W3C presentation rules, and reader-side behavior
- move the outer route shell for `/spec/latest/` into `site/src/pages/spec/latest.astro`

This deliberately does not force the latest spec into the broader `PublicSurfaceLayout` marketing/reader shell. That would reduce the clarity of the standards-reading experience for little architectural gain.

## What changed

### 1. Astro now owns the `/spec/latest/` document shell

Updated:

- `site/src/pages/spec/latest.astro`

That route now:

- extracts the checked-in spec document's `<head>` and `<body>` content at build time
- emits the canonical HTML document for `/spec/latest/`
- owns the calm public nav for this route with only:
  - `Home`
  - `Latest Spec`
- keeps internal `universalmanifest.net` links host-relative when rendered locally or in mirrors

### 2. The checked-in spec document remains the source of truth for the reader surface

Updated:

- `docs/W3C-STYLE-SPEC.html`

That file now explicitly serves as the source of truth for:

- the normative spec body content
- W3C-style document presentation
- TOC behavior and related reader scripts

It no longer owns the route-level site nav, because that is now part of the Astro shell for `/spec/latest/`.

## Result

The authoritative posture is now:

- `/spec/latest/` remains the one-click public latest-spec route
- the W3C-style standards-reading experience remains intact
- the route is no longer a raw full-document injection exception
- shell ownership is explicit: Astro owns the route shell, the checked-in HTML owns the document body and spec-reader behavior

## Verification

Build verification:

- Ran `npm run build` in `/Users/grig/work/repo/universalmanifest/site`
- Result: passed
- Residual warnings were the existing route-priority warnings for:
  - `/about/one-pager`
  - `/about/why-um`
  - `/proof/harness`
  - `/use-cases`

Generated output verification:

- Confirmed `/Users/grig/work/repo/universalmanifest/site/dist/spec/latest/index.html` now contains:
  - canonical metadata for `https://universalmanifest.net/spec/latest/`
  - the Astro-owned `Site` nav with `Home` and `Latest Spec`
  - the checked-in W3C stylesheet and document body content

Browser-visible verification:

- Served the built site locally from `/Users/grig/work/repo/universalmanifest/site/dist` via `python3 -m http.server 4326`
- Opened `http://127.0.0.1:4326/spec/latest/` in a browser
- Verified the rendered page shows:
  - calm top nav with `Home` and `Latest Spec`
  - the W3C-style title block and publication metadata
  - the abstract and TOC in the expected reading layout
- Console verification was clean: no warnings or errors
- Captured evidence:
  - screenshot: `/Users/grig/work/repo/universalmanifest/.tmp-browser-checks/wo-0185-spec-latest.png`
  - accessibility snapshot: `/Users/grig/work/repo/universalmanifest/.tmp-browser-checks/wo-0185-spec-latest.snapshot.txt`
