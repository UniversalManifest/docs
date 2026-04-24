# Home-Cluster Copy Briefs

**Date:** 2026-04-24  
**Status:** Draft for approval  
**Purpose:** Copy briefs for the approved `Home` cluster sitemap before public-site rewriting resumes.

This document is a brief, not final page copy. It defines what each page must do, what it must avoid, which routes it should hand off to, and how markdown/source fidelity must be preserved when implementation resumes.

## Approved IA Inputs

- Global navigation: `Home`, `Latest Spec`
- `/explorer/` visible label: `Scenario Explorer`
- Approved `Scenario Explorer` lanes:
  1. Metaverse Portaling and Digital-World Interoperability
  2. EU Digital Identity and SSI
  3. Platform Builders and Cross-System Interoperability
  4. Credential Issuers and Verifiers
  5. Agent-to-Agent Transactions
  6. Peer-to-Peer Crypto Payments
  7. Privacy, Consent, and Bounded Disclosure
- Secondary/support pages, not canonical first-contact pages:
  - `/about/why-um/`
  - `/about/one-pager/`
  - `/about/standards-landscape/`

Source sitemap:

- `/Users/grig/work/repo/universalmanifest/docs/HOME-CLUSTER-SITEMAP.md`

## Copy System Rules

- Lead with concrete reader understanding, not internal site architecture.
- Use `Scenario Explorer`, not bare `Explorer`, in visible copy.
- Do not use standalone venue/spatial framing as a top-level public lane.
- Do not name a specific chain, offer protocol, wallet provider, or payment rail in peer-to-peer crypto payment copy unless explicitly approved.
- Ground EU digital identity / SSI claims in public standards, public specifications, architecture references, or public implementation direction.
- Treat private facets, encrypted data, and attested identifier/control binding as cross-cutting material inside the approved credential/verifier, privacy, how-it-works, and standards-fit surfaces unless a later IA decision creates a separate lane.
- Do not overclaim v0.2 identity binding: `claims[].claimProof` and `identity.crossDidBinding` support Tier 1 attested or proof-backed verification; stronger cryptographic or multi-party binding tiers are deferred.
- Do not overclaim encryption as mandatory core behavior: projection is the normative private-data path, while encrypted inline facets are optional guidance that can provide cryptographic confidentiality at rest.
- Every implemented canonical page must have a markdown/source counterpart and a bottom-page source link.

Reusable bottom-page source block:

```text
Source
- Download Markdown
- View source
- Agent-readable entry
```

Implementation handoff checklist:

- markdown/source copy exists
- rendered page uses the approved copy direction
- bottom-page source link exists
- machine-readable and agent-facing references checked
- compatibility aliases checked

## Public Source Anchors For EU Digital Identity / SSI

Use these as public grounding sources for the EU digital identity path:

- European Commission, `Implementing regulation for European Digital Identity Wallets`  
  `https://digital-strategy.ec.europa.eu/en/library/implementing-regulation-european-digital-identity-wallets`
- EU Digital Identity Wallet Architecture and Reference Framework repository  
  `https://github.com/eu-digital-identity-wallet/eudi-doc-architecture-and-reference-framework`
- EUDI Wallet Standards and Technical Specifications repository  
  `https://github.com/eu-digital-identity-wallet/eudi-doc-standards-and-technical-specifications`
- European Commission, `Q&A Digital Identity`  
  `https://digital-strategy.ec.europa.eu/en/faqs/qa-digital-identity`

## Project Source Anchors For Metaverse Portaling / IWPS

Use these as source grounding for metaverse portaling and the Inter-World Portaling System relationship:

- IWPS Base Specification v0.3 localized reference  
  `/Users/grig/work/repo/universalmanifest/docs/research/iwps-base-specification-v0.3.md`
- IWPS–Universal Manifest alignment analysis  
  `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-11-iwps-um-alignment-analysis.md`
- OMA3 handout, `IWPS + UM: The Complete Portaling Stack`  
  `/Users/grig/work/repo/universalmanifest/docs/handouts/oma3-2026-03-12/07-iwps-integration.md`
- Metaverse portaling integration note  
  `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-metaverse-portaling-integration-note.md`
- Metaverse Portaling and Digital-Worlds content pack  
  `/Users/grig/work/repo/universalmanifest/docs/reports/2026-04-22-metaverse-portaling-and-digital-worlds-content-pack.md`
- Metaverse integration lane  
  `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`

Portaling copy should frame IWPS and UM as complementary layers:

- IWPS handles the portaling transport: Query, Teleport, capability negotiation, communication path, and session binding.
- UM handles the portable state envelope: identity references, consent/policy, facets, pointers, credentials/claims where relevant, validity windows, and integrity.
- UM should not be framed as replacing IWPS.
- IWPS should not be criticized for its reserved/TBD areas; those are collaboration points where UM can supply the portable-state payload.

## Project Source Anchors For Private Facets, Encryption, And Attested Binding

Use these as source grounding for private-data handling, encrypted facets, and attested identifier/control binding:

- Private data handling ADR, projection plus encrypted inline facets  
  `/Users/grig/work/repo/universalmanifest/docs/reports/2026-04-01-wo-0143-private-encrypted-inline-facets-vs-projection-adr.md`
- Facet privacy explainer  
  `/Users/grig/work/repo/universalmanifest/docs/explainers/facet-encryption-deep-dive.md`
- v0.2 private data handling model  
  `/Users/grig/work/repo/universalmanifest/spec/v0.2/README.md`
- v0.2 identity-binding and Bag of Claims delta  
  `/Users/grig/work/repo/universalmanifest/docs/VERSION-DIFFERENCES-V01-V02.md`
- v0.2 decision record for tiered trust, `claimProof`, and `identity.crossDidBinding`  
  `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
- v0.2 schema field for optional `claims[].claimProof`  
  `/Users/grig/work/repo/universalmanifest/spec/v0.2/schema.json`
- v0.2 conformance guidance for encrypted facets and Tier 1 claimed conformance  
  `/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md`
- Proof-of-personhood integration examples for attested cross-DID binding  
  `/Users/grig/work/repo/universalmanifest/integrations/proof-of-personhood.md`
- DID + VC integration examples for `claimProof`  
  `/Users/grig/work/repo/universalmanifest/integrations/did-vc.md`
- Tier 1 identity-binding fixture  
  `/Users/grig/work/repo/universalmanifest/examples/v0.2/identity-binding-tier1-cross-did-binding.jsonld`
- Encrypted inline facet examples  
  `/Users/grig/work/repo/universalmanifest/examples/v0.2/encrypted-inline-facets/manifest-encrypted-inline-facet-initial.jsonld`
  `/Users/grig/work/repo/universalmanifest/examples/v0.2/encrypted-inline-facets/manifest-encrypted-inline-facet-key-rotation.jsonld`
  `/Users/grig/work/repo/universalmanifest/examples/v0.2/encrypted-inline-facets/manifest-encrypted-inline-facet-revocation.jsonld`

Copy should keep the concepts separate:

- Private data handling: projection is normative; encrypted inline facets are optional guidance for cryptographic confidentiality at rest.
- Encrypted facets: the manifest envelope can stay readable and signature-verifiable while sensitive facet payloads remain unreadable to consumers without keys.
- Attested identifier/control binding: v0.2 can surface proof material that a claim, DID, or identifier relationship is attested to the manifest subject, including proof-of-personhood DID binding examples. Public copy should avoid saying this is absolute ownership proof unless the relevant proof tier and verification path are stated.

## Brief 1: Overview

Route:

- `/`

Page role:

- first-contact explanation and routing

Reader question:

- "What is Universal Manifest, and where should I go next?"

Primary audience:

- first-time human readers
- standards evaluators who need a quick orientation before the spec
- implementers who need the plain-language object before implementation detail

Must communicate:

- Universal Manifest is a portable document/envelope for identity references, claims, consents, policies, pointers, and related state between compatible systems.
- The problem is fragmented context: identity, consent, credentials, and permissions do not travel cleanly across systems.
- UM does not replace every wallet, database, credential standard, blockchain, or runtime.
- The spec remains one click away through `Latest Spec`.

Must include:

- one plain definition
- 2 to 4 concrete scenario summaries
- at least one metaverse portaling scenario grounded in the IWPS + UM relationship
- at least one EU digital identity / SSI scenario
- at least one agent transaction or peer-to-peer payment scenario
- at least one privacy / bounded-disclosure signal that can mention private facets, encrypted data, or attested binding without turning the homepage into a security explainer
- primary CTA to `/use-cases/`
- secondary CTA to `/spec/latest/`
- limited audience links only

Must avoid:

- long standards comparison
- giant audience taxonomy
- implementation checklists
- repeated "spec is one click away" language
- internal wording about the homepage mandate

CTA hierarchy:

- primary: `/use-cases/` - `Browse Use Cases`
- secondary: `/spec/latest/` - `Read Latest Spec`
- tertiary only if needed: `/explorer/` - `Open Scenario Explorer`

Source/rendered parity target:

- canonical markdown/source copy should be created before implementation
- rendered route target: `/`
- bottom-page source link required

## Brief 2: Use Cases

Route:

- `/use-cases/`

Page role:

- narrative scenario-family overview

Reader question:

- "Where would Universal Manifest matter in the real world?"

Primary audience:

- first-time readers who understand the basic object
- strategic evaluators looking for the right adoption lane
- implementers looking for practical problem families

Must communicate:

- Use cases are the bridge between first-contact explanation and deeper inspection.
- The page is narrative and scannable.
- The `Scenario Explorer` is the next step for lane-by-lane inspection.

Approved scenario groups:

1. metaverse portaling and digital-world interoperability
2. EU digital identity / SSI / credential wallets
3. platform builders and cross-system interoperability
4. credential issuers and verifiers
5. agent-to-agent transactions
6. peer-to-peer crypto payments
7. privacy, consent, and bounded disclosure

Cross-cutting material to weave into the groups:

- private facets and encrypted data belong primarily in `Privacy, Consent, and Bounded Disclosure`, with light references in `How It Works`
- attested identifier/control binding, `claimProof`, proof-of-personhood DID binding, and `identity.crossDidBinding` belong primarily in `Credential Issuers and Verifiers`, with related references in `EU Digital Identity and SSI`, `Agent-to-Agent Transactions`, and `Peer-to-Peer Crypto Payments` when trust context matters

Must include for each group:

- the concrete fragmentation problem
- what UM carries or points to
- who cares about the scenario
- the best next route
- public standards, protocols, or interoperability context where relevant

Must avoid:

- turning every group into an audience page
- turning every group into an explorer lane
- detailed implementation steps
- provider-specific payment copy

CTA / handoff model:

- `/explorer/` for deeper scenario inspection
- `/audiences/*` for role/ecosystem framing
- `/docs/`, `/integrations/`, `/conformance/`, `/sandbox/`, or `/workbench/` only after the scenario is clear

Source/rendered parity target:

- canonical markdown/source copy should be created before implementation
- rendered route target: `/use-cases/`
- bottom-page source link required

## Brief 3: Scenario Explorer

Route:

- `/explorer/`

Visible label:

- `Scenario Explorer`

Page role:

- lane-by-lane scenario inspection after use-case context

Reader question:

- "What happens in this scenario, what travels, and what proof or spec surface backs it?"

Primary audience:

- readers who already understand the scenario space
- standards evaluators comparing applicability
- implementers deciding where UM fits

Must communicate:

- This is not a generic concept explorer.
- This is not the sandbox.
- This is not a route family for every possible lane.
- The first release should favor fewer strong lanes over many thin lanes.

Approved lane order:

1. Metaverse Portaling and Digital-World Interoperability
2. EU Digital Identity and SSI
3. Platform Builders and Cross-System Interoperability
4. Credential Issuers and Verifiers
5. Agent-to-Agent Transactions
6. Peer-to-Peer Crypto Payments
7. Privacy, Consent, and Bounded Disclosure

Lane copy requirements:

- exact lane headline
- concrete scenario steps
- why UM fits
- what actually travels
- what remains authoritative elsewhere
- consent/policy/freshness considerations
- proof/spec links
- audience links

Special lane constraints:

- Metaverse portaling should include a standards-oriented example grounded in IWPS where a subject moves between compatible worlds. IWPS should provide the transport/negotiation/session layer, while UM provides the portable state payload: avatar state, identity references, credential/DID references where relevant, consent/policy, content pointers, and portable state the destination can project.
- EU digital identity / SSI must cite or align with public EUDI Wallet / eIDAS / ARF / standards-and-technical-specification direction.
- Credential issuers and verifiers should surface `claims[].claimProof`, Verifiable Presentation or attestation proof material, proof-of-personhood DID binding examples, and `identity.crossDidBinding` as Tier 1-style identity/claim authenticity tools. Do not present these as mandatory conformance requirements or as stronger cryptographic common-control proofs than the v0.2 source material supports.
- Agent-to-agent transactions should stay framework-neutral.
- Peer-to-peer crypto payments should stay provider-neutral and intermediary-free.
- Privacy/consent should preserve default-deny and bounded-disclosure framing, including projection and optional encrypted inline facets as complementary private-data paths.

Must avoid:

- standalone venue/spatial top-level framing
- naming specific chains, offer protocols, wallet providers, or payment rails in payment copy unless approved
- making `/explorer/` sound like `/tools/concept-explorer/`

Source/rendered parity target:

- canonical markdown/source copy should be created before implementation
- rendered route target: `/explorer/`
- bottom-page source link required
- lane content should be source-addressable for agents where possible

## Brief 4: How It Works

Route:

- `/how-it-works/`

Page role:

- conceptual model explanation

Reader question:

- "What is the shape of the thing, and how does it move between systems?"

Primary audience:

- readers who have seen use cases and need the mental model
- implementers before they read the spec
- standards evaluators before standards comparison

Must communicate:

- UM is the portable envelope, not the whole system.
- It can carry identity references, records/facets, claims, consents, policies, pointers, and validity windows.
- Large or authoritative data can stay outside the manifest.
- Receivers project only what they understand and are allowed to use.
- Private data can be handled through consumer-specific projections and, where an adopter needs cryptographic confidentiality at rest, optional encrypted inline facets.
- Claims and DID relationships can carry optional proof material or attested binding conventions, but relying parties still decide what trust tier is sufficient.
- The same model can support human, agent-mediated, peer-to-peer, and standards-oriented exchange without requiring one runtime.

Must include:

- envelope model
- records / facets / claims / consents
- pointers and authoritative sources
- consent and policy
- private facets, projection, and optional encrypted inline facets
- claim authenticity, `claimProof`, cross-DID binding, and trust-tier boundaries
- issued/expires validity window and bounded trust
- optional runtime/resolver context

Must avoid:

- dense normative spec prose
- standards-comparison tables
- implementation checklists
- implying `myum.net`, one wallet, one blockchain, or one agent framework is required

CTA / handoff model:

- `/standards-fit/` for adjacent standards
- `/spec/latest/` for the normative contract
- `/getting-started/` for implementation orientation

Source/rendered parity target:

- canonical markdown/source copy should be created before implementation
- rendered route target: `/how-it-works/`
- bottom-page source link required

## Brief 5: Standards Fit

Route:

- `/standards-fit/`

Page role:

- canonical standards-comparison and ecosystem-boundary surface

Reader question:

- "How does UM relate to the standards and protocols I already know?"

Primary audience:

- standards evaluators
- ecosystem architects
- implementers comparing UM to adjacent standards

Must communicate:

- UM is not a replacement for every adjacent standard.
- UM is a portable pointer-and-policy envelope that can compose with identity, credential, storage, messaging, resolver, payment, agent, and projection systems.
- EU digital identity / SSI claims must be grounded in public standards or public implementation direction.
- `/about/standards-landscape/` is secondary/supporting, not the canonical public positioning page.

Must include:

- credentials and verifiable claims
- identity and subject identifiers
- claim proof, attested identifier binding, and proof-of-personhood binding examples
- consent and policy signals
- private data handling, projection, encrypted inline facets, and selective disclosure context
- storage and pointer-based data access
- messaging / exchange / projection
- agent transaction context
- peer-to-peer payment and settlement context
- runtime / resolver context
- conformance and proof posture

Must avoid:

- product marketing copy
- first-contact persuasion
- implementation tutorials
- overclaiming support for standards that are still emerging

CTA / handoff model:

- `/spec/latest/`
- `/spec/v01/`
- `/spec/v02/`
- `/conformance/`
- `/integrations/`
- `/reference/resolver-api/`

Source/rendered parity target:

- canonical markdown/source copy should be created before implementation
- rendered route target: `/standards-fit/`
- bottom-page source link required

## Approval Checklist

- [ ] Approve Overview copy brief.
- [ ] Approve Use Cases copy brief.
- [ ] Approve Scenario Explorer copy brief.
- [ ] Approve How It Works copy brief.
- [ ] Approve Standards Fit copy brief.
- [ ] Confirm markdown/source file paths for actual copy before implementation.
- [ ] Confirm bottom-page source-link pattern before implementation.
