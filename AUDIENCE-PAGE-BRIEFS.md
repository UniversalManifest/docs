# Audience Page Briefs

**Date:** 2026-04-24  
**Status:** Draft for approval  
**Purpose:** First-wave audience-page briefs for the approved Home-cluster sitemap.

This document defines the first audience pages to brief before public-site implementation resumes. These are not final page-copy drafts. They define audience role, route intent, required source grounding, links, and markdown/rendered parity requirements.

Source sitemap:

- `/Users/grig/work/repo/universalmanifest/docs/HOME-CLUSTER-SITEMAP.md`

Related copy briefs:

- `/Users/grig/work/repo/universalmanifest/docs/HOME-CLUSTER-COPY-BRIEFS.md`

## Audience Rules

- Audience pages must name real audiences, ecosystem groups, operator groups, implementer groups, or evaluator groups.
- Topic-only pages should live under use cases, integrations, proof, standards fit, or docs.
- Audience pages are downstream from the homepage and should not widen the global public navigation.
- Every audience page must link back to relevant use-case groups, `Scenario Explorer`, `Latest Spec`, and relevant proof/implementation surfaces.
- Every audience page must have a markdown/source counterpart and a bottom-page source link when implemented.
- Private facets, encrypted data, and attested identifier/control binding are cross-cutting capabilities. Weave them into the audience pages where they help the audience understand trust, privacy, or verification; do not create a new first-wave audience page for them unless a later IA decision reframes it around a real audience.

Bottom-page source block:

```text
Source
- Download Markdown
- View source
- Agent-readable entry
```

## First-Wave Audience Targets

1. Metaverse Portaling and Digital Worlds
2. EU Digital Identity and SSI
3. Platform Builders
4. Credential Issuers and Verifiers
5. Agent Builders
6. Payment and Wallet Builders

Not first-wave audience pages:

- `Venues and Spatial` - not approved as a standalone audience route.
- `Privacy and Consent` - remains a scenario / policy / proof theme unless reframed later for privacy officers, policy evaluators, or consent-system builders.
- `Credential and Personhood` - compatibility or rewrite candidate only; preferred audience label is `Credential Issuers and Verifiers`.

## Cross-Cutting Source Anchors

Private facets, encrypted data, and attested identifier/control binding should use these local sources:

- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-04-01-wo-0143-private-encrypted-inline-facets-vs-projection-adr.md`
- `/Users/grig/work/repo/universalmanifest/docs/explainers/facet-encryption-deep-dive.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/README.md`
- `/Users/grig/work/repo/universalmanifest/docs/VERSION-DIFFERENCES-V01-V02.md`
- `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/schema.json`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md`
- `/Users/grig/work/repo/universalmanifest/integrations/proof-of-personhood.md`
- `/Users/grig/work/repo/universalmanifest/integrations/did-vc.md`
- `/Users/grig/work/repo/universalmanifest/examples/v0.2/identity-binding-tier1-cross-did-binding.jsonld`

Public framing rule:

- projection is the normative private-data path
- encrypted inline facets are optional guidance for cryptographic confidentiality at rest
- `claims[].claimProof` and `identity.crossDidBinding` support Tier 1 attested/proof-backed claim and identifier binding in v0.2
- stronger cryptographic or multi-party common-control proofs must be framed as deferred or future-tier work unless a later source promotes them

## Brief 1: Metaverse Portaling and Digital Worlds

Preferred route:

- `/audiences/metaverse/`

Audience type:

- ecosystem / standards evaluator group

Reader question:

- "Can Universal Manifest support standards-oriented portaling between compatible digital worlds?"

Must communicate:

- This is the lead standards-oriented use case.
- A subject should be able to move between compatible worlds while carrying a portable envelope of identity references, avatar state, credential/DID references where relevant, consent/policy, content pointers, and other bounded state.
- The destination world should be able to project what it understands without requiring a bespoke world-to-world integration.
- IWPS and UM are complementary: IWPS defines the inter-world transport/negotiation/session layer, while UM defines the portable state payload that can travel through that portaling event.
- Spatial concepts are handled inside this broader digital-world portability frame, not as a separate venue/spatial audience.

Project source anchors:

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

Must avoid:

- narrow venue examples as the primary story
- implying one metaverse platform, one identity system, or one asset format is required
- implying UM replaces IWPS or IWPS replaces UM
- criticizing IWPS reserved/TBD areas instead of framing them as alignment points
- turning the page into a full technical implementation guide

Primary links:

- `/use-cases/`
- `/explorer/`
- `/how-it-works/`
- `/standards-fit/`
- `/spec/latest/`
- `/integrations/metaverse/`

Scenario Explorer lanes to surface:

- Metaverse Portaling and Digital-World Interoperability
- Platform Builders and Cross-System Interoperability
- Credential Issuers and Verifiers

Source/rendered parity target:

- markdown/source copy required before implementation
- rendered route target: `/audiences/metaverse/`
- bottom-page source link required

## Brief 2: EU Digital Identity and SSI

Preferred route:

- `/audiences/eu-ssi/`

Audience type:

- ecosystem / standards evaluator group

Reader question:

- "How could Universal Manifest complement EU digital identity, SSI, wallets, credentials, and public-sector/private-sector relying-party flows?"

Must communicate:

- This path is confirmed and must be grounded in public standards and public implementation direction.
- UM should be positioned as a complementary portable envelope around identity, credential, consent, pointer, and policy context.
- UM must not claim to replace EUDI Wallets, eIDAS, verifiable credentials, or national eID systems.
- UM can help carry surrounding portable context that a receiving system may need beyond a single credential exchange.
- Where relevant, UM can carry optional claim proof references, private-data handling policy, and disclosure constraints around wallet or relying-party flows without taking over the wallet's credential exchange protocol.

Public source anchors:

- European Commission, `Implementing regulation for European Digital Identity Wallets`  
  `https://digital-strategy.ec.europa.eu/en/library/implementing-regulation-european-digital-identity-wallets`
- EU Digital Identity Wallet Architecture and Reference Framework repository  
  `https://github.com/eu-digital-identity-wallet/eudi-doc-architecture-and-reference-framework`
- EUDI Wallet Standards and Technical Specifications repository  
  `https://github.com/eu-digital-identity-wallet/eudi-doc-standards-and-technical-specifications`
- European Commission, `Q&A Digital Identity`  
  `https://digital-strategy.ec.europa.eu/en/faqs/qa-digital-identity`

Must avoid:

- internal assumptions about unsupported standards
- claiming current support where the public ecosystem is still emerging
- vendor-specific wallet recommendations
- implying UM is a wallet replacement

Primary links:

- `/use-cases/`
- `/explorer/`
- `/standards-fit/`
- `/spec/latest/`
- `/integrations/did-vc/`
- `/conformance/`

Scenario Explorer lanes to surface:

- EU Digital Identity and SSI
- Credential Issuers and Verifiers
- Privacy, Consent, and Bounded Disclosure

Source/rendered parity target:

- markdown/source copy required before implementation
- rendered route target: `/audiences/eu-ssi/`
- bottom-page source link required

## Brief 3: Platform Builders

Preferred route:

- `/audiences/platforms/`

Audience type:

- implementer / operator group

Reader question:

- "Why would an app, service, marketplace, world, wallet, or platform team support Universal Manifest?"

Must communicate:

- Platform builders are trying to reduce custom handoff and integration cost.
- UM gives compatible systems a common portable envelope for identity-adjacent state, policy, pointers, and bounded validity.
- Platforms can adopt incrementally by reading the sections they understand and ignoring unknown fields safely.
- Platforms that need higher privacy or trust can layer in projections, optional encrypted inline facets, and proof-backed claim or identifier binding without requiring every consumer to implement the same depth on day one.

Must avoid:

- turning the page into enterprise-only copy
- implying every platform must use one shared backend
- treating the TypeScript helper as the only implementation path

Primary links:

- `/use-cases/`
- `/explorer/`
- `/how-it-works/`
- `/getting-started/`
- `/conformance/`
- `/workbench/`
- `/spec/latest/`

Scenario Explorer lanes to surface:

- Platform Builders and Cross-System Interoperability
- Metaverse Portaling and Digital-World Interoperability
- Peer-to-Peer Crypto Payments
- Agent-to-Agent Transactions

Source/rendered parity target:

- markdown/source copy required before implementation
- rendered route target: `/audiences/platforms/`
- bottom-page source link required

## Brief 4: Credential Issuers and Verifiers

Preferred route:

- `/audiences/credential-issuers-verifiers/`

Compatibility route:

- `/audiences/credential-and-personhood/` may remain only as a compatibility alias or rewritten page with the visible label `Credential Issuers and Verifiers`.

Audience type:

- role group

Reader question:

- "How can issuers, verifiers, and relying parties use UM around credential-bearing claims without turning UM into a credential standard?"

Must communicate:

- UM complements credential ecosystems.
- A manifest can carry or reference credential-bearing claims while also carrying consent, policy, pointers, identity references, and bounded validity.
- Credential-specific verification remains the responsibility of the relevant credential ecosystem.
- UM helps receiving systems understand surrounding context and disclosure policy.
- v0.2 includes optional `claims[].claimProof` support for Verifiable Presentation or attestation proof material.
- The `identity.crossDidBinding` convention can represent attested links between DIDs, including the source-grounded pattern for showing that a proof-of-personhood DID and another DID or manifest element are associated with the same subject.
- The audience page should distinguish attested Tier 1 binding from stronger cryptographic common-control proofs that are deferred to later trust tiers.

Must avoid:

- replacing VC, DID, or wallet standards
- treating proof of personhood as the whole audience
- naming individual credential providers as if they are endorsed

Primary links:

- `/use-cases/`
- `/explorer/`
- `/standards-fit/`
- `/integrations/did-vc/`
- `/integrations/proof-of-personhood/`
- `/conformance/`
- `/spec/latest/`

Scenario Explorer lanes to surface:

- Credential Issuers and Verifiers
- EU Digital Identity and SSI
- Privacy, Consent, and Bounded Disclosure

Project source anchors:

- `/Users/grig/work/repo/universalmanifest/docs/VERSION-DIFFERENCES-V01-V02.md`
- `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/schema.json`
- `/Users/grig/work/repo/universalmanifest/integrations/proof-of-personhood.md`
- `/Users/grig/work/repo/universalmanifest/integrations/did-vc.md`

Source/rendered parity target:

- markdown/source copy required before implementation
- rendered route target: `/audiences/credential-issuers-verifiers/`
- bottom-page source link required

## Brief 5: Agent Builders

Preferred route:

- `/audiences/agent-builders/`

Audience type:

- implementer / evaluator group

Reader question:

- "How can agents use manifests to understand identity, authority, consent, policy, and transaction context before acting?"

Must communicate:

- Agent-to-agent exchange needs portable, inspectable context.
- UM can help an agent receive a bounded envelope that says who/what the subject is, what authority or claims are relevant, what consent/policy applies, and what pointers or proof surfaces should be inspected.
- This should remain framework-neutral and protocol-neutral until a specific agent protocol or toolchain is approved.
- For higher-stakes agent decisions, copy should point to trust-tier evaluation, optional proof material, and consent/private-data boundaries rather than implying agents can blindly trust every manifest claim.

Must avoid:

- naming one agent framework as required
- claiming autonomous payment or action safety without proof
- turning agent-facing discovery into the same page as human audience copy

Primary links:

- `/use-cases/`
- `/explorer/`
- `/for-agents/`
- `/for-agents/external-agent-onboarding/`
- `/.well-known/universal-manifest.json`
- `/llms.txt`
- `/spec/latest/`

Scenario Explorer lanes to surface:

- Agent-to-Agent Transactions
- Platform Builders and Cross-System Interoperability
- Peer-to-Peer Crypto Payments
- Privacy, Consent, and Bounded Disclosure

Source/rendered parity target:

- markdown/source copy required before implementation
- rendered route target: `/audiences/agent-builders/`
- bottom-page source link required
- agent-readable entry link strongly recommended

## Brief 6: Payment and Wallet Builders

Preferred route:

- `/audiences/payment-and-wallet-builders/`

Audience type:

- implementer / operator group

Reader question:

- "How can Universal Manifest support portable context for peer-to-peer crypto payments without depending on an intermediary or one payment rail?"

Must communicate:

- The lane is about portable transaction context, consent/policy, payer/payee identifiers, claims where relevant, pointers, and bounded validity.
- Peer-to-peer crypto payment copy must stay abstract and provider-neutral.
- UM should not become a payment protocol, wallet, chain, escrow layer, or settlement engine.
- UM can help compatible systems understand the context around a payment or offer before a payment rail handles settlement.
- Higher-stakes payment contexts can require claim proof or attested identifier binding, while still leaving settlement and key custody outside UM.

Must avoid:

- naming a specific chain, offer protocol, wallet provider, or payment rail unless explicitly approved
- implying UM performs settlement
- implying an intermediary is required
- turning the page into financial advice

Primary links:

- `/use-cases/`
- `/explorer/`
- `/how-it-works/`
- `/standards-fit/`
- `/spec/latest/`
- `/conformance/`

Scenario Explorer lanes to surface:

- Peer-to-Peer Crypto Payments
- Agent-to-Agent Transactions
- Platform Builders and Cross-System Interoperability
- Privacy, Consent, and Bounded Disclosure

Source/rendered parity target:

- markdown/source copy required before implementation
- rendered route target: `/audiences/payment-and-wallet-builders/`
- bottom-page source link required

## Approval Checklist

- [ ] Approve Metaverse Portaling and Digital Worlds audience brief.
- [ ] Approve EU Digital Identity and SSI audience brief.
- [ ] Approve Platform Builders audience brief.
- [ ] Approve Credential Issuers and Verifiers audience brief.
- [ ] Approve Agent Builders audience brief.
- [ ] Approve Payment and Wallet Builders audience brief.
- [ ] Confirm whether Privacy/Consent remains only a scenario/policy/proof theme for now.
- [ ] Confirm compatibility treatment for `/audiences/credential-and-personhood/`.
- [ ] Confirm compatibility treatment for `/audiences/venues-and-spatial/`.
