# Journey 02 — TTL and freshness enforcement (do not use expired manifests)

Goal: prove local-first safety: manifests must not grant permissions or drive UI after expiry.

## Steps

1. Load an expected-invalid “expired for use” fixture:
   - `examples/v0.1/invalid/expired-for-use.jsonld`
2. Validate using “freshness” mode (enforces `now > expiresAt` rejection).

## Expected outcome

- Validation fails with an error containing: `Manifest expired`

## Executable proof

- `cd packages/universal-manifest && npm test`

