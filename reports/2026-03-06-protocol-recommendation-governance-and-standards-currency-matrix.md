# Protocol Recommendation Governance and Standards Currency Matrix

Date: 2026-03-06  
Project: Universal Manifest (`/Users/grig/work/repo/universalmanifest`)  
Work order: `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0133-protocol-recommendation-governance-and-standards-currency-matrix.md`

## 1) Purpose

This report defines how Universal Manifest documentation should talk about named protocol families when those ecosystems are changing over time.

It introduces:

- a recommendation-governance model,
- a dated standards-currency matrix,
- promotion and demotion rules,
- and the narrative-doc surfaces that should reference this matrix instead of freezing status claims inline.

## 2) Core rule

Narrative UM documentation should distinguish between three different things:

- `relationship`: how UM relates to a standards family at the architecture level,
- `currency`: the current maturity or stability checkpoint of that standards family,
- `recommendation tier`: how strongly UM docs are allowed to talk about that family.

The problem this report solves is that those three concepts were starting to blur together.

## 3) Recommendation tiers

### Tier A — Foundation reference

Definition:

- Safe to name as a stable standards family that UM builds on or interoperates with directly.

Allowed wording:

- “UM builds on...”, “UM can carry...”, “UM is compatible with...”.

Not allowed:

- method-level or vendor-level prescriptions unless separately justified.

### Tier B — Bounded current guidance

Definition:

- Safe to mention as a current candidate family in integration guidance, but only with explicit caveats and no lock-in language.

Allowed wording:

- “One current presentation family is...”, “An implementation may use...”, “Examples include...”.

Required guardrails:

- link to this currency matrix,
- no normative language,
- no implication that UM selected the family.

### Tier C — Architecture context only

Definition:

- Safe to mention as an example substrate or adjacent system in positioning material, but not safe to recommend as an implementation choice.

Allowed wording:

- “UM may point to...”, “UM can attach to...”, “UM does not replace...”.

Not allowed:

- “recommended store”, “preferred federation substrate”, or equivalent wording.

### Tier D — Research only

Definition:

- Mention only in reports, research-first work orders, or bounded internal analysis until stronger evidence exists.

Allowed wording:

- “under evaluation”, “research-first topic”, “not currently recommended”.

## 4) Promotion rules

A protocol family may move up one tier only when all applicable conditions are met:

1. Its formal specification status is stable enough for the intended claim, or there is a documented exception.
2. The ecosystem has at least two independent implementation paths or a comparable anti-lock-in justification.
3. UM has executable evidence or a bounded implementation artifact showing the family can attach without changing core UM behavior.
4. Security, privacy, revocation, freshness, and failure-mode implications are documented.
5. The promotion is recorded in a dated matrix review, not only implied by narrative docs.

## 5) Demotion rules

A protocol family must move down a tier when any of the following becomes true:

1. The formal spec posture weakens or becomes too unsettled for the claim being made.
2. The ecosystem collapses toward a single-vendor or single-stack dependency.
3. UM's executable evidence becomes stale, broken, or no longer representative.
4. New privacy or security issues materially change the safe guidance boundary.
5. Narrative UM docs contain frozen status claims that are newer than the evidence supporting them.

## 6) Review cadence

Use two review modes.

### Scheduled review

- Every 90 days for Tier B, Tier C, and Tier D families that appear in published UM docs.

### Event-driven review

Run an out-of-band review when any of the following occurs:

- an official spec changes status,
- a named ecosystem materially gains or loses viability,
- UM adds a new integration lane that names the family,
- a work order proposes promoting a family into stronger guidance.

## 7) Standards currency matrix (2026-03-06)

## 7.1 JSON-LD 1.1

- `Current status`: W3C Recommendation
- `UM role`: core document model foundation
- `Tier`: `A — Foundation reference`
- `Allowed wording now`: safe to describe as a foundational dependency
- `Next review trigger`: only if UM changes its core syntax assumptions

## 7.2 DID Core

- `Current status`: W3C Recommendation
- `UM role`: method-agnostic identifier family for `subject`, issuer, and key references
- `Tier`: `A — Foundation reference`
- `Allowed wording now`: safe to describe UM as DID-compatible without requiring DIDs
- `Next review trigger`: if UM narrows or expands method-level examples materially

## 7.3 Named DID methods (`did:key`, `did:web`, `did:ion`, `did:pkh`, `did:plc`, extension lanes such as `did:chia`)

- `Current status`: mixed ecosystem; method viability varies by community and deployment context
- `UM role`: examples only unless a lane-specific evidence pack says otherwise
- `Tier`: `B — Bounded current guidance`
- `Allowed wording now`: “examples include...” with explicit non-endorsement language
- `Not allowed now`: “recommended DID methods for UM”
- `Next review trigger`: any new method added to an integration lane or standards-positioning surface

## 7.4 Verifiable Credentials Data Model 2.0

- `Current status`: W3C Recommendation
- `UM role`: stable credential-family reference; UM can carry VC-shaped claims
- `Tier`: `A — Foundation reference`
- `Allowed wording now`: safe to position VC DM as a standards family UM can transport alongside other state
- `Next review trigger`: if UM starts naming specific VC proof profiles as preferred

## 7.5 Verifiable Credential Data Integrity 1.0

- `Current status`: W3C Recommendation
- `UM role`: candidate additive integrity family beyond UM's current JCS + Ed25519 baseline
- `Tier`: `B — Bounded current guidance`
- `Allowed wording now`: safe to say it is a future additive option
- `Not allowed now`: “preferred UM signing profile”
- `Next review trigger`: any work order proposing a formal UM Data Integrity profile

## 7.6 OpenID for Verifiable Presentations 1.0

- `Current status`: final specification
- `UM role`: candidate presentation/proof transport family for wallet-mediated exchange
- `Tier`: `B — Bounded current guidance`
- `Allowed wording now`: safe to name as a current presentation family under explicit caveats
- `Not allowed now`: “recommended UM wallet transport”
- `Next review trigger`: completion of proximity/presentation boundary work under `WO-0134`

## 7.7 OpenID for Verifiable Credential Issuance 1.0

- `Current status`: final specification
- `UM role`: candidate issuance family adjacent to UM-managed proof pointers and wallet/runtime state
- `Tier`: `B — Bounded current guidance`
- `Allowed wording now`: safe to mention as a current issuance family in research and bounded guidance
- `Not allowed now`: “required UM issuance protocol”
- `Next review trigger`: any adoption guide or lane that starts describing issuance flows in detail

## 7.8 SD-JWT VC

- `Current status`: active IETF draft
- `UM role`: candidate selective-disclosure proof family
- `Tier`: `D — Research only`
- `Allowed wording now`: “under evaluation” or “candidate proof family” in research work only
- `Not allowed now`: published recommendation in adopter-facing guidance
- `Next review trigger`: formal spec progression or completion of a dedicated selective-disclosure decision package

## 7.9 Digital Credentials API

- `Current status`: W3C Working Draft
- `UM role`: candidate browser or OS mediation surface for live presentation flows
- `Tier`: `D — Research only`
- `Allowed wording now`: research and architecture discussion only
- `Not allowed now`: browser-level recommendation in implementation guidance
- `Next review trigger`: `WO-0134` completion or a formal status change

## 7.10 Solid Protocol

- `Current status`: Editor's Draft
- `UM role`: example canonical-store substrate that UM can point to
- `Tier`: `C — Architecture context only`
- `Allowed wording now`: safe to describe as one possible external storage substrate or pointer target
- `Not allowed now`: “recommended canonical store for UM”
- `Next review trigger`: any doc that tries to present Solid as more than one example substrate

## 7.11 Decentralized Web Node (DWN)

- `Current status`: active specification surface
- `UM role`: candidate external substrate for subject-controlled state and sync
- `Tier`: `D — Research only`
- `Allowed wording now`: research-only discussion or future-substrate analysis
- `Not allowed now`: adopter-facing recommendation
- `Next review trigger`: `WO-0135` completion or a dedicated substrate comparison wave

## 7.12 AT Protocol

- `Current status`: active production protocol with official sync docs
- `UM role`: example federation substrate for social identity projection
- `Tier`: `C — Architecture context only`
- `Allowed wording now`: safe to position as one attachable federation surface UM can point into
- `Not allowed now`: “recommended federation substrate for UM”
- `Next review trigger`: if UM adds a dedicated AT Protocol integration lane or stronger social portability claims

## 7.13 OpenID Federation 1.0

- `Current status`: final specification
- `UM role`: trust-federation family relevant to verifier or issuer trust relationships, not subject-state portability by itself
- `Tier`: `B — Bounded current guidance`
- `Allowed wording now`: safe to mention as trust-federation context with explicit scope limits
- `Not allowed now`: “solves UM federation”
- `Next review trigger`: `WO-0135` completion or any verifier-trust integration lane proposal

## 8) Narrative-doc surfaces that should point to this matrix

Highest priority surfaces:

- `/Users/grig/work/repo/universalmanifest/docs/STANDARDS-POSITIONING.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/about/standards-positioning.md`
- `/Users/grig/work/repo/universalmanifest/integrations/did-vc.md`

Next editorial pass surfaces:

- `/Users/grig/work/repo/universalmanifest/docs/explainers/full-briefing.md`
- `/Users/grig/work/repo/universalmanifest/docs/OUTREACH-AND-ADOPTION-STRATEGY.md`
- `/Users/grig/work/repo/universalmanifest/docs/UNIVERSAL-MANIFEST-BRIEFING.md`

Policy:

- Narrative docs may describe the relationship between UM and a standards family.
- Narrative docs should not freeze volatile maturity judgments without also pointing to this matrix.
- Integration docs may name Tier B families only with explicit caveats.

## 9) Immediate doc-sync decision

Adopt the following immediate synchronization rule:

- `docs/STANDARDS-POSITIONING.md` and its site mirror should explicitly say that live protocol-family currency is tracked in this dated matrix.

This keeps the positioning page useful without turning it into a maintenance trap.

## 10) Final conclusion

UM does not need a bigger protocol shortlist.

UM needs a better discipline for how it talks about protocol families over time.

This report establishes that discipline:

- stable standards families can be named directly,
- current candidate families can be named only with bounded caveats,
- architecture substrates can be used as examples without endorsement,
- and active research families stay out of adopter-facing guidance until they earn promotion.
