# TypeScript Helper Package (`packages/universal-manifest/`)

This repo includes a small TypeScript helper package used for:

- keeping fixtures honest (executable validation)
- giving early adopters reference-quality types and assertions

Package location:

- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/`

Current package name (internal):

- `@localartistnetwork/universal-manifest`

## What it provides (and what it does not)

Provides:

- v0.1 types + structural assertions + TTL “freshness” assertion
- v0.2 draft types + signature verification (JCS + Ed25519) when `publicKeySpkiB64` is present
- a repo-local harness: `npm test`

Does not provide:

- a full SDK
- resolver clients
- DID/key resolution (beyond the fixture-friendly `publicKeySpkiB64` escape hatch)
- long-term stability guarantees independent of the spec repo

## How to run

From the package directory:

- `npm test` (validates v0.1 + v0.2 fixtures)
- `npm run journeys` (runs the journeys → tests proof suite; writes `docs/journeys/_artifacts/` report JSON)

## Distribution policy (current)

This package is **private** for now.

Rationale:

- the spec is still in v0.x and signatures/publishing are still stabilizing
- we want to avoid “public SDK drift” before the standard is ready

Publishing options (future):

- npm under an ecosystem-neutral scope (after naming/governance is settled)
- GitHub Packages for early adopter cohorts

Decision record:

- `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`

