# OMATrust Integration Assessment for Universal Manifest

Date: 2026-02-22 UTC  
Project root: `/Users/grig/work/repo/universalmanifest`  
Prepared for: Universal Manifest status check + OMATrust product and OMA3 standards-body integration decision support

## 1) Executive status summary

- Universal Manifest repo status now:
  - Branch: `main`
  - `HEAD`: `06b2da2`
  - `origin/main`: `06b2da2`
  - Work-order docs indicate `WO-0001` through `WO-0024` are marked completed.
  - Working tree is heavily dirty (many modified/untracked implementation and docs artifacts not yet committed).
- Live endpoint spot-checks are green right now:
  - `https://universalmanifest.net/` -> `200`
  - `https://universalmanifest.net/workbench/` -> `200`
  - `https://universalmanifest.net/harness/` -> `200`
  - `https://myum.net/health` -> `200`
  - `https://www.myum.net/health` -> `200`

Interpretation: the project is operational and feature-rich, but release hygiene is currently gated by uncommitted local state.

## 2) OMATrust research scope and coverage

I covered OMATrust sources in two layers:

- Layer A: semantic deep-read of the key protocol/product pages (reputation model, attestation taxonomy, verification flow, SDK/API, app-registry architecture, chain architecture, x402, ERC-8004).
- Layer B: link-coverage crawl across OMATrust root site links plus the full docs sitemap.

Coverage artifact created:

- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-22-oma-link-coverage-evidence.md`

Coverage highlights from the artifact:

- Root site outbound links discovered: 15.
- `docs.omatrust.org/sitemap.xml` entries: 43 pages (all resolved `200`). [32]
- Preview portals reachable (`200`) and explicitly labeled preview/pre-alpha/testnet oriented. [27] [28]

## 3) What OMATrust currently is (source-backed)

### 3.1 Platform positioning

- OMATrust positions itself as a decentralized trust layer with attestations, identity, and reputation for internet services. [1]
- Governance framing is tied to OMA3 consortium stewardship and neutrality language. [1]
- The developer docs frame OMATrust as an EAS-based reputation layer for services/agents with SDK-first integration paths. [2]

### 3.2 Current product surfaces

- Reputation Portal exists and is labeled pre-alpha/testnet/incomplete. [27]
- Registry Developer Portal exists and is labeled developer preview/testnet/data-loss risk. [28]
- App Registry docs are explicitly marked preview and not production-ready. [18] [23]

### 3.3 Protocol model and trust semantics

- Reputation model is service-centric (apps/APIs/contracts/organizations), not end-user social scoring. [5]
- Attestation families are split into support attestations and reputation attestations. [5] [6]
- Canonical reputation/support types include Linked Identifier, Key Binding, Controller Witness, User Review, User Review Response, Endorsement, Certification, Security Assessment. [6]
- Verification flow is explicitly three-stage: structural validation, proof verification, trust-model application. [6]
- The model supports both proof-based trustless evaluation and trusted-attester policy evaluation. [6]
- Trust scoring is intentionally left to consumer policy; OMATrust does not prescribe a universal score. [7]

### 3.4 Proof and schema model

- Proof wrappers use `proofType` and `proofObject` core fields, with optional metadata fields. [6] [12]
- SDK/docs enumerate proof families including `pop-eip712`, `pop-jws`, `x402-receipt`, `x402-offer`, `evidence-pointer`, `tx-encoded-value`, `tx-interaction`. [11] [12] [24]
- JSON Schema Draft 2020-12 is treated as canonical, with generated EAS schema strings for on-chain usage. [14] [15]
- EAS schema docs explicitly note revocability policy differences (not all schema types revocable). [15]

### 3.5 API and SDK surfaces relevant to UM integration

- SDK package reference is `@oma3/omatrust` with module splits for reputation, identity, and app-registry. [10]
- Reputation SDK core flows include `listAttestations` and `verifyAttestation`. [4] [11] [12]
- Identity SDK includes DID normalization/parsing/helpers for `did:web` and `did:pkh` flows. [13]
- Controller Witness API and Delegated Attestation API are documented with concrete endpoint and payload contracts. [16] [17]

### 3.6 App Registry and ERC-8004 alignment

- App Registry is described as ERC-8004-compliant with OMA3 extensions. [18] [20] [25]
- Registry model includes DID identity, interface typing, metadata hash verification (`dataHash`), and versioned service representation. [18] [20]
- ERC-8004 extension effort is active; referenced PR is currently open (not merged) as of 2026-02-22. [25] [30]

### 3.7 Chain/deployment maturity signals

- Infrastructure pages describe OMAchain testnet as current and mainnet as planned; contract and infra details are marked subject to change. [26]
- Delegated attestation docs explicitly note mainnet delegated path is not yet enabled in the described flow. [17]

## 4) Documentation and maturity risks you should treat as real

### 4.1 Domain/documentation transition risk

- `docs.omatrust.org` currently serves a sitemap that points to `docs.oma3.org` pages. [32]
- Canonical URLs in docs pages resolve to `docs.oma3.org`. [2]

Risk implication:

- Integration docs in UM should track both domains until OMATrust settles on one stable canonical structure.

### 4.2 Placeholder documentation risk

- Several pages exist only as headers without substantive policy/procedure content (notably some operations pages and "other chains"). [33] [34] [35] [36]
- App Registry status page is mostly a preview warning, not a detailed maturity matrix. [23]

Risk implication:

- Some operational assumptions must remain provisional; do not model UM normative behavior on currently empty policy pages.

### 4.3 Preview/testnet risk

- Reputation and registry portals are preview/pre-alpha/testnet surfaces. [27] [28]
- App Registry docs repeatedly state non-production readiness. [18] [19] [23]

Risk implication:

- Integration should be and feature-flagged until OMATrust production posture is explicit.

## 5) Universal Manifest <-> OMATrust fit assessment

### 5.1 Strong fit areas

- Identity model fit: OMATrust uses DID-heavy identity (`did:web`, `did:pkh`), which maps cleanly into UM identity-neutral subject handling. [5] [13] [18] [20]
- Attestation model fit: OMATrust attestation envelopes/proofs are portable data objects that UM can carry as claims/pointers without forcing protocol lock-in. [6] [12] [14]
- Trust-policy fit: OMATrust explicitly separates validation from scoring, aligning with UM’s policy-layer concept. [7]

### 5.2 Medium-fit areas needing careful design

- Supersession/revocation semantics for review-like attestations must be represented explicitly in UM overlays to avoid stale-trust projection. [6] [9] [15]
- Mixed trust modes (proof-based vs trusted-attester) require explicit provenance labels in UM so downstream consumers do not over-assume trustlessness. [6] [7]

### 5.3 Low-fit / active-risk areas

- App Registry and some operations docs are still preview/partial; implementation interfaces may drift. [18] [23] [33] [34] [35]

## 6) Recommended UM integration architecture (inference from sources)

Inference: build a deep integration lane, but keep it until OMATrust production maturity signals improve.

### 6.1 Proposed UM integration lane

- Add a dedicated lane doc: `integrations/oma-trust.md`.
- Publish matching docs-site page under `site/src/content/docs/integrations/`.
- Add fixtures for:
  - Support-attestation chain (Linked Identifier + Key Binding + Controller Witness)
  - Proven and unproven User Review cases
  - Trusted-attester-only flows (Endorsement/Certification/Security Assessment)
  - Failure states (revoked, superseded, missing proof, bad proof type)

### 6.2 Proposed UM data mapping

- `omatrust.identity`
  - `subjectDid`, `linkedIds`, `keyBindings`, `controllerWitnesses`
- `omatrust.reputation`
  - `attestationType`, `attestationUid`, `schemaUid`, `issuedAt`, `effectiveAt`, `expiresAt`, `revocationState`
- `omatrust.proofs`
  - proof wrapper capture: `proofType`, `proofObject`, verification result, failure reasons
- `omatrust.policy`
  - `trustMode` (`proof-based` vs `trusted-attester`), local policy source, score derivation metadata

### 6.3 Resolver/consumer behavior

- Keep OMATrust overlays optional and freshness-scoped; do not let stale trust overlays outlive manifest cache windows by accident.
- Require explicit provenance fields when score-like outputs are derived from OMATrust signals (because OMATrust leaves scoring open to consumers). [7]

## 7) Implementation plan to integrate “to fullest potential”

### Phase 0: Governance and source control

- Create a new work order for OMATrust integration (recommended ID: `WO-0025`).
- Materialize OMATrust corpus into K2B ingestion ledger with selected/deferred/conflict decisions.
- Lock source-map entries to exact docs URLs + spec repo paths.

### Phase 1: Docs + fixtures

- Add OMATrust integration docs and constraints.
- Add fixture set (valid/invalid + lifecycle edge cases).
- Add docs-site pages linking integration to workbench/harness flows.

### Phase 2: Journey and verifier expansion

- Add journey lane (suggested `J11`) for OMATrust:
  - parse/validate OMATrust overlays
  - verify proof wrapper semantics
  - assert supersession/revocation behavior
  - assert trust-mode switching behavior

### Phase 3: Workbench and harness integration

- Add OMATrust preset manifests to Workbench fixture loader.
- Add Harness quick assertions for:
  - proofType coverage
  - attestation-type coverage
  - policy-mode projection correctness

### Phase 4: Production hardening

- Extend production smoke checks to include OMATrust integration docs pages and fixture availability.
- Add post-deploy drift checks for OMATrust integration routes/assets.

## 8) Decision recommendation

Recommendation: GO, but as a staged integration lane first.

Why:

- Conceptual compatibility is high.
- Ecosystem upside is high if OMA3 adoption proceeds.
- Maturity risk is manageable with feature-flagged, provenance-heavy integration.

## 9) Immediate next actions

1. Open and execute `WO-0025` (OMATrust integration lane).
2. Add OMATrust source-set into K2B ingestion and conflict tracking.
3. Implement Phase 1 docs+fixtures and Phase 2 journey proofs in one bounded execution batch.
4. Defer any “universal trust score” semantics to explicit local policy modules.

## 10) Sources

[1] https://www.omatrust.org/  
[2] https://docs.omatrust.org/  
[3] https://docs.omatrust.org/start-here/quickstart-publish  
[4] https://docs.omatrust.org/start-here/quickstart-verify  
[5] https://docs.omatrust.org/reputation/reputation-model  
[6] https://docs.omatrust.org/reputation/verification-flow  
[7] https://docs.omatrust.org/reputation/trust-scoring  
[8] https://docs.omatrust.org/reputation/consumer-workflow  
[9] https://docs.omatrust.org/reputation/issuer-workflow  
[10] https://docs.omatrust.org/sdk/getting-started  
[11] https://docs.omatrust.org/sdk/guides  
[12] https://docs.omatrust.org/sdk/api-reference/reputation-sdk  
[13] https://docs.omatrust.org/sdk/api-reference/identity-sdk  
[14] https://docs.omatrust.org/sdk/schemas/json-schemas  
[15] https://docs.omatrust.org/sdk/schemas/eas-schema-definitions  
[16] https://docs.omatrust.org/api/controller-witness  
[17] https://docs.omatrust.org/api/delegated-attestation  
[18] https://docs.omatrust.org/app-registry/overview  
[19] https://docs.omatrust.org/app-registry/registration-guide  
[20] https://docs.omatrust.org/app-registry/erc8004-compatibility  
[21] https://docs.omatrust.org/app-registry/registry-concepts  
[22] https://docs.omatrust.org/app-registry/registry-sdk-reference  
[23] https://docs.omatrust.org/app-registry/status  
[24] https://docs.omatrust.org/integrations/x402-integration  
[25] https://docs.omatrust.org/integrations/erc8004-integration  
[26] https://docs.omatrust.org/chain-architecture/omachain  
[27] https://preview.reputation.omatrust.org/  
[28] https://preview.registry.omatrust.org/  
[29] https://api.github.com/repos/oma3dao/omatrust-docs/contents/specification  
[30] https://api.github.com/repos/erc-8004/erc-8004-contracts/pulls/20  
[31] https://registry.npmjs.org/@oma3/omatrust  
[32] https://docs.omatrust.org/sitemap.xml  
[33] https://docs.omatrust.org/operations/versioning-policy  
[34] https://docs.omatrust.org/operations/governance-schema-control  
[35] https://docs.omatrust.org/operations/running-an-issuer  
[36] https://docs.omatrust.org/chain-architecture/other-chains

## 11) Evidence artifacts generated in this assessment run

- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-22-oma-link-coverage-evidence.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-22-omatrust-integration-assessment.md`
