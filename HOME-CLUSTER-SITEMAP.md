# Universal Manifest Sitemap

**Date:** 2026-04-24  
**Status:** Approved IA direction; ready for copy briefs  
**Purpose:** Plain markdown sitemap for the public site structure before any more homepage rewriting.

This document is the source-of-truth sitemap for the next public-site copy pass. It describes the intended information architecture, not the current implementation state. Public-site implementation should not resume until this sitemap and the related copy briefs are approved.

Every public reader page in this sitemap should have a markdown/source counterpart and a bottom-page link that lets readers download or view that markdown/source version. Future site changes must update the markdown/source document and rendered site surface together.

Related approval documents:

- `/Users/grig/work/repo/universalmanifest/docs/HOME-CLUSTER-COPY-BRIEFS.md`
- `/Users/grig/work/repo/universalmanifest/docs/AUDIENCE-PAGE-BRIEFS.md`
- `/Users/grig/work/repo/universalmanifest/docs/MARKDOWN-SOURCE-FIDELITY-PROCESS.md`

## Top-Level Public Navigation

- `Home` — `/`
- `Latest Spec` — `/spec/latest/`

This top-level navigation is approved and should stay exactly this small.

Rationale:

- `Home` is the human first-contact path.
- `Latest Spec` is the standards-reader shortcut.
- Everything else remains discoverable through the `Home` cluster, docs, audience pages, proof surfaces, or machine-readable discovery, without widening the public header.

## Home-Cluster Page Role Contracts

These page roles are part of the sitemap. They exist to prevent duplicate copy and unclear reader flow.

| Page | Route | Primary job | Must not become |
| --- | --- | --- | --- |
| `Home` / `Overview` | `/` | first-contact definition and routing | a full standard explainer, docs index, or audience directory |
| `Use Cases` | `/use-cases/` | narrative scenario-family overview | an interactive tool or complete integration catalog |
| `Scenario Explorer` | `/explorer/` | lane-by-lane scenario inspection after use-case context | a generic concept explorer, sandbox, or route family for every lane |
| `How It Works` | `/how-it-works/` | conceptual model: envelope, pointers, consent, validity windows, projection | a standards-comparison page or normative spec substitute |
| `Standards Fit` | `/standards-fit/` | canonical standards-comparison and ecosystem-boundary surface | a second homepage or implementation guide |
| `Latest Spec` | `/spec/latest/` | normative contract and stable public draft route | a first-contact explanation page |
| `Audience` pages | `/audiences/*` | downstream role/ecosystem/evaluator landing pages | a topic taxonomy |
| supporting reading pages | mixed | secondary references, handouts, or compatibility routes | competing first-contact pages |

Reader progression:

```text
first-contact explanation
-> concrete use-case families
-> scenario explorer
-> conceptual model
-> standards fit
-> latest spec / implementation / proof surfaces
```

Branching rule:

- readers who want the normative contract can use `Latest Spec` at any time
- readers who want adoption guidance should move from `Use Cases` or `Scenario Explorer` into audience, implementation, integration, or proof surfaces
- readers who are evaluating fit against adjacent standards should move through `How It Works` before `Standards Fit`
- every canonical public reader page should end with a markdown/source link so humans and agents can inspect or download the source version

## Sitemap

### 1. HOME PAGE — `/`

Purpose:

- first-contact explanation
- plain-language definition of Universal Manifest
- route into the right next path

Elements:

#### a. Global Header

- logo / project name
- top-level navigation:
  - `Home`
  - `Latest Spec`

Interaction:

- clicking `Home` returns to `/`
- clicking `Latest Spec` goes to `/spec/latest/`

#### b. Hero

Content:

- one plain-language definition of UM
- one short explanation of the fragmentation problem
- one short line making clear that UM is a portable document/envelope
- one restrained credibility signal that this is an open standard/specification effort, not a closed app

Interaction:

- primary CTA: go to `/use-cases/`
- secondary CTA: go to `/spec/latest/`
- optional tertiary route: go to `/explorer/` only after the use-case framing is clear and the visible label is `Scenario Explorer`

CTA hierarchy rule:

- do not send first-time readers directly into tools, proof surfaces, or implementation docs from the primary hero action
- do not use `Explore` alone as a CTA label when the destination is `/explorer/`; use `Scenario Explorer` or a phrase that names scenario inspection

#### c. Problem / Why This Exists

Content:

- 2 to 4 short scenario summaries showing the kinds of fragmentation UM solves
- examples should be concrete, not abstract systems language
- at least one summary should support metaverse / digital-world portaling
- at least one summary should support EU digital identity / credential-wallet portability
- at least one summary should support agent-to-agent exchange or peer-to-peer payment portability
- at least one summary should support privacy, encrypted/private facets, and attested identifier/control binding without creating a new top-level lane

Interaction:

- each item can link to either:
  - `/use-cases/`
  - `/explorer/` when it is clearly framed as the `Scenario Explorer`
  - a relevant audience page

#### d. Secondary Routing Block

Content:

- links into the rest of the `Home` cluster in this order:
  - `/use-cases/` — visible label: `Use Cases`
  - `/explorer/` — visible label: `Scenario Explorer`
  - `/how-it-works/` — visible label: `How It Works`
  - `/standards-fit/` — visible label: `Standards Fit`

Interaction:

- each item is a simple route into the next depth level
- each item should say what question it answers, not just repeat the page title

#### e. Limited Audience Entry

Content:

- selective links to the most strategic audience pages
- not a giant audience taxonomy

Interaction:

- default homepage audience links:
  - `/audiences/metaverse/` — visible label: `Metaverse Portaling and Digital Worlds`
  - `/audiences/eu-ssi/` — visible label: `EU Digital Identity and SSI`
  - `/audiences/platforms/` — visible label: `Platform Builders`

Audience-entry rule:

- the homepage may link to at most 3 audience pages by default
- additional audience routes belong on `/use-cases/`, `/explorer/`, relevant audience pages, or docs/integration surfaces

#### f. Footer

Content:

- minimal footer
- no giant route dump
- may include secondary links to docs, governance, machine-readable discovery, and project repository only if they do not compete with the primary page flow
- must include a markdown/source download or view-source link for the current page when a markdown/source counterpart exists

### 2. LATEST SPEC PAGE — `/spec/latest/`

Purpose:

- normative contract
- stable public draft route
- standards-reader shortcut from every top-level page

Elements:

#### a. Global Header

- logo / project name
- top-level navigation:
  - `Home`
  - `Latest Spec`

Interaction:

- same top-level behavior as the homepage

#### b. Spec Identity Banner

Content:

- clear label that this is the latest draft specification
- clear relationship to UM as a standard
- clear status language so readers know whether they are reading a draft, candidate release, or final version

#### c. Spec Intro

Content:

- title
- abstract
- status of this document

#### d. Table of Contents

Content:

- section index for the specification

Interaction:

- expand/collapse behavior if present
- anchor links to sections

#### e. Spec Body

Content:

- normative content
- examples
- conformance
- security/privacy

#### f. Practical Handoff

Content:

- restrained links to implementation and validation surfaces for readers ready to act:
  - `/getting-started/`
  - `/conformance/`
  - `/reference/resolver-api/`
  - `/spec/v01/`
  - `/spec/v02/`
- markdown/source link for the spec or generated-source artifact where available

### 3. USE CASES PAGE — `/use-cases/`

Purpose:

- narrative overview of the strongest public scenario families
- primary next step after the homepage
- bridge between first-contact comprehension and deeper scenario/audience evaluation

This page should answer: "Where would Universal Manifest matter in the real world?"

Elements:

#### a. Local `Home` Cluster Navigation

- `Overview`
- `Use Cases`
- `Scenario Explorer`
- `How It Works`
- `Standards Fit`

Interaction:

- each item routes inside the `Home` cluster
- order stays consistent across every `Home` cluster page

#### b. Page Intro

- short explanation that these are the main use-case families
- clear statement that this page is narrative and scannable, while `Scenario Explorer` provides deeper lane-by-lane inspection

#### c. Use-Case Groups

Initial group order:

1. metaverse portaling and digital-world interoperability
2. EU digital identity / SSI / credential wallets
3. platform builders and cross-system interoperability
4. credential issuers and verifiers
5. agent-to-agent transactions
6. peer-to-peer crypto payments
7. privacy, consent, and bounded disclosure

Each group should include:

- the concrete fragmentation problem
- what UM carries or points to
- who cares about this scenario
- the best next route
- the public standards, protocols, or interoperability context that make the scenario plausible

Interaction:

- each group links to:
  - `/explorer/` when deeper scenario inspection is the next step
  - relevant audience pages
  - relevant integration, proof, or implementation surfaces only after the reader understands the use case

Use-case page rule:

- do not make every group an audience page
- do not make every group an explorer lane
- group by reader comprehension first, then route to audiences, explorer lanes, and implementation surfaces

### 4. SCENARIO EXPLORER PAGE — `/explorer/`

Visible page label:

- `Scenario Explorer`

Route:

- keep `/explorer/` as the route unless a later route-compatibility decision says otherwise
- do not use `Explorer` alone as the visible label in navigation or CTAs

Approval status:

- visible label `Scenario Explorer` is approved

Purpose:

- use-case drill-down after `/use-cases/`
- interactive inspection of one lane at a time
- proof/spec/audience handoff for readers who already understand the scenario space
- not a generic tool page and not the same surface as `/tools/concept-explorer/`

This page should answer: "What happens in this scenario, what travels, and what proof or spec surface backs it?"

Elements:

#### a. Local `Home` Cluster Navigation

- `Overview`
- `Use Cases`
- `Scenario Explorer`
- `How It Works`
- `Standards Fit`

#### b. Intro / Scenario Explorer Framing

- short explanation that this page inspects one scenario lane at a time
- clear statement that readers should use `/use-cases/` first if they need the narrative overview
- clear distinction from `/tools/concept-explorer/`, which is a broader concept/tool surface outside the `Home` cluster

#### c. Left Column / Lane Selector

Initial approved lane order:

1. Metaverse Portaling and Digital-World Interoperability
2. EU Digital Identity and SSI
3. Platform Builders and Cross-System Interoperability
4. Credential Issuers and Verifiers
5. Agent-to-Agent Transactions
6. Peer-to-Peer Crypto Payments
7. Privacy, Consent, and Bounded Disclosure

Subtopics that should not start as top-level lanes:

- avatars and portable identity
- content and asset projection
- private facets, encrypted data, claim proofs, cross-DID binding, and attested identifier/control binding when they are better handled inside the credential/verifier, privacy, how-it-works, or standards-fit surfaces
- individual credential providers
- individual games, apps, wallets, chains, devices, or service providers
- standalone venue or spatial lanes

These can appear inside the relevant lane, use-case group, audience page, integration page, or proof page if they have enough source material.

Lane notes:

- `Metaverse Portaling and Digital-World Interoperability` should be grounded in the project IWPS source stack, especially `/Users/grig/work/repo/universalmanifest/docs/research/iwps-base-specification-v0.3.md` and `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-11-iwps-um-alignment-analysis.md`. It should include a clear standards-oriented example of a subject portaling between compatible worlds where IWPS handles Query/Teleport, capability negotiation, communication paths, and session binding, while UM carries avatar state, identity references, DID/credential references where relevant, consent/policy, content pointers, and other portable state that the destination world can project without one-off integrations.
- `EU Digital Identity and SSI` must be grounded in public EU digital identity / wallet / credential standards and publicly available implementation direction. If a public standard is emerging but not fully supported yet, the lane should clearly distinguish current support from forward-compatible readiness.
- `Credential Issuers and Verifiers` should surface v0.2 claim authenticity and identifier-binding guidance, especially optional `claims[].claimProof` proof material and the non-normative `identity.crossDidBinding` convention for attested cross-DID binding. Public copy should distinguish Tier 1 attested binding from deferred stronger cryptographic/multi-party binding tiers.
- `Peer-to-Peer Crypto Payments` should describe intermediary-free peer-to-peer blockchain payment flows abstractly. Do not name a specific chain, offer protocol, wallet provider, or payment rail in public lane copy unless explicitly approved.
- `Agent-to-Agent Transactions` should cover machine/agent-mediated exchange where manifests help agents understand identity, authority, consent, policy, and transaction context.
- `Privacy, Consent, and Bounded Disclosure` should cover default-deny consent, projection, and optional encrypted inline facets as complementary privacy paths. It should explain that the clear envelope can remain verifiable while sensitive facet payloads stay unreadable to parties without keys, and that consumers without keys can still process partial visibility safely.

Interaction:

- click a lane to load that lane into the main pane
- no infinite scroll
- no route explosion required for each lane

#### d. Main Explorer Pane

Content per lane:

- exact lane headline
- short summary
- concrete scenario steps
- why UM fits
- what actually travels
- what remains authoritative elsewhere
- policy/consent/freshness considerations
- proof/spec links
- links to relevant audience pages
- markdown/source link for the lane content or page source where available

Interaction:

- when a lane is clicked in the left column, this pane updates in place
- deeper detail may expand/collapse

Lane governance:

- a lane should exist only when it represents a distinct public scenario with enough proof, source material, and audience relevance to support inspection
- narrower examples should live inside a use-case detail, audience page, integration page, or proof page rather than becoming top-level explorer lanes
- the first release should favor fewer stronger lanes over many thin lanes

### 5. HOW IT WORKS PAGE — `/how-it-works/`

Purpose:

- explain the conceptual model simply
- translate scenario interest into a working mental model
- prepare evaluators for standards comparison or spec reading

This page should answer: "What is the shape of the thing, and how does it move between systems?"

Elements:

#### a. Local `Home` Cluster Navigation

- `Overview`
- `Use Cases`
- `Scenario Explorer`
- `How It Works`
- `Standards Fit`

#### b. Conceptual Intro

- what UM is
- what UM is not
- why UM is pointer-first rather than a database replacement

#### c. Core Model Sections

- the envelope
- records / facets / claims / consents
- what travels
- what remains authoritative elsewhere
- pointers
- consent / policy
- private data handling through projection and optional encrypted inline facets
- claim authenticity, attested identifier binding, and trust-tier boundaries
- issued/expires validity windows and bounded trust
- optional runtime/resolver context without making `myum.net` sound like a required dependency
- how agent-to-agent and peer-to-peer exchange can use the same portable envelope without making any one payment rail, blockchain, agent framework, or runtime mandatory

#### d. Conceptual Handoff

Content:

- link to `/standards-fit/` for adjacent-standard comparison
- link to `/spec/latest/` for the normative contract
- link to `/getting-started/` for implementation orientation

How-it-works rule:

- this page should use conceptual language, not dense spec copy
- normative requirements belong in `/spec/latest/`
- implementation checklists belong in `/getting-started/`, `/guides/`, `/conformance/`, or related docs

### 6. STANDARDS FIT PAGE — `/standards-fit/`

Purpose:

- explain where UM fits among adjacent standards
- reduce false replacement claims
- give standards evaluators a canonical positioning page before they read the spec

This page should answer: "How does UM relate to the standards and protocols I already know?"

Elements:

#### a. Local `Home` Cluster Navigation

- `Overview`
- `Use Cases`
- `Scenario Explorer`
- `How It Works`
- `Standards Fit`

#### b. Boundary Intro

- UM is not a replacement for every adjacent standard
- UM is a portable pointer-and-policy envelope that can compose with identity, credential, storage, messaging, resolver, and projection systems

#### c. Comparison / Positioning Sections

- credentials and verifiable claims
- identity and subject identifiers
- claim authenticity, `claimProof`, and attested cross-DID binding
- consent and policy signals
- private data handling, projection, and encrypted inline facets
- storage and pointer-based data access
- messaging / exchange / projection
- runtime / resolver context
- agent transaction context
- peer-to-peer payment and settlement context
- conformance and proof posture

#### d. Standards Handoff

Content:

- `/spec/latest/`
- `/spec/v01/`
- `/spec/v02/`
- `/conformance/`
- `/integrations/`
- `/reference/resolver-api/`

Canonicalization rule:

- `Standards Fit` is the canonical public standards-comparison role
- `/about/standards-landscape/` may remain as a secondary support page, source page, or compatibility route, but it should not compete as a separate canonical standards explanation
- if both pages exist publicly, `Standards Fit` owns the current public positioning and `/about/standards-landscape/` should point readers there
- EU digital identity / SSI material must be grounded in actual public standards, specifications, architecture references, or public implementation direction rather than internal assumptions

### 7. AUDIENCE LANDING PAGE FAMILY — `/audiences/*`

Purpose:

- downstream pages for strategic audiences, roles, or ecosystem evaluator groups
- not part of the top-level public nav
- not a general topic taxonomy

Audience taxonomy rule:

- every audience route must name a real audience, implementer group, operator group, buyer/evaluator group, or ecosystem group
- topic-only pages should live under use cases, integrations, standards fit, policy/proof material, or docs
- if a page cannot say who it serves, it is not ready to be an audience page

Approved initial audience routes:

| Route | Visible label | Audience type | Notes |
| --- | --- | --- | --- |
| `/audiences/metaverse/` | `Metaverse Portaling and Digital Worlds` | ecosystem / evaluator group | first-class because of MUM lineage, portaling strategy, and standards-organization relevance |
| `/audiences/eu-ssi/` | `EU Digital Identity and SSI` | ecosystem / evaluator group | must connect to credential-wallet and issuer/verifier scenarios |
| `/audiences/platforms/` | `Platform Builders` | implementer / operator group | includes app, service, and platform builders evaluating interoperability |
| `/audiences/credential-issuers-verifiers/` | `Credential Issuers and Verifiers` | role group | preferred canonical audience route if this audience is approved |

Compatibility / rename guidance:

- `/audiences/credential-and-personhood/` should not remain the canonical visible audience route because it names topics, not an audience
- if implementation or published links require keeping `/audiences/credential-and-personhood/`, treat it as a compatibility alias or rewrite it with the visible label `Credential Issuers and Verifiers`
- `/audiences/venues-and-spatial/` should not remain a canonical audience route. Treat it as legacy or compatibility-only unless a broader non-venue-specific operator group is approved later.

Do not approve as audience routes unless reframed around a real audience:

- `/audiences/privacy-and-consent/` — should move to use cases, policy, standards-fit, or proof unless rewritten for privacy officers, policy evaluators, or consent-system builders
- `/audiences/credential-and-personhood/` — should move to use cases or integrations unless rewritten for credential issuers, verifiers, identity providers, or personhood ecosystem operators
- `/audiences/venues-and-spatial/` — should move out of the approved audience taxonomy unless it is replaced by a broader, non-venue-specific operator group approved later

Candidate future audience routes for brief approval:

- `/audiences/agent-builders/` — visible label: `Agent Builders`
- `/audiences/payment-and-wallet-builders/` — visible label: `Payment and Wallet Builders`

Shared page structure:

#### a. Audience Hero

- audience-specific framing
- why UM matters to this audience
- audience type stated implicitly through copy, not as internal IA terminology

#### b. Audience Pressure Points

- what this audience is trying to solve
- what breaks across systems today

#### c. Relevant Use Cases / Lanes

- links back into `/use-cases/`
- links back into `/explorer/`
- links to the strongest relevant scenario lanes

#### d. Relevant Standards / Proof / Docs Links

- appropriate next-step links for this audience
- should include `/spec/latest/` when the audience is a standards evaluator or implementer

Audience-page rule:

- every audience page must link back to relevant use-case groups, the `Scenario Explorer`, the latest spec, and any proof or implementation surfaces that help that audience take the next step
- every audience page must make clear whether it is serving a role, an ecosystem, or an evaluator group
- audience pages should be curated landing pages, not exhaustive topic repositories

### 8. SUPPORTING READING SURFACES

These are public but not part of the primary first-contact path:

- `/docs/`
- `/about/why-um/`
- `/about/one-pager/`
- `/about/standards-landscape/`

Route posture:

| Route | Posture | Rule |
| --- | --- | --- |
| `/docs/` | curated docs entry | may remain a major secondary route, but not in top-level public nav |
| `/about/why-um/` | secondary explainer or compatibility route | should not compete with the homepage and `/use-cases/` |
| `/about/one-pager/` | handout / secondary reference | should not be treated as a parallel homepage |
| `/about/standards-landscape/` | source, support, or compatibility route | should feed or point to `Standards Fit`, not compete with it |

Canonicalization rule:

- the `Home` cluster owns first-contact explanation
- `Standards Fit` owns public standards comparison
- secondary about pages should become handouts, supporting references, or compatibility routes unless a future approved IA decision assigns them a distinct job
- secondary about pages must still be kept current with their markdown/source versions and any HTML/rendered versions that remain public

### 9. TOOL AND PROOF SURFACES

These are public but not part of the top-level public nav:

- `/learning/`
- `/sandbox/`
- `/workbench/`
- `/proof/harness/`
- `/proof/journeys/`
- `/proof/smoke/`
- `/tools/concept-explorer/`

Tool/proof route rule:

- tools and proof routes should be linked from relevant use cases, explorer lanes, implementation docs, and spec/conformance pages
- do not use the homepage footer as a route dump for tools
- keep `/explorer/` distinct from `/tools/concept-explorer/`

### 10. STANDARDS / GOVERNANCE / IMPLEMENTATION SURFACES

These remain public secondary surfaces:

- `/conformance/`
- `/getting-started/`
- `/guides/`
- `/integrations/`
- `/governance/`
- `/publishing/`
- `/reference/resolver-api/`
- `/spec/v01/`
- `/spec/v02/`
- `/resolver/`

Implementation/proof handoff rule:

- the `Home` cluster should include explicit next-step links into existing implementation and proof surfaces without adding another top-level navigation item
- handoffs should be contextual:
  - `/use-cases/` and `/explorer/` hand off to audience, integration, sandbox, workbench, and proof surfaces
  - `/how-it-works/` hands off to getting-started, spec, conformance, and resolver context
  - `/standards-fit/` hands off to spec, conformance, integrations, governance, and resolver API reference
- likely handoff targets:
  - `/docs/`
  - `/getting-started/`
  - `/conformance/`
  - `/sandbox/`
  - `/workbench/`
  - `/proof/harness/`
  - `/reference/resolver-api/`

### 11. MACHINE-READABLE AND AGENT-FACING SURFACES

These support machines, external agents, and agent evaluators. They are not part of the primary human first-contact path.

Machine-readable surfaces:

- `/.well-known/universal-manifest.json`
- `/.well-known/security.txt`
- `/llms.txt`
- `/agent/fixture-catalog.json`
- `/agent/sandbox-scenarios.json`

Agent-facing reader surfaces:

- `/for-agents/`
- `/for-agents/external-agent-onboarding/`

Rule:

- machine-readable and agent-facing surfaces should stay discoverable from docs, discovery descriptors, and relevant implementation/proof routes
- they should not become top-level public navigation
- public reader pages should include bottom-page markdown/source links so agents and humans can inspect the exact source text
- machine-readable descriptors and agent-facing pages should point to canonical markdown/source material where practical

### 12. MARKDOWN / HTML / AGENT VARIANT FIDELITY

Purpose:

- prevent drift between markdown documents, rendered HTML pages, machine-readable files, and agent-facing variants
- make future public-site changes auditable by humans and agents

Rules:

- every canonical public reader page should have a markdown/source counterpart or a documented exception
- every canonical public reader page should include a bottom-page link to download or view the markdown/source version
- future agents updating a public site page must update the markdown/source document in the same change
- future agents updating a markdown/source document that has a rendered public page must update the rendered page or explicitly document why no rendered-page change is needed
- agent-facing files and machine-readable descriptors should be checked for consistency whenever source copy, route names, audience labels, or scenario lanes change
- copy briefs should include source-of-truth paths and rendered-route targets for each page

Recommended reusable solution:

- maintain one canonical markdown/source file per public reader page or content family
- render or mirror from that source wherever possible
- add a standard bottom-page source block:
  - `Download Markdown`
  - `View source`
  - optional `Agent-readable entry`
- add a parity checklist to every copy brief and implementation handoff:
  - markdown/source updated
  - rendered page updated
  - bottom-page markdown/source link present
  - machine-readable / agent-facing references checked
  - aliases or compatibility pages checked

## Current Structural Rule

```text
Top level:
- Home
- Latest Spec

Inside Home:
- Overview
- Use Cases
- Scenario Explorer
- How It Works
- Standards Fit

Below Home:
- Audience pages for real audiences, roles, implementer groups, operator groups, or ecosystem evaluator groups

Outside first-contact flow but still public:
- Docs
- About/supporting reading pages
- Tools
- Proof surfaces
- Standards / governance / implementation pages
- Machine-readable and agent-facing surfaces
- Markdown/source links and source-fidelity rules
```

## Approval Checklist

Approved decisions:

- global navigation stays limited to `Home` and `Latest Spec`
- `/explorer/` uses `Scenario Explorer` as its visible label
- EU digital identity / SSI is a confirmed strategic path and must be grounded in public standards or public implementation direction
- `/about/why-um/`, `/about/one-pager/`, and `/about/standards-landscape/` are secondary support or compatibility surfaces, not competing canonical explanations
- canonical public reader pages need bottom-page markdown/source links
- markdown/source and rendered-page parity is a top-level project rule
- standalone venue/spatial framing is removed from the approved lane and audience taxonomy
- `Privacy, Consent, and Bounded Disclosure` remains the seventh `Scenario Explorer` lane

Remaining confirmation before copy-brief work:

- use this approved 7-lane `Scenario Explorer` list:
  - Metaverse Portaling and Digital-World Interoperability
  - EU Digital Identity and SSI
  - Platform Builders and Cross-System Interoperability
  - Credential Issuers and Verifiers
  - Agent-to-Agent Transactions
  - Peer-to-Peer Crypto Payments
  - Privacy, Consent, and Bounded Disclosure
- approve the initial audience taxonomy and the preferred replacement of `Credential and Personhood` with `Credential Issuers and Verifiers`
- approve first audience-page brief targets, including whether `Agent Builders` and `Payment and Wallet Builders` become first-wave audience pages

## Order Of Operations

1. Approve the copy brief for each page in the `Home` cluster.
2. Approve the first audience-page briefs.
3. Only then rewrite the homepage and related site pages.
