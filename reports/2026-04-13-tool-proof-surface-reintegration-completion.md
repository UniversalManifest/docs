# 2026-04-13 Tool/Proof-Surface Reintegration Completion

## Summary

`WO-0177` is complete. The interactive and proof entry routes now sit under a coherent shared tool shell instead of presenting as unrelated sprint-era products.

## What changed

- `site/src/layouts/ToolSurfaceLayout.astro` became the shared framing pattern for tool/proof entry routes.
- `site/src/pages/learning/index.astro` became the shared hub for sandbox, workbench, harness, journeys, and standards/discovery boundary framing.
- `site/src/pages/sandbox/index.astro` moved under the shared tool shell.
- `site/src/components/sandbox/ScenarioModal.astro` and `site/src/styles/sandbox/modal.css` were adjusted so the sandbox chooser can be hosted inside the shared shell instead of owning the whole route.
- `site/src/pages/workbench/index.astro` now presents the workbench under the shared shell.
- `site/public/workbench/app/index.html` preserves the existing workbench application as a subordinate payload.
- `site/public/workbench/index.html` now redirects legacy direct-entry traffic to `/workbench/app/`.

## Verification

- `npm run build` passed in `site/`.
- Browser verification passed on:
  - `http://127.0.0.1:4325/learning/`
  - `http://127.0.0.1:4325/sandbox/`
  - `http://127.0.0.1:4325/workbench/`
  - `http://127.0.0.1:4325/workbench/app/`
- Route-level verification confirmed:
  - `/workbench/` renders the shared public/tool shell and hosts the workbench payload in an iframe.
  - `/workbench/app/` loads the existing client-side workbench directly.
  - Loading `/harness/fixtures/v0.1/minimal-manifest.jsonld` still succeeds inside the embedded workbench payload.

## Outcome

The MVP-first site wave (`WO-0172` through `WO-0177`) is now complete. The public front door remains intentionally calm, while the higher-complexity tool and proof surfaces are available again behind the shared public/tool-shell family.
