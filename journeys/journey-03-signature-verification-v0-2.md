# Journey 03 — v0.2 signature verification (JCS + Ed25519)

Goal: prove the v0.2 baseline integrity profile is executable and fails safely.

## Steps

1. Validate a v0.2 signed fixture:
   - `examples/v0.2/minimal-signed-manifest.jsonld`
2. Validate an invalid signature fixture:
   - `examples/v0.2/invalid/invalid-signature.jsonld`

## Expected outcome

- Signed fixture validates successfully.
- Invalid signature fixture fails with an error containing: `Signature verification failed`

## Executable proof

- `cd packages/universal-manifest && npm test`

