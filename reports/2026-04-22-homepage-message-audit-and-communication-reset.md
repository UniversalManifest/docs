# Homepage Message Audit and Communication Reset

**Date:** 2026-04-22  
**Status:** Audit and strategy report  
**Scope:** `universalmanifest.net/` homepage messaging and positioning  

## Objective

Audit the current homepage against the project's actual vision, definitions, and public positioning, then define a lower-noise communication strategy that explains Universal Manifest clearly to first-time human readers.

## Sources reviewed

- `/Users/grig/work/repo/universalmanifest/site/src/pages/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/layouts/PublicSurfaceLayout.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/components/ui/SiteHeader.astro`
- `/Users/grig/work/repo/universalmanifest/README.md`
- `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md`
- `/Users/grig/work/repo/universalmanifest/docs/DOMAIN-ARCHITECTURE.md`
- `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
- `/Users/grig/work/repo/universalmanifest/docs/COMPREHENSIVE-PROJECT-PROPERTIES-AND-SURFACES-MAP.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/about/why-um.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/about/one-pager.md`

## The simplest true description of Universal Manifest

Across the canonical project docs, Universal Manifest is most consistently described as:

- a **portable document format**
- for moving **identity references, claims, consents, devices, and pointers**
- between **compatible systems**
- with **bounded trust** through validity windows and optional signatures
- in a **pointer-first** way that does not try to replace every existing system or data store

The strongest short definitions in the repo are:

- "A portable document format for sharing identity, credentials, and preferences between systems." (`README.md`)
- "A portable document format that solves fragmentation." (`about/why-um.md`)
- "A portable pointer-and-policy envelope, not a monolithic database replacement." (`PROJECT-VISION.md`)

That is the conceptual center of gravity.

## What the current homepage says

The current homepage at `/Users/grig/work/repo/universalmanifest/site/src/pages/index.astro` currently leads with these ideas:

- "One portable document instead of a custom handoff for every new system."
- "identity references, permissions, claims, and authoritative pointers"
- "bounded subject state"
- "Latest Spec, One Click Away"
- "The public draft already being shared now lives at `/spec/latest/`"
- "The latest draft stays one click away"

Structurally, the page currently spends most of its energy on:

1. abstract systems-language framing,
2. a repeated explanation that the spec is easy to find,
3. audience cards,
4. a closing spec callout.

## Audit findings

### 1. Internal product-management language is leaking into public copy

This is the clearest failure mode.

The homepage currently includes language that makes sense only if the reader already knows the internal project mandate:

- "A simpler front door for Universal Manifest"
- "Latest Spec, One Click Away"
- "The public draft already being shared now lives at `/spec/latest/`"
- "This homepage exists to explain the idea first, then route directly to the contract."
- "The latest draft stays one click away."

This is not user-facing explanation. It is maintainership language. It tells the visitor about site-architecture decisions instead of telling them what Universal Manifest is.

### 2. The homepage is too abstract too early

The first-screen copy uses phrases like:

- "custom handoff"
- "identity references"
- "authoritative pointers"
- "bounded subject state"

These are not wrong, but they are too compressed and too internal for a first read.

A person with no prior context still does not know:

- what a manifest actually is,
- why they should care,
- whether this is for personal data portability, identity, privacy, credentials, or app integration,
- whether UM replaces existing standards or works with them.

### 3. The problem is present, but not felt

The project's better explanatory material makes the fragmentation problem concrete:

- people re-enter the same profile repeatedly,
- privacy preferences do not travel,
- offline devices either trust everything or nothing,
- platforms rebuild fragile pairwise integrations.

The homepage mostly describes the solution in systems language before the human problem has become intuitive. It does not make the fragmentation pain vivid enough.

### 4. The current page over-rotates toward implementer phrasing

The broader project is intentionally multi-audience, but the homepage currently sounds like it is written mainly for someone already thinking about payloads, TTL, receivers, and trust posture.

That loses:

- curious first-time readers,
- policy/evaluator readers,
- people trying to understand the idea before the contract,
- non-technical stakeholders who still need to understand why the standard matters.

### 5. The strongest differentiators are underexplained

The repo's strongest positioning points are not landing cleanly on the homepage:

- UM is **not** another auth protocol.
- UM is **not** another database or storage system.
- UM is **not** trying to replace every adjacent standard.
- UM is a **portable envelope** that works with existing systems.
- Consent and policy can travel alongside state.
- Offline validity windows are part of the model.

Those ideas appear elsewhere in the project, but not with enough clarity on the homepage.

### 6. The audience segmentation appears before comprehension

The "People / Apps / Devices / Organizations" chips and the three audience cards are not inherently wrong, but they arrive before the visitor has a clean mental model.

That means the page starts classifying readers before it has taught the core object.

### 7. The page repeats spec discoverability too many times

The permanent top navigation already contains `Home` and `Latest Spec`.

That means the body does not need to keep saying:

- the spec is one click away,
- the draft is already being shared,
- the homepage exists to route to the contract,
- the latest draft stays one click away.

One clear CTA is enough. The rest becomes noise.

## The underlying mismatch

The project's canonical docs describe Universal Manifest as a portable state/pointer/policy envelope with trust, data, and interaction layers.

The homepage currently describes it more like:

- a generic interoperability object,
- a site-routing problem,
- and a contract-discoverability problem.

That is the core mismatch.

The homepage is explaining:

- how the website is arranged,
- how systems might think about the object,
- and why the spec link is easy to find,

instead of explaining:

- what the object is,
- what human/system problem it solves,
- why it is different,
- and where a reader should go next.

## Recommended communication reset

The homepage should do only four jobs:

1. **Name the thing clearly.**
2. **Make the fragmentation problem obvious.**
3. **Explain the model simply.**
4. **Offer one clear path to the spec.**

Everything else should be deferred.

## Recommended homepage message strategy

### 1. Lead with the object, not the site

The first sentence should define Universal Manifest in plain language.

Recommended shape:

"Universal Manifest is a portable document for carrying identity, permissions, and related state between compatible systems."

That is stronger than leading with "custom handoff" or "simpler front door."

### 2. Lead with the fragmentation problem in human terms

The next thing the reader should understand is:

- the same profile gets rebuilt over and over,
- consent does not travel,
- receiving systems lack shared context,
- offline environments lack a bounded permission packet.

Use one or two concrete examples, not a category taxonomy.

### 3. Explain UM as an envelope

The most stable metaphor in the repo is the envelope/container/capsule idea.

That is better for the homepage than:

- "bounded subject state"
- "authoritative pointers"
- "core envelope to read"
- "custom handoff for every relationship"

Recommended explanatory move:

- the manifest carries the important summary,
- it points to authoritative sources when needed,
- it includes consent/policy,
- it expires when it should stop being trusted.

That is enough for the homepage.

### 4. State the boundary explicitly

The page should say, in plain language, that UM is not trying to replace every adjacent standard or store.

Recommended shape:

"It does not replace your database, your identity provider, or your existing standards. It gives compatible systems one portable document they can all understand."

That aligns much better with `PROJECT-VISION.md` and `about/why-um.md`.

### 5. Keep the spec obvious without talking about the mandate

The homepage should keep:

- top nav: `Home` and `Latest Spec`
- one primary hero CTA to the spec

The homepage should remove:

- "one click away"
- "already being shared"
- "this homepage exists to..."
- "stays one click away"

Those are internal concerns, not public communication.

### 6. Reduce the homepage to a minimum viable argument

A good homepage for the current project state should probably have only:

1. Hero: what UM is
2. Problem: what is broken today
3. Model: how UM solves that at a high level
4. CTA band: learn more or read the spec

No audience chips.
No audience-card matrix.
No repeated spec reassurance.
No meta commentary about website structure.

## Recommended structure for the next homepage pass

### Hero

Goal:

- one-sentence definition
- one-sentence problem
- two actions at most

Example direction:

- H1: "A portable document for moving identity, permissions, and related state between systems."
- Supporting line: "Instead of rebuilding the same profile, consent, and trust context in every new app or device, compatible systems can read one shared manifest."
- Actions: `What is Universal Manifest?` and `Read Latest Spec`

### Problem section

Goal:

- make fragmentation feel real

Content shape:

- profile portability,
- consent portability,
- offline trust / bounded validity

This section should read like consequences, not like architecture.

### How it works section

Goal:

- explain the envelope model in the simplest possible way

Content shape:

- who/what the manifest is about,
- what it is allowed to share,
- where authoritative data lives,
- when it expires.

### Boundary section

Goal:

- clarify what UM is not

Content shape:

- not a replacement for every data store,
- not another auth protocol,
- not a demand that every system share the same backend,
- yes: a portable document that works across systems.

### Closing CTA

Goal:

- give the reader exactly two choices

Recommended:

- `Read the latest spec`
- `Read the plain-language explanation`

## Messaging guardrails

For future homepage drafts, these should be treated as constraints:

- Do not reference internal publication strategy in public copy.
- Do not use unexplained phrases like "bounded subject state" on the homepage.
- Do not lead with audience taxonomy before defining the object.
- Do not explain the route architecture of the website on the homepage.
- Do not repeat spec discoverability more than once in body copy.
- Do not make the homepage summarize the entire project.
- Prefer concrete human/system consequences over abstract interoperability language.

## Bottom line

The homepage has not failed because the project lacks good source material. It has failed because the project's strongest source material has not been distilled aggressively enough.

The repo already contains better raw messaging than the homepage currently uses.

The right move is not to add more. The right move is to remove most of the current homepage rhetoric and rebuild it around:

- one clear definition,
- one clear problem,
- one simple model,
- one clear spec path.
