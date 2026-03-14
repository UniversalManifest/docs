# WO-0029 Live Verification Report

Date: 2026-02-22

## Deployment

- Build artifact refresh:
  - `node deploy/universalmanifest.net/build.mjs`
- Cloudflare Pages deploy:
  - `CLOUDFLARE_ACCOUNT_ID=62421a9019bd0761655214e1160bcad0 npx --yes wrangler pages deploy deploy/universalmanifest.net/dist --project-name universalmanifest-net`
- Deployment URL returned by Wrangler:
  - `https://1683128a.universalmanifest-net.pages.dev`

## Live route checks

- `https://universalmanifest.net/` -> `200`
- `https://universalmanifest.net/integrations/social/` -> `200`
- `https://universalmanifest.net/getting-started/workbench/` -> `200`
- `https://universalmanifest.net/proof/harness/` -> `200`

## agent-browser verification (live)

Session: `um-navcheck`

Validated on `https://universalmanifest.net/`:

- Integrations sidebar order:
  1. Social/Profile
  2. Proof-of-Personhood
  3. OMATrust
  4. RP1 Spatial Fabric
  5. Smart Glasses
  6. Metaverse
  7. Chia DID/VC
- reference implementation page is not present in Integrations sidebar.
- Tools section contains:
  - Manifest Workbench
  - Verification Harness
- Overview no longer contains "Highlighted Tools" text.
- Core pilot animation exists on page (`/animations/um-core-flow-pilot.svg`).

Validated on `https://universalmanifest.net/getting-started/universal-manifest-overview/`:

- Overlay pilot animation exists (`/animations/um-overlay-lanes-pilot.svg`).

Validated on `https://universalmanifest.net/integrations/smart-glasses/`:

- Page title renders as `Smart Glasses | Universal Manifest`.

