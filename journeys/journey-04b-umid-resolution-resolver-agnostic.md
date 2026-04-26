# Journey 04b — UMID resolution (resolver-agnostic, any HTTP base URL)

Goal: prove that **any conformant HTTP resolver implementation** — Cloudflare Worker, Node.js, Go, Rust, or other — exposes the contract documented in `services/myum-resolver/CONTRACT.md` (sections 4.1, 4.5, and the eight mandatory status codes for `/{UMID}`).

Journey J04 (`docs/journeys/journey-04-umid-resolution-myum.md`) targets the in-repo Cloudflare Worker via `wrangler dev` and is intentionally preserved for the spec repo's own runtime. **J04b is the resolver-agnostic sibling**: it accepts any HTTP base URL via a flag/env var so adopters building their own resolver can prove conformance against their own server with the same scenario matrix.

## Targeted-runtime contract surface

The resolver under test MUST implement the contract documented in `services/myum-resolver/CONTRACT.md`. J04b exercises the following baseline (a strict subset of `npm run test:contract` from `services/myum-resolver/`):

- `GET /health` returns `200` with `Cache-Control: no-store` and JSON body containing `status: "ok"` and `contract`.
- `GET /{UNKNOWN_UMID}` returns `404`.
- `GET /{PAYLOAD_UMID}` returns `200` with `application/ld+json` body and weak `ETag`.
- `GET /{REDIRECT_UMID}` returns `307` with a `Location` header.
- `GET /{REVOKED_UMID}` returns `410`.
- `OPTIONS /{UMID}` returns `204` with CORS headers (`Access-Control-Expose-Headers` MUST list `etag`, `cache-control`, `location`, `x-um-resolver-contract`, `x-um-resolver-source`).
- Required response headers present on `/{UMID}` GET: `X-UM-Resolver-Contract: myum-resolver/v0.1`, `X-UM-Resolver-Source: kv | runtime | fallback_fixture`.

Optional adversarial extensions (`B04b-extended`):

- `GET /{INVALID_UMID_ENCODING}` returns `400`.
- `POST /{UMID}` returns `405`.
- `GET /{UMID}` with `If-None-Match: <current-etag>` returns `304`.

## Steps

1. **Provision a target resolver.** The implementer brings up their resolver such that it is reachable at an HTTP base URL (e.g., `http://127.0.0.1:8788`, `http://localhost:3000`, or a deployed staging URL).
2. **Seed deterministic fixtures.** The implementer SHOULD ensure that the following demo UMIDs resolve as documented:
   - `urn:uuid:11111111-1111-4111-8111-111111111111` → `200` payload (use the spec's v0.2 minimal signed manifest fixture from `examples/v0.2/minimal-signed-manifest.jsonld`).
   - `urn:uuid:22222222-2222-4222-8222-222222222222` → `307` redirect to a static URL.
   - `urn:uuid:33333333-3333-4333-8333-333333333333` → `410` revoked.
   - `urn:uuid:99999999-9999-4999-8999-999999999999` → `404` unknown.
   The exact UMID values are configurable via env vars (see "Configuration").
3. **Run the conformance probe.** Run the resolver-agnostic probe against the base URL:
   ```bash
   UM_RESOLVER_BASE_URL=http://127.0.0.1:8788 \
     npm --prefix services/myum-resolver run test:contract:agnostic
   ```
   or, for adopters consuming the published reference implementation:
   ```bash
   UM_RESOLVER_BASE_URL=https://my-resolver.example \
     npx @universalmanifest/typescript resolver-conformance
   ```
4. **Assert PASS.** All scenarios in the baseline matrix MUST pass. Extended scenarios are recommended.

## Configuration

| Knob | Default | Purpose |
|---|---|---|
| `UM_RESOLVER_BASE_URL` (env) or `--base-url` (CLI) | `http://127.0.0.1:8788` | HTTP base URL of the resolver under test. |
| `UM_RESOLVER_PAYLOAD_UMID` | `urn:uuid:11111111-1111-4111-8111-111111111111` | UMID expected to return `200` with manifest payload. |
| `UM_RESOLVER_REDIRECT_UMID` | `urn:uuid:22222222-2222-4222-8222-222222222222` | UMID expected to return `307` redirect. |
| `UM_RESOLVER_REVOKED_UMID` | `urn:uuid:33333333-3333-4333-8333-333333333333` | UMID expected to return `410` gone. |
| `UM_RESOLVER_UNKNOWN_UMID` | `urn:uuid:99999999-9999-4999-8999-999999999999` | UMID expected to return `404` not found. |
| `UM_RESOLVER_REQUIRE_EXTENDED` (`true`/`false`) | `false` | If `true`, also runs B04b-extended (304/400/405). |

Implementations MAY ignore the seeding step and instead pre-load fixtures on startup; the probe only asserts response shape, not how state was provisioned.

## Compliance levels

- **B04b-baseline** — `200`, `307`, `404`, `410`, `/health`, header presence. **Required** for "conformant resolver" claim.
- **B04b-extended** — `304`, `400`, `405`, OPTIONS source header, ETag round-trip. **Recommended.**

## Backwards compatibility with J04

J04 (Cloudflare-coupled) is **NOT removed**. It continues to run the spec repo's own `services/myum-resolver/` via `wrangler dev` as part of `npm run journeys`. J04b layers a resolver-agnostic test surface on top of the same contract; the two journeys are not mutually exclusive.

When an adopter forks `https://github.com/grigb/um-typescript` and stands up their own resolver, they run J04b — not J04 — to prove conformance.

## Expected outcome

- Any HTTP resolver claiming UM compliance can satisfy J04b without bundling Cloudflare tooling.
- The reference implementation at `https://github.com/grigb/um-typescript` (and any fork) can run J04b against itself in CI.
- J04 remains the spec repo's internal end-to-end check.

## Executable proof

For the spec repo's Cloudflare Worker (preserved):

```bash
cd packages/universal-manifest && npm run journeys
```

For an arbitrary HTTP resolver:

```bash
UM_RESOLVER_BASE_URL=<base-url> \
  npm --prefix services/myum-resolver run test:contract -- --base-url=$UM_RESOLVER_BASE_URL
```

(Implementers MAY also vendor `services/myum-resolver/scripts/contract-tests.mjs` directly; it already accepts a base URL via `RESOLVER_URL` env var as of v0.1 of the contract suite.)

## Implementation notes for adopters

- Header casing: HTTP/1.1 is case-insensitive. Probes lowercase header names before comparing.
- `ETag` weakness: the contract specifies a weak ETag (`W/"sha256-..."`). Implementations MAY use a stronger derivation as long as the same body produces the same ETag deterministically.
- `X-UM-Resolver-Source` values: for non-Cloudflare resolvers, `kv` MAY be replaced with a runtime-specific label (e.g., `postgres`, `dynamodb`). The contract requires the header to be present and non-empty, not a fixed enum.

## Cross-references

- `services/myum-resolver/CONTRACT.md` — authoritative public contract.
- `docs/journeys/journey-04-umid-resolution-myum.md` — the original Cloudflare-targeted journey.
- `docs/IMPLEMENTING-UM.md` — fork-and-conform guide for new implementations.
- `https://github.com/grigb/um-typescript` — reference implementation (npm package consumes resolver via `resolve()`; a future companion repo MAY provide a Node.js resolver suitable for J04b).
