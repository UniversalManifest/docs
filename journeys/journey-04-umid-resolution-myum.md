# Journey 04 — UMID resolution (myum.net skeleton)

Goal: prove resolver semantics (404/200/307/410) and deterministic retrieval.

## Steps

1. Start the `myum.net` resolver skeleton locally.
2. Verify:
   - `GET /health` returns `200`
   - unknown UMID returns `404`
3. Seed a payload record and verify `GET /{UMID}` returns `200` with manifest JSON.
4. Seed a redirect record and verify `GET /{UMID}` returns `307` with `Location`.
5. Seed a revoked record and verify `GET /{UMID}` returns `410`.

## Expected outcome

- Resolver behavior matches `docs/DOMAIN-ARCHITECTURE.md` and the skeleton contract doc.

## Executable proof

- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`

