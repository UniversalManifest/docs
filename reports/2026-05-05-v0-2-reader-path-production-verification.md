# v0.2 Reader Path Production Verification

Date: 2026-05-05T20:14:07Z

## Summary

Production route verification for the v0.2 reader path passed after Cloudflare credential repair and a deploy workflow artifact fix.

Final production deploy run:

- Run: https://github.com/grigb/universal-manifest/actions/runs/25399523864
- Head SHA: `4cdf0f890afe0d0234f105a43fd599003cb45849`
- Result: success
- Build publish bundle: success
- Deploy staging resolver: success
- Deploy staging docs: success
- Verify staging gates: success
- Deploy production resolver: success
- Deploy production docs: success
- Verify production gates: success

## Workflow Fix

The first production promotion after credential repair succeeded, but an independent check found:

- `https://universalmanifest.net/.well-known/universal-manifest.json` -> `404`

Root cause:

- `deploy/universalmanifest.net/build.mjs` writes `dist/.well-known/universal-manifest.json`.
- The `actions/upload-artifact@v4` publish-bundle step did not include hidden files/directories.
- Deploy jobs downloaded a bundle without `dist/.well-known/`.

Fix:

- Commit `4cdf0f890afe0d0234f105a43fd599003cb45849`
- File: `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml`
- Change: set `include-hidden-files: true` on the publish-bundle artifact upload.

Validation before rerun:

- `verify` workflow passed: https://github.com/grigb/universal-manifest/actions/runs/25399422359
- `CI/CD Pipeline` passed: https://github.com/grigb/universal-manifest/actions/runs/25399422262

## Production Route Checks

Independent route checks were run at `2026-05-05T20:13:37Z`.

- `https://universalmanifest.net/` -> `200`, `text/html; charset=utf-8`, title `Universal Manifest | Universal Manifest`
- `https://universalmanifest.net/use-cases/` -> `200`, `text/html; charset=utf-8`, title `Use Cases | Universal Manifest`
- `https://universalmanifest.net/explorer/` -> `200`, `text/html; charset=utf-8`, title `Scenario Explorer | Universal Manifest`
- `https://universalmanifest.net/how-it-works/` -> `200`, `text/html; charset=utf-8`, title `How It Works | Universal Manifest`
- `https://universalmanifest.net/standards-fit/` -> `200`, `text/html; charset=utf-8`, title `Standards Fit | Universal Manifest`
- `https://universalmanifest.net/spec/latest/` -> `200`, `text/html; charset=utf-8`, title `Universal Manifest v0.2 Specification`
- `https://universalmanifest.net/spec/v0.2/` -> `200`, `text/html; charset=utf-8`, title `Universal Manifest v0.2 Specification`
- `https://universalmanifest.net/guides/migration-v01-v02/` -> `200`, `text/html; charset=utf-8`, title `Migration Guide: v0.1 to v0.2 | Universal Manifest`
- `https://universalmanifest.net/publishing/changelog/` -> `200`, `text/html; charset=utf-8`, title `Changelog | Universal Manifest`
- `https://universalmanifest.net/.well-known/universal-manifest.json` -> `200`, `application/json`
- `https://universalmanifest.net/llms.txt` -> `200`, `text/plain; charset=utf-8`

## Artifact Evidence

Downloaded deploy artifact from run `25399523864` contains:

- `/tmp/um-deploy-artifacts-25399523864/publish-bundle/dist/.well-known/security.txt`
- `/tmp/um-deploy-artifacts-25399523864/publish-bundle/dist/.well-known/universal-manifest.json`
- `/tmp/um-deploy-artifacts-25399523864/production-deploy-checks/2026-05-05T20-13-10-765Z-post-deploy-verification.md`

The production workflow report recorded:

- docs workbench route: pass
- docs harness page: pass
- sandbox route: pass
- resolver tool route: pass
- resolver health apex/www: pass
- endpoint smoke suite: pass
- overall: pass

## Result

WO-0255 acceptance criteria are satisfied:

- Required production routes return `200`.
- v0.2 latest and durable spec routes are reachable.
- Discovery descriptor and `llms.txt` are reachable.
- Production deployment and verification gates are green.

Remaining user-action blocker for reader validation is no longer Cloudflare deployment. It is the real external-reader cohort/process required for WO-0256.
