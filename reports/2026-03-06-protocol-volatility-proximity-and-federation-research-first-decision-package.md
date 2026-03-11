# Protocol Volatility, Proximity Credentials, and Federation Bridges — Research-First Decision Package

Date: 2026-03-06  
Project: Universal Manifest (`/Users/grig/work/repo/universalmanifest`)  
Work order: `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0132-research-first-protocol-volatility-proximity-and-federation-gaps.md`

## 1) Purpose and outcome

This report closes the first Research-First pass for the unresolved topics surfaced by the newly localized source corpus.

It answers four questions:

- what is already covered well enough to keep as current guidance,
- what remains only partially covered,
- what is still a real gap,
- and what promotion gates must be met before any of these topics are presented as stronger integration guidance or normative candidates.

This is not a protocol-selection memo. It is a decision package that prevents accidental lock-in.

## 2) Executive judgment

Direct answer:

- Universal Manifest already has the correct high-level architecture for these topics: pointer-first, storage-neutral, subject-controlled runtime, and bridge adapters as implementation detail.
- Universal Manifest does **not** yet have a complete, implementation-safe answer for all three unresolved topics.
- The correct next move is mixed:
  - keep current non-locking guidance where the architecture is already clear,
  - run targeted Research-First work before claiming a preferred protocol family for volatile credential ecosystems,
  - do not introduce new core-schema obligations yet.

Current classification:

- `protocol volatility and recommendation boundaries` -> `PARTIAL`
- `proximity-aware credential presentation` -> `GAP`
- `federation and bridge strategy` -> `PARTIAL`

Safe to say now:

- UM can carry pointers, consent state, verification metadata, and projection hints for all three areas.
- UM should remain agnostic about the underlying credential, transport, storage, and federation substrates.
- Subject-side runtime state is the right place to mediate live consent and transport-specific behavior.

Not safe to say now:

- that UM has selected a preferred DID method, VC profile, proof stack, proximity transport, or federation substrate,
- that proximity presentation semantics belong in the UM core contract,
- that closed/open surface bridge behavior has one recommended protocol stack today.

## 3) Inputs used for this decision package

### 3.1 Newly localized corpus

Primary localized sources:

- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-25-user-centric-pointer-protocols-2025-landscape.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-26-universal-manifest-architectures-comprehensive-analysis.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-27-peermesh-universal-manifest-vision.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-28-hot-grid-manifest-note.md`

### 3.2 Existing in-repo coverage checked in this pass

- `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md`
- `/Users/grig/work/repo/universalmanifest/integrations/reference-runtime.md`
- `/Users/grig/work/repo/universalmanifest/integrations/did-vc.md`
- `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`
- `/Users/grig/work/repo/universalmanifest/docs/guides/MUM-SYNCHRONIZATION-PROFILE.md`
- `/Users/grig/work/repo/universalmanifest/research/federation/universal-manifest-workstream.md`
- `/Users/grig/work/repo/universalmanifest/research/reference-platform/profile-architecture.md`
- `/Users/grig/work/repo/universalmanifest/research/reference-platform/interoperability-sync.md`
- `/Users/grig/work/repo/universalmanifest/docs/design/PERMISSIONS-FIREWALL-DESIGN.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-05-portable-identity-profile-go-now-research-first-execution-plan.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-05-metaverse-universal-manifest-go-now-research-first-execution-plan.md`

### 3.3 Current standards checkpoints verified in this pass

The following current official or primary-source references were checked because these ecosystems are time-volatile:

- W3C DID Core: [https://www.w3.org/TR/did-core/](https://www.w3.org/TR/did-core/)
- W3C Verifiable Credentials Data Model 2.0: [https://www.w3.org/TR/vc-data-model-2.0/](https://www.w3.org/TR/vc-data-model-2.0/)
- W3C Verifiable Credential Data Integrity 1.0: [https://www.w3.org/TR/vc-data-integrity/](https://www.w3.org/TR/vc-data-integrity/)
- OpenID for Verifiable Presentations 1.0 final: [https://openid.net/specs/openid-4-verifiable-presentations-1_0.html](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html)
- OpenID for Verifiable Credential Issuance 1.0 final: [https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html)
- IETF SD-JWT VC draft: [https://datatracker.ietf.org/doc/draft-ietf-oauth-sd-jwt-vc/](https://datatracker.ietf.org/doc/draft-ietf-oauth-sd-jwt-vc/)
- W3C Digital Credentials API Working Draft: [https://www.w3.org/TR/digital-credentials/](https://www.w3.org/TR/digital-credentials/)
- Solid Protocol Editor's Draft: [https://solidproject.org/TR/protocol](https://solidproject.org/TR/protocol)
- Decentralized Web Node specification: [https://identity.foundation/decentralized-web-node/spec/](https://identity.foundation/decentralized-web-node/spec/)
- AT Protocol sync documentation: [https://atproto.com/specs/sync](https://atproto.com/specs/sync)
- OpenID Federation 1.0 final approval notice: [https://openid.net/2025/06/06/openid-federation-1-0-approved-as-final-specification/](https://openid.net/2025/06/06/openid-federation-1-0-approved-as-final-specification/)

Inference from those sources:

- core identity and credential models are stable enough to reference at the standards-family level,
- transport, selective-disclosure, browser/OS wallet mediation, and federation substrate selection are still active choice surfaces,
- therefore UM should keep naming protocol families carefully and avoid hard recommendations without explicit promotion evidence.

## 4) Crosswalk: what UM already covers vs what is still open

### 4.1 Protocol volatility and recommendation boundaries

Current repo coverage:

- `integrations/did-vc.md` now explicitly states that DID methods, VC profiles, and toolchains are examples, not an endorsed shortlist.
- `docs/PROJECT-VISION.md` and `integrations/reference-runtime.md` now anchor the architecture in a composite stack so credential systems are clearly one layer, not the whole solution.
- Prior reports already identified selective disclosure and proof-family choice as a Research-First topic.

What this means:

- UM already has the correct boundary language.
- UM does **not** yet have a maintained recommendation policy for when a protocol family can be named more strongly than “example”.

Classification:

- `PARTIAL`

Why it is not closed:

- A bounded caveat is not the same thing as an explicit recommendation-governance model.
- The project has no current standards-currency matrix, no review cadence for named examples, and no promotion threshold for moving from generic references to implementation guidance.

### 4.2 Proximity-aware credential presentation

Current repo coverage:

- Existing docs mention consent-gated disclosure, subject-side runtime authority, and external proof pointers.
- The PIP and MUM execution plans already flagged selective disclosure and adjacent proof transport work as Research-First.
- There is no dedicated UM document that explains how proximity-triggered credential presentation should work across same-device, cross-device, QR, NFC, BLE, or browser/OS wallet mediation patterns.

What current standards checkpoints indicate:

- OpenID4VP is now final and explicitly relevant to presentation exchange.
- W3C Digital Credentials API is active, but still a Working Draft, so browser-mediated presentation behavior remains an evolving surface.
- SD-JWT VC is still an IETF draft, which means selective-disclosure and wallet/verifier expectations are not yet a closed field.

Classification:

- `GAP`

Why it is not closed:

- UM currently has no profile describing what belongs in the manifest versus what belongs in the external request/presentation protocol.
- There is no fixture, journey, or integration lane that proves proximity-triggered exchange behavior.

### 4.3 Federation and bridge strategy

Current repo coverage:

- `docs/PROJECT-VISION.md` and `integrations/reference-runtime.md` now explicitly allow subject-controlled runtimes and bridge adapters.
- `research/federation/universal-manifest-workstream.md` and `research/reference-platform/interoperability-sync.md` already capture substantial prior thinking about user-controlled storage, synchronization, relays, and federated propagation.
- `docs/guides/MUM-SYNCHRONIZATION-PROFILE.md` partially covers staleness, change-log, and authoritative-source behavior.

What current standards checkpoints indicate:

- Solid remains important conceptually, but its protocol is still Editor's Draft status.
- DWN remains an active specification surface rather than a closed industry baseline.
- AT Protocol has a defined sync model, but it is not a drop-in answer for UM's general bridge problem.
- OpenID Federation is real and relevant for trust federation, but it does not solve subject-state portability across arbitrary surfaces.

Classification:

- `PARTIAL`

Why it is not closed:

- UM still lacks a standards-neutral bridge strategy memo that says exactly how to evaluate open-network, wallet-mediated, and closed-surface adapters without accidentally selecting a canonical substrate.
- Current material is strong on architecture direction but weaker on decision criteria.

## 5) Topic-by-topic decision package

## 5.1 Topic A — Protocol volatility and recommendation boundaries

### Overlap with current UM work

UM already overlaps correctly with current identity standards in one narrow sense:

- UM can carry identifiers, pointers, verification metadata, and consent state.
- UM can reference proof material or credential status resources.
- UM does not need to embed a single identity stack in order to be useful.

### Gap in current UM work

What is missing is not document structure. What is missing is governance:

- when a protocol family is stable enough to name,
- how often named examples are rechecked,
- and what evidence is required before a named example becomes recommended guidance.

### Replacement question

Should any current UM concept be replaced by a standards-family concept here?

Answer:

- No core UM concept should be replaced.
- The correct move is to add a stricter recommendation policy around examples, not to collapse UM into DID/VC/OIDC-specific language.

### Can this be integrated directly as a facet?

Answer:

- No.
- Volatility governance is not a facet concern. It is a documentation and promotion-governance concern.
- At most, manifests carry pointers or claims that happen to use a volatile upstream protocol family.

### Recommended position now

- Keep current DID/VC lane language non-locking.
- Explicitly treat named methods and profiles as examples until they pass project-level promotion gates.
- Add a standards-currency review artifact before any stronger recommendation is made.

### Promotion gate

Promote a protocol family from `example only` to `recommended guidance` only when all of the following are true:

1. The underlying specification is final or equivalent-stability, or there is a documented reason to accept a draft.
2. There are at least two independent implementation ecosystems or production-grade stacks to reduce single-vendor risk.
3. UM has at least one fixture or journey showing how the protocol attaches without changing core UM behavior.
4. The threat-model and revocation/freshness implications are documented.
5. A dated standards-currency review has been recorded in repo documentation.

### Human example

Example application:

- A retail verifier wants an age-over-threshold proof.
- UM should carry a pointer or claim hook for a proof artifact and the consent state for disclosure.
- The proof itself may currently use SD-JWT VC, a data-integrity VC, or another external presentation format.
- UM documentation should not say “use SD-JWT VC” until the promotion gate above is satisfied.

## 5.2 Topic B — Proximity-aware credential presentation

### Overlap with current UM work

UM already covers some of the surrounding pieces:

- subject-side consent mediation,
- pointer-first references to proofs or policies,
- separation between document state and live transport behavior,
- external-wallet/runtime authority for current state.

### Gap in current UM work

UM has no explicit answer yet for:

- whether proximity presentation is same-device, cross-device, or device-to-device,
- how request intent is represented,
- how transport-specific details are kept out of UM core semantics,
- what evidence is required before saying a proximity flow is “supported”.

### Replacement question

Should proximity behavior replace existing UM consent or pointer concepts?

Answer:

- No.
- Proximity is not a replacement for consent or pointers.
- It is a transport and presentation context that may consume UM policy state.

### Can this be integrated directly as a facet?

Answer:

- Not as a primary design.
- A manifest may carry request-policy pointers, verifier preferences, or audit references related to a proximity flow.
- The live proximity exchange itself belongs to the presentation protocol and runtime layer, not to a static facet.

### Recommended position now

- Keep proximity as an external presentation context.
- Define a non-normative boundary profile that says what UM can supply to a proximity flow:
  - verifier or relying-party policy pointer,
  - consent scope,
  - freshness expectations,
  - proof-result or audit pointer.
- Do not put QR/NFC/BLE/browser-wallet mechanics into the UM core contract.

### Promotion gate

Promote proximity guidance from `gap` to `published integration guidance` only when all of the following are true:

1. The profile clearly separates UM document content from the live presentation protocol.
2. At least one same-device and one cross-device flow have been mapped to the same boundary model.
3. There is executable evidence in fixtures and/or journeys showing a relying party requesting proof through a runtime without embedding transport specifics into UM.
4. The privacy and anti-correlation risks are documented.
5. The guidance references current official standards checkpoints for the transport/presentation family it depends on.

### Human example

Example application:

- A venue entrance kiosk requests proof that a visitor is of legal age.
- The visitor's phone or wallet runtime handles the QR/NFC/BLE or browser-mediated presentation exchange.
- The UM document provides the policy context, allowed disclosure scope, and optional proof-result pointer.
- The UM document does not itself become the transport envelope for the live credential presentation.

## 5.3 Topic C — Federation and bridge strategy

### Overlap with current UM work

UM already has the correct architectural posture:

- subject-controlled source of truth,
- pointer-first references to external systems,
- projection into consuming surfaces,
- adapters for closed or constrained environments,
- synchronization and freshness checks as separate concerns.

### Gap in current UM work

What remains unresolved is the comparison and selection layer:

- when to use open-network sync versus adapter-style push,
- what makes a storage or federation substrate “good enough” for UM guidance,
- how to describe bridge behavior without accidentally making Solid, DWN, AT Protocol, or any other substrate look normative.

### Replacement question

Should federation/bridge standards replace UM runtime concepts?

Answer:

- No.
- The subject-controlled runtime and adapter model remain the right umbrella abstraction.
- External storage or federation systems should be treated as attachable substrates, not as the definition of UM itself.

### Can this be integrated directly as a facet?

Answer:

- No, not as the primary solution.
- Facets may describe public-profile projections, social handles, canonical-source pointers, or change-log references.
- Federation semantics, relay behavior, and bridge contracts remain runtime/integration concerns.

### Recommended position now

- Keep the current composite-stack and bridge-adapter framing.
- Create a standards-neutral decision package that compares substrate families by role:
  - canonical private state,
  - public projection,
  - trust federation,
  - live relay/sync,
  - closed-surface automation or import/export bridge.
- Publish criteria, not endorsements, unless a substrate passes a later promotion gate.

### Promotion gate

Promote a federation/bridge pattern from `partial` to `recommended guidance` only when all of the following are true:

1. The pattern is described by role rather than by vendor alone.
2. The source-of-truth model, refresh model, and failure modes are explicit.
3. UM has at least one example or journey proving pointer-first and consent-first behavior across the bridge.
4. Closed-surface handling is clearly marked as implementation detail.
5. The pattern can be explained without making any external substrate appear required for UM conformance.

### Human example

Example application:

- A creator keeps canonical state in a subject-controlled runtime.
- The runtime exposes selected public references through one open storage substrate, pushes social projection to a federated surface, and exports a reduced view into a closed game or commerce platform.
- UM remains the portable state layer and policy envelope; the bridge mechanisms stay outside the core contract.

## 6) Source disposition after this Research-First pass

### `external-25-user-centric-pointer-protocols-2025-landscape.md`

Disposition:

- already used correctly to drive `WO-0130`, `WO-0131`, and this report.
- still produces follow-on research work on protocol recommendation governance and bridge-strategy comparison.

### `external-26-universal-manifest-architectures-comprehensive-analysis.md`

Disposition:

- already used correctly to drive the composite-stack architecture clarification.
- still produces follow-on research work on multi-substrate bridge criteria.

### `external-27-peermesh-universal-manifest-vision.md`

Disposition:

- already used correctly to strengthen the active-runtime direction.
- still produces follow-on research work on subject-controlled runtime plus adapter boundaries.

### `external-28-hot-grid-manifest-note.md`

Disposition:

- no further execution work required beyond provenance and archive accounting.
- retain only as a recorded source-disposition artifact.

## 7) Follow-on work recommended

This report recommends three explicit follow-on work orders.

### Recommended follow-on 1

Title:

- `Protocol Recommendation Governance and Standards Currency Matrix`

Reason:

- the repo needs a reusable mechanism for deciding when protocol examples move from “named example” to “recommended guidance”.

### Recommended follow-on 2

Title:

- `Proximity Credential and Presentation Profile Assessment`

Reason:

- proximity flows are the clearest remaining practical gap between runtime ambition and integration-safe documentation.

### Recommended follow-on 3

Title:

- `Federation and Bridge Strategy Decision Package`

Reason:

- the repo has strong architecture fragments but still needs a standards-neutral comparison and evaluation framework for attachable substrates and closed-surface bridges.

## 8) Final conclusion

The newly localized source wave did not reveal a missing core UM concept.

It did reveal three areas where project discipline matters:

- naming volatile upstream protocol families carefully,
- keeping live proximity presentation out of the core document model,
- and describing federation and bridge behavior as attachable runtime strategy rather than as core UM semantics.

That means the right answer is not a schema rewrite.

The right answer is:

- preserve the composite-stack and active-runtime direction,
- keep current guidance non-locking,
- and promote only those protocol-specific patterns that pass explicit evidence and stability gates.
