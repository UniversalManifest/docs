# Docs Root Relocation And Warning-Free Build Baseline

**Date:** 2026-03-19
**Related work order:** `WO-0164`
**Status:** Completed relocation of the old docs-root content and cleared the final site-build warning

## Summary

The site build is now warning-free.

The final remaining warning came from Starlight still trying to publish the old docs-root content at `/` while the landing-first public surface already owned `/` with a custom page. This pass resolves that conflict by relocating the old docs-root content to `/docs/overview/` and linking it from the curated `/docs/` entry page.

## What Changed

### Relocated the old docs-root content

The file at `site/src/content/docs/index.md` no longer maps to `/`.

It now publishes as:

- `/docs/overview/`

To make that change explicit to readers:

- the page title is now `Documentation Overview`
- the page includes a note that `/docs/` is the curated docs start

### Updated the curated docs entry

The `/docs/` landing page now includes a direct link to the relocated long-form overview so the content remains reachable from the public docs surface.

## Verification

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build` -> PASS
- No warnings appeared in the build output
- Served-route checks returned `200 OK` for:
  - `/`
  - `/docs/`
  - `/docs/overview/`
- Served HTML confirmed:
  - `/docs/` includes a `Long-form docs overview` link
  - `/docs/overview/` includes the curated-entry note and renders the relocated overview content

## Browser Verification Note

I did not use browser-MCP verification in this pass. Earlier in the work stream those transports were unavailable, so verification here relied on the warning-free build plus direct served-route checks.

## Result

`WO-0164` is complete. The landing-first `/` route remains intact, the long-form overview remains published under `/docs/overview/`, and the site build baseline is now warning-free.
