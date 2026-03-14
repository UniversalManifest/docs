# WO-0024 — Multi-provider proof-of-personhood, social identity, DID, and Chia integration

**Status:** COMPLETED
**Created:** 2026-02-20

## Objective

Prove Universal Manifest supports real multi-provider personhood credentials by integrating 3 API-backed proof-of-personhood providers (including World ID), binding those credentials to Mastodon and Bluesky-linked account manifests, supporting multiple DID methods, and adding a Chia integration lane.

## Scope

In scope:
- ingest and assess API-backed proof-of-personhood providers with traceable source records.
- target a 3-provider implementation lane:
  - World ID (Worldcoin)
  - Gitcoin Passport
  - BrightID
- create manifest fixtures showing one identity profile linked to:
  - Mastodon account metadata
  - Bluesky account metadata
- include multiple DID methods in fixtures and validation flow.
- include Chia integration references (DID/VC attestation lane) in fixture + journey documentation.
- add executable journey coverage proving multi-credential resolution and policy decisions.

Out of scope:
- production user onboarding flows for external providers.
- paid vendor contracts or enterprise-only APIs.
- normative spec version bumps unless conformance policy requires them.

## Deliverables

- work order execution artifacts under:
  - `.dev/ai/knowledge-index/`
  - `.dev/ai/knowledge-corpus/`
  - `.dev/ai/ingestion/records/`
- new/updated integration docs under:
  - `integrations/`
  - `site/src/content/docs/integrations/`
- fixtures and proof artifacts under:
  - `examples/`
  - `docs/journeys/`
  - `docs/journeys/_artifacts/`
- source-of-truth updates:
  - `docs/PROJECT-VISION.md`
  - `docs/DECISIONS.md`
  - `docs/STATE-OF-THE-PROJECT.md`

## Acceptance criteria

- [x] Stage -1/0 source intake is complete for at least 3 API-backed proof-of-personhood providers, including World ID.
- [x] each selected provider has provenance-mapped records in SOURCE-MAP and ingestion ledger updates.
- [x] at least one Mastodon-linked manifest and one Bluesky-linked manifest include 2 or more proof-of-personhood credential references.
- [x] DID coverage includes at least 3 methods with explicit rationale and interoperability constraints (for example `did:plc`, `did:web`, `did:key` or equivalent selected set).
- [x] Chia lane includes at least one concrete fixture/documented mapping for Chia DID/VC-style credential references.
- [x] journey runner includes executable checks proving multi-provider credentials can coexist and be resolved per policy.
- [x] strict K2B validator remains PASS after ingestion and artifact updates.

## Dependencies

- `docs/workorders/WO-0014-interactive-manifest-workbench.md`
- `docs/workorders/WO-0017-corpus-to-ia-and-journey-synthesis.md`
- `docs/workorders/WO-0018-mum-lineage-and-emerging-integration-codification.md`
- `docs/workorders/WO-0020-rp1-source-ingestion-and-synthesis-materialization.md`
- `docs/workorders/WO-0021-smart-glasses-consent-fixtures-and-proof-journeys.md`
- `docs/workorders/WO-0022-metaverse-lane-fixtures-and-proof-hardening.md`
- `docs/workorders/WO-0023-production-deployment-drift-prevention-automation.md`

## Execution evidence (2026-02-20)

K2B source intake (P1):

- `.dev/ai/knowledge-corpus/imports/external-22-world-id-proof-of-personhood.md`
- `.dev/ai/knowledge-corpus/imports/external-23-gitcoin-passport-verification.md`
- `.dev/ai/knowledge-corpus/imports/external-24-brightid-verification.md`
- `.dev/ai/ingestion/records/2026-02-20-wo0024-personhood-provider-intake.md`

Fixtures (P2):

- `examples/v0.1/stubs/mastodon-personhood-multi-credential-manifest.jsonld`
- `examples/v0.1/stubs/bluesky-personhood-multi-credential-manifest.jsonld`
- `examples/v0.1/stubs/multi-did-method-coverage-manifest.jsonld`
- `examples/v0.1/stubs/chia-credential-lane-manifest.jsonld`

Integration docs (P3):

- `integrations/proof-of-personhood.md`
- `integrations/chia-vc.md`
- `site/src/content/docs/integrations/proof-of-personhood.md`
- `site/src/content/docs/integrations/chia-vc.md`

Journey evidence (P4):

- `docs/journeys/J10-multi-provider-personhood-coexistence.md`
- `packages/universal-manifest/scripts/run-journeys.mjs`
- `docs/journeys/_artifacts/2026-02-20T19-58-34-497Z-journey-report.json`

Validation gate (P5):

- npm test: 18 valid OK, 13 invalid OK (0 failures)
- npm run journeys: 6 pass, 0 fail
- site build: 31 pages built successfully

## Execution notes

- if one target provider is blocked by API access policy, replace it with another API-backed proof-of-personhood provider and record rationale in ingestion records.
- all provider-specific claims must be marked until conformance criteria are formalized.
