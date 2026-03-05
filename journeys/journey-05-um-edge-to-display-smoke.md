# Journey 05 — UM edge -> display smoke (optional, integration proof)

Goal: prove at least one real consumer integration path exists without coupling the standard to a single implementation.

This journey is optional in this repo's proof suite and is controlled by the journey-runner optional smoke configuration.

## Steps

1. Run the optional edge-to-display smoke path that:
   - starts backend
   - issues a manifest
   - verifies socket delivery
   - validates caching/logging semantics by ID reference

## Expected outcome

- Optional smoke path passes end-to-end when enabled.

## Executable proof

- `cd packages/universal-manifest && npm run journeys`
