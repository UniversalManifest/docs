# Journey 05 — LAN edge → display smoke (optional, integration proof)

Goal: prove at least one real consumer integration path exists (LAN) without making UM “about LAN”.

This journey is optional in this repo’s proof suite. It is controlled by runtime config:

- `UM_LAN_SMOKE=auto|on|off` (default: `auto`)
- `UM_LAN_REPO_PATH=/absolute/path/to/lan-platform`

Behavior:

- `auto`: run only when `UM_LAN_REPO_PATH` is configured and exists
- `on`: require LAN smoke to run (missing path is a failure)
- `off`: always skip LAN smoke

## Steps

1. Run the LAN smoke test that:
   - starts backend
   - issues a manifest
   - verifies socket delivery
   - validates caching/logging semantics by ID reference

## Expected outcome

- LAN smoke passes end-to-end.

## Executable proof

- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`
