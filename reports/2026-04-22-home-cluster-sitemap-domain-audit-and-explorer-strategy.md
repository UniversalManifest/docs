# Home-Cluster Sitemap, Domain Audit, and Explorer Strategy

**Date:** 2026-04-22  
**Status:** Strategy and IA report  
**Related WO:** `WO-0195`

## Purpose

Define a better public information architecture for Universal Manifest after the homepage message audit.

This report answers five questions:

1. What should the homepage actually optimize for?
2. How should the `Home` surface be split into subpages without widening the global menu?
3. How should the project be organized into domains of thought and levels of depth?
4. What should the interactive explorer actually be?
5. In what order should content and UI work happen?

## Core correction

The previous homepage reset direction was correct about noise reduction but incomplete about audience shape.

The homepage should not be:

- one giant summary page,
- a spec-routing explanation,
- or a generic message aimed at only one audience.

It should instead act as the front of a **home cluster**:

- one calm global menu: `Home` and `Latest Spec`
- one local `Home` navigation model underneath
- multiple focused views for different ways of understanding UM
- one interactive explorer centered on concrete use cases

The key shift is:

**do not organize the homepage primarily by audience category; organize it by use-case and understanding path.**

That lets multiple audiences find themselves through the concrete problem they care about instead of being forced through generic audience copy.

That does **not** mean audience pathways are unimportant. It means they should live one layer down as dedicated landing pages rather than competing with the homepage for first-contact attention.

## What the homepage must optimize for now

The public front door should optimize for:

1. **first-contact comprehension**
2. **concrete use-case discovery**
3. **clear relationship to the latest spec**
4. **progressive depth rather than one-page overload**

It should not try to optimize for:

- summarizing the entire project,
- teaching the whole architecture in one screen,
- or routing every possible visitor from a single hero section.

## Global navigation rule

Keep the public global menu exactly as it is now:

- `Home`
- `Latest Spec`

That part is already correct.

The change should happen **inside the Home cluster**, not in the global nav.

## Recommended home-cluster architecture

The `Home` surface should become a family of related pages with a local tab bar that appears under the global header.

### Recommended local `Home` tabs

1. **Overview**
2. **Use Cases**
3. **Explorer**
4. **How It Works**
5. **Standards Fit**

## Recommended home-cluster sitemap

This is the recommended route model.

### Global public routes

- `/` — Home cluster landing page (`Overview`)
- `/spec/latest/` — latest public draft specification

### Home-cluster local routes

- `/` — **Overview**
  - one-screen orientation
  - plain-language definition
  - short problem framing
  - clear path into explorer or spec

- `/use-cases/` — **Use Cases**
  - curated narrative index of the strongest use cases
  - grouped by domain
  - reader-oriented, not interactive-first

- `/explorer/` — **Explorer**
  - interactive use-case explorer
  - left-rail selection + large hero/detail pane
  - metaverse portaling as default first lane

- `/how-it-works/` — **How It Works**
  - simplest explanation of the manifest model
  - what travels
  - what stays authoritative elsewhere
  - how expiry, consent, and pointers fit

- `/standards-fit/` — **Standards Fit**
  - what UM is and is not
  - how it relates to VCs, DIDComm, Solid, resolver/runtime patterns, and standards-track discussion

### Supporting, non-tab surfaces

These should remain available, but they should not be the primary local tabs:

- `/docs/`
- `/about/one-pager/`
- `/learning/`
- `/sandbox/`
- `/workbench/`
- `/proof/*`

They are support surfaces, not the primary public onboarding structure.

## Audience landing pages should exist, but not on the homepage

This is the key refinement.

The homepage should be:

- use-case-first,
- depth-aware,
- and low-noise.

Audience-specific entry pages should still exist, but as a **separate route family that the homepage and explorer can direct into**.

### Recommended audience-landing route family

- `/audiences/metaverse/`
- `/audiences/eu-ssi/`
- `/audiences/platforms/`
- `/audiences/privacy-and-consent/`
- `/audiences/venues-and-spatial/`
- `/audiences/credential-and-personhood/`

### What these pages should do

Each audience landing page should answer:

- why UM matters to this audience,
- which use cases matter most to them,
- how UM fits their current ecosystem,
- which adjacent standards or initiatives are most relevant,
- what proof or implementation surfaces they should inspect next.

### Why this separation matters

This avoids two failure modes:

1. the homepage turning into a giant audience taxonomy,
2. the project losing critical strategic audiences such as EU self-sovereign identity because the homepage can only foreground one story at a time.

So the correct split is:

- homepage and home-cluster tabs = use-case and understanding-path navigation
- audience landing pages = downstream tailored entry points

## Why this route model is better

It solves four current problems at once:

1. The root page no longer has to carry everything.
2. The `Home` experience can serve multiple audiences without becoming vague.
3. The site gets a progressive-depth model.
4. The global menu stays calm.

## Domain-of-thought audit

The project should now be thought of in six public-facing domains of thought.

### 1. The problem

Question:

- What is broken in the world that UM helps solve?

Content themes:

- repeated profile rebuilding
- consent not traveling
- pairwise custom integrations
- offline trust gaps
- fragmented subject context across surfaces

Best current source material:

- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/about/why-um.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/about/one-pager.md`

### 2. The object

Question:

- What is Universal Manifest, exactly?

Content themes:

- portable document format
- envelope/container/capsule model
- identity, claims, consent, devices, pointers
- validity windows and optional integrity

Best current source material:

- `/Users/grig/work/repo/universalmanifest/README.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/universal-manifest-overview.md`

### 3. The use cases

Question:

- Where does UM actually help?

Content themes:

- metaverse portaling
- avatars and content portability
- smart-glasses consent
- social/profile portability
- venue and edge-device trust
- proof-of-personhood portability
- enterprise or cross-platform permissions

Best current source material:

- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/use-cases/*.md`
- `/Users/grig/work/repo/universalmanifest/integrations/`

### 4. The model

Question:

- How does it work at a conceptual level?

Content themes:

- subject
- facets / records
- pointers
- consent and policy
- TTL / expiry
- projection by receiving systems

Best current source material:

- `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/universal-manifest-overview.md`

### 5. The standards boundary

Question:

- How does UM relate to other standards and why is it different?

Content themes:

- not another auth protocol
- not another database
- not a replacement for all adjacent standards
- works with VCs, DIDs, pointer-based systems, and subject runtimes

Best current source material:

- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/about/standards-landscape.md`
- `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md`

### 6. The proof layer

Question:

- Is this just an idea, or is it real?

Content themes:

- sandbox
- workbench
- journeys
- fixtures
- resolver
- conformance

Best current source material:

- `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
- `/Users/grig/work/repo/universalmanifest/docs/COMPREHENSIVE-PROJECT-PROPERTIES-AND-SURFACES-MAP.md`

## Levels of depth

The project also needs a stable depth model so that pages stop mixing explanation levels.

### Level 0 — Glance

Goal:

- "What is this?"

Best surface:

- `Overview`

### Level 1 — Human explanation

Goal:

- "Why does this matter and where would I use it?"

Best surfaces:

- `Use Cases`
- `Explorer`

### Level 2 — Evaluator model

Goal:

- "How does it work and how does it fit with adjacent standards?"

Best surfaces:

- `How It Works`
- `Standards Fit`

### Level 3 — Implementer depth

Goal:

- "What is the actual contract and proof surface?"

Best surfaces:

- `/spec/latest/`
- `/docs/`
- `/conformance/`
- `/sandbox/`
- `/workbench/`

## Content-positioning decision

The homepage should be **use-case-first**, not **audience-card-first**.

That does not ignore different audiences. It simply lets them converge through real scenarios instead of abstract segmentation.

For Universal Manifest, that is especially important because the most persuasive current lane is not generic identity exchange. One lead lane is:

- **metaverse portaling**
- **avatar portability**
- **portable content and policy across digital worlds**

This should become the leading public explorer lane because it reflects the current strategic adoption posture around Metaverse Standards Forum consideration.

But it should not become the only strategic audience story. The project also needs dedicated audience-facing routes for other critical pathways, especially the evolving EU self-sovereign identity and digital-identity ecosystem.

## Recommended explorer concept

The explorer should become the centerpiece of the `Home` cluster, but as a dedicated page or tab view rather than a giant section forced into the root page.

### Explorer behavior

- full-screen or near-full-screen component
- fixed left rail
- large main pane taking roughly 75% of the width
- non-infinite-scroll experience
- click-to-explore rather than read-through-everything

### Left-rail structure

The left rail should list the major use-case lanes, not audiences.

Recommended order:

1. Metaverse Portaling
2. Avatars and Portable Identity
3. Content and Asset Projection
4. Smart-Glasses Consent
5. Social/Profile Portability
6. Venue and Edge Devices
7. Proof of Personhood
8. Enterprise and Cross-System Permissions

### Main-pane structure for each lane

Each explorer lane should include:

1. **Hero graphic**
   - visually explains the lane
2. **Exact headline**
   - states the use case directly
3. **Short summary**
   - what happens in this scenario
4. **Why UM fits**
   - why a portable manifest helps here
5. **What actually travels**
   - identity, avatar settings, permissions, content pointers, claims, etc.
6. **Expandable deep detail**
   - enough substance to persuade serious evaluators
7. **Proof or related links**
   - spec, docs, integrations, sandbox, or journeys where relevant

## Metaverse-first content priority

The first lane should be explicitly:

### Metaverse Portaling

Core public story:

- a subject moves between digital worlds,
- identity and avatar-related state can travel,
- content pointers and permissions can travel,
- receiving worlds can project only what they understand and are allowed to use,
- the manifest is the portable carrying document, not the entire world database.

This lane is the best current lead because it combines:

- strategic standards relevance,
- visual explainability,
- strong differentiator value,
- and a direct line back to the project's lineage.

## What existing material should seed the new home cluster

### Use directly as source material

- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/about/why-um.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/about/one-pager.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/universal-manifest-overview.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/about/standards-landscape.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/use-cases/*.md`
- `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`
- `/Users/grig/work/repo/universalmanifest/integrations/rp1-spatial-fabric.md`
- `/Users/grig/work/repo/universalmanifest/integrations/smart-glasses.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/did-vc.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/about/standards-positioning.md`

### Do not use as primary homepage voice

- current homepage copy in `site/src/pages/index.astro`
- internal publication-strategy language from prior homepage passes
- route-architecture explanation as public-facing body copy

## Content-first execution order

This should happen in this order:

### Step 1 — Sitemap and IA

Done in this report.

### Step 2 — Content architecture by page

For each home-cluster route, define:

- goal
- reader level
- source files
- what belongs there
- what does not

### Step 3 — Explorer content packs

Write the actual content payloads for the explorer lanes, beginning with:

1. Metaverse Portaling
2. Avatars and Portable Identity
3. Content and Asset Projection

Only once those are strong should additional lanes be filled in.

### Step 4 — Audience landing-page content packs

Write tailored audience pages beginning with:

1. Metaverse
2. EU self-sovereign identity
3. App and platform teams

These pages should reuse the same source material but reframe it around adoption questions specific to each audience.

### Step 5 — Home-cluster UI implementation

Build:

- local `Home` tabs,
- the home-cluster route family,
- the explorer component,
- and the revised root overview page.

### Step 6 — Migration and cleanup

After the new cluster is live:

- decide which existing reader routes remain primary,
- which become support routes,
- and which should be re-homed or de-emphasized.

## Bottom line

The next homepage wave should not be "write a better homepage."

It should be:

- create a real `Home` cluster,
- organize it around use cases and understanding depth,
- lead with metaverse portability,
- add separate audience landing pages rather than collapsing them into the homepage,
- write the content before building the UI,
- and keep the global navigation calm.

That is the cleanest path to a homepage that is more persuasive, less sloppy, and more faithful to what Universal Manifest actually is.
