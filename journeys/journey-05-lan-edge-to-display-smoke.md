# Journey 05 — LAN edge → display smoke (optional, integration proof)

Goal: prove at least one real consumer integration path exists (LAN) without making UM “about LAN”.

This journey is optional in this repo’s proof suite. It is run automatically only if the LAN repo exists at:

- `/Users/grig/work/lan/lan-platform/`

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

