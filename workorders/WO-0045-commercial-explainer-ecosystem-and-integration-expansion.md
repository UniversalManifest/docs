# WO-0045 — Commercial Explainer Ecosystem and Integration Expansion

**Status:** IN_PROGRESS
**Created:** 2026-02-27
**Priority:** CRITICAL
**Type:** Work stream (multi-phase, multi-deliverable)

## Problem Statement

Universal Manifest has a solid technical foundation — spec, conformance, fixtures, code examples, and production infrastructure — but it lacks the commercial-friendly communication layer needed to drive adoption at scale. Specifically:

1. **No graduated explanation system.** There is no way to explain UM in a single paragraph, a single page, or a comprehensive briefing. Explanations are scattered across 12+ documents with inconsistent framing (spec-technical vs adopter-friendly vs vision-strategic).

2. **No animation scripts.** The project has animated SVG specs and placement plans, but no narrative scripts that could be produced as video explainers, motion graphics, or interactive walkthroughs with characters and visual metaphors.

3. **No commercial user journeys.** The 11 existing proof journeys (J01–J11) are technical validation artifacts. They prove the system works but don't show a non-technical person *why they should care*. There are no "day in the life" journeys showing real humans benefiting from UM.

4. **Integration docs over-index on favorites.** The current 8 integration lanes (Social, PoP, OMATrust, RP1, Smart Glasses, Metaverse, Chia, Reference Runtime) reflect the creator's initial vision priorities. Now that adoption interest spans many industries, we need a broader integration catalog with a template-driven contribution system.

5. **No agent-ready briefing materials.** When an AI agent is asked "what is Universal Manifest?", "pitch this to a developer", or "create an animation explaining this", there is no single document optimized for that handoff.

## Vision

When this work stream is complete:

- Anyone can understand what UM is in 30 seconds (paragraph), 3 minutes (one-pager), or 15 minutes (full briefing)
- Animation studios or AI animation tools have production-ready scripts with character descriptions, scene breakdowns, and visual metaphor guides
- The "Swiss Army Knife of Personal Data" metaphor is developed into a visual identity element for explainer content
- Commercial user journeys show UM through the eyes of real people: a freelance creator, a venue operator, a device manufacturer, an app developer, a privacy-conscious individual
- The integration catalog is open-ended, template-driven, and can grow from 8 to 80+ lanes without structural changes
- AI agents have optimized briefing docs they can use to pitch, explain, or create derivative content about UM

## Deliverables

### Phase A: Explanation Cascade (graduated explainers)

**A1. The Paragraph** (`docs/explainers/paragraph.md`)
A single paragraph (50-80 words) that explains what UM is to a person with zero context. No jargon. Tested against: "Could my mother understand this?"

**A2. The One-Pager** (`docs/explainers/one-pager.md`)
A single page (~500 words) that covers: what it is, what problem it solves, how it works (conceptually), who it's for, and what it enables. Written in the hybrid style guide's Why→What→How structure.

**A3. The Full Briefing** (`docs/explainers/full-briefing.md`)
A comprehensive document (~2000 words) covering: problem, solution, architecture overview, core concepts (UMID, TTL, shards, pointers, consent, signatures), integration examples, adoption path, competitive positioning, and FAQ. Suitable for a board presentation or partnership pitch.

**A4. The Agent Briefing** (`docs/explainers/agent-briefing.md`)
A structured document optimized for AI agent consumption. Contains: canonical description, key facts, positioning statements, common questions with answers, pitch angles for different audiences (developer, business, privacy advocate, standards body), and links to supporting materials. An agent reading this should be able to pitch UM competently.

**A5. The Animation Briefing** (`docs/explainers/animation-briefing.md`)
A structured handoff document for animation producers. Contains: the core metaphor ("Swiss Army Knife of Personal Data"), visual vocabulary (what manifests look like, what shards look like, what pointers look like), the "characters" (Creator, Venue, Device, App, Privacy Guardian), and scene-by-scene guidance for the three core animation scripts.

### Phase B: Animation Scripts

**B1. Script: "What Is Universal Manifest?" (60-90 seconds)** (`docs/scripts/script-what-is-um.md`)
The origin story. Introduces the problem (fragmented data), the metaphor (Swiss Army Knife), and the solution. Characters: Alex (a creator) trying to move their profile between three different apps. Shows the manifest as a glowing document that carries their identity, preferences, and permissions in one portable package.

**B2. Script: "How It Works" (90-120 seconds)** (`docs/scripts/script-how-it-works.md`)
The technical walkthrough for a non-technical audience. Shows: creating a manifest (filling out the "Swiss Army Knife"), publishing it to the resolver (putting it in a locker anyone can check), fetching it by UMID (giving someone the locker key), validating it (checking the expiry date), and reading shards (opening specific tools on the knife). Visual: manifest as an animated object with fold-out sections.

**B3. Script: "Why It Matters" (60-90 seconds)** (`docs/scripts/script-why-it-matters.md`)
The impact story. Five 10-second vignettes showing UM in action: (1) Creator's art shows up at a venue they've never visited, (2) Smart glasses respect someone's "don't record me" preference, (3) A game character moves between virtual worlds, (4) A proof-of-personhood check works without revealing personal details, (5) A device automatically enrolls at a new venue. Ends with: "One document. Every system. Your rules."

**B4. Script: "Day in the Life" (2-3 minutes)** (`docs/scripts/script-day-in-the-life.md`)
Follow one character (Sam, a mixed-media artist) through a full day where UM enables seamless, consent-driven interactions across physical and digital spaces. Morning: updates their manifest with new work. Afternoon: walks into a gallery and their art appears on screens. Evening: joins a virtual world and their reputation carries over. Night: reviews what was shared and adjusts consents for tomorrow.

### Phase C: Commercial User Journeys

Distinct from the technical proof journeys (J01–J11). These are narrative journeys showing real-world value.

**C1. The Freelance Creator** (`docs/journeys/commercial/creator-journey.md`)
**C2. The Venue Operator** (`docs/journeys/commercial/venue-operator-journey.md`)
**C3. The App Developer** (`docs/journeys/commercial/app-developer-journey.md`)
**C4. The Privacy-Conscious Individual** (`docs/journeys/commercial/privacy-journey.md`)
**C5. The Enterprise Integrator** (`docs/journeys/commercial/enterprise-journey.md`)

Each journey: persona description, scenario, step-by-step narrative (what happens, what UM does behind the scenes, what the person experiences), key UM concepts demonstrated, and "aha moment."

### Phase D: Integration Expansion

**D1. Integration Template** (`integrations/TEMPLATE.md`)
A standardized template for creating new integration lane documentation. Sections: Overview, Use Cases, Manifest Structure (suggested shards/pointers/consents), Consumer Behavior, Issuer Behavior, Example Fixture, Proof Coverage, Implementation Checklist.

**D2. Expanded Integration Catalog** (`site/src/content/docs/integrations/index.md`)
Reorganize integrations into categories. Move current 8 from being the entire integration story to being "featured" examples within a larger taxonomy:

- **Identity & Social**: Social profiles, ActivityPub/Fediverse, professional networks, dating platforms, gaming profiles
- **Trust & Verification**: Proof-of-personhood, OMATrust, KYC/AML, age verification, academic credentials
- **Spatial & Immersive**: Metaverse, RP1, smart glasses AR, VR social, digital twins, location-based services
- **IoT & Devices**: Venue displays, smart home, wearables, automotive, industrial IoT
- **Blockchain & Web3**: Chia DID/VC, Ethereum ENS, Solana DID, IPFS-backed manifests
- **Healthcare & Wellbeing**: Patient consent, health records portability, fitness data, mental health preferences
- **Commerce & Finance**: Portable loyalty programs, payment preferences, merchant trust, supply chain
- **Government & Civic**: Digital ID, voting eligibility, permit portability, cross-border credentials
- **Education**: Academic credentials, learning records, skill attestations, institutional trust
- **Media & Entertainment**: Content licensing, creator attribution, rights management, recommendation portability

**D3. Agent-Driven Integration Generator Instructions** (`docs/guides/integration-authoring-guide.md`)
Instructions that an AI agent can follow to create a new integration lane document from the template. Includes: how to identify relevant shards/pointers/consents, how to create an example fixture, naming conventions, and quality checklist.

**D4. Three New Integration Lanes** (created using the template to prove the system works)
Pick three from the expanded catalog that are NOT in the current 8. Create them as proof that the template + authoring guide produces quality output.

## Style & Voice Requirements

### For Explainers and Scripts (Phase A & B)
- Use the **hybrid writing style guide** principles: Analogy First, Why→What→How, Explicit Rationale
- Tone: Warm, confident, accessible. NOT the implementer-focused neutral voice of the spec docs
- Metaphors: Lean into "Swiss Army Knife of Personal Data" as the core visual metaphor
- Reading level: Target a smart 16-year-old. No jargon without immediate explanation
- Format: Short paragraphs, visual breaks, progressive disclosure

### For Commercial Journeys (Phase C)
- First-person narrative ("I open the app...")
- Concrete, sensory details (what they see, what happens on screen)
- The UM mechanics happen behind the scenes — the person experiences the benefit, not the protocol
- Each journey should make the reader think "I want that"

### For Integration Docs (Phase D)
- Use the existing editorial style guide (professional, neutral, implementer-oriented)
- Follow the normative/non-normative boundary pattern from existing integration docs
- Include concrete fixture examples

## Dependencies

- Existing explainer content from 12+ sources (researched, available)
- Style guides: Editorial (`docs/site/EDITORIAL-STYLE-GUIDE.md`), Hybrid Writing (`~/.agents/style-guides/writing/STYLE-GUIDE-HYBRID.md`), Animation Spec (`docs/design/ANIMATED-SVG-SPEC.md`)
- Existing proof journeys (J01-J11) for technical accuracy
- Existing integration docs (8 lanes) as patterns
- Existing stub manifests (16 fixtures) for integration reference

## Acceptance Criteria

- [ ] Explanation cascade covers paragraph, one-pager, full briefing, agent briefing, animation briefing
- [ ] All four animation scripts have complete scene breakdowns with character and visual direction
- [ ] Five commercial user journeys written in first-person narrative style
- [ ] Integration template is complete and documented
- [ ] Integration catalog page reorganized with categories
- [ ] Agent authoring guide enables autonomous integration creation
- [ ] Three new integration lanes created from template as proof
- [ ] All content reviewed against style guide requirements
- [ ] No technical inaccuracies (validated against spec and conformance)

## Sequencing

Phase A (explainers) and Phase C (commercial journeys) can run in parallel.
Phase B (animation scripts) depends on A1 and A5 for core metaphor and visual vocabulary.
Phase D (integration expansion) can run in parallel with everything else.
Within Phase D, D1 (template) must complete before D4 (new lanes).
