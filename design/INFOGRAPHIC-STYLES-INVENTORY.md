# Infographic Styles Inventory — Universal Manifest

> **Purpose:** Complete inventory of every infographic, diagram, animated SVG, and visual asset needed across the project. Use this as the briefing document for the infographics generation agent.
>
> **Date:** 2026-02-26
> **Total assets:** 56 (32 exist, 24 need creation)

---

## Color System & Visual Language

All visuals must use a consistent design language:

- **Background:** Dark (#0f172a)
- **Accent / Primary:** Bright blue (#3b82f6)
- **Consent Allowed:** Green (#22c55e)
- **Consent Denied:** Red (#ef4444)
- **Consent Unset:** Gray (#6b7280)
- **Manifest Glow:** Warm white / gold edge glow on dark matte card
- **Style Reference:** Stripe / Notion / Arc Browser — clean, modern, confident
- **Technical Constraints:** See `docs/design/ANIMATED-SVG-SPEC.md` for accessibility, performance budgets, and reduced-motion support requirements

---

## Style Types Used in This Inventory

| Style | Description |
|-------|-------------|
| `animated-svg` | SVG with CSS/SMIL animation, looping or triggered |
| `static-diagram` | Non-animated SVG or PNG diagram |
| `flowchart` | Decision-tree or process-flow diagram |
| `sequence-diagram` | Ordered interaction between actors/systems |
| `illustration` | Artistic/conceptual depiction |
| `character-illustration` | Named character design for use across animations |
| `icon-set` | Coherent set of small icons sharing one style |
| `journey-map` | Timeline-style user experience flow |
| `comparison-diagram` | Side-by-side or matrix comparing concepts |
| `motion-graphics` | Full animation script (video-length storyboard) |

---

## Category 1: Core Concept Explainers

### 1.1 Swiss Army Knife Metaphor

- **ID:** `swiss-army-knife-metaphor`
- **Style:** illustration, static-diagram
- **Subject:** Manifest as a compact card with fold-out panels (shards)
- **Visual Direction:** Glowing credit-card-sized rounded rectangle, matte dark material with bright-blue edge glow, circular emblem/seal on front, UMID engraved on bottom edge, fold-out panels like Swiss Army Knife tools
- **Status:** needs-creation
- **Priority:** critical
- **Source:** `docs/explainers/animation-briefing.md`

### 1.2 Core Flow Pipeline

- **ID:** `um-core-flow-pilot`
- **Style:** animated-svg
- **Subject:** Resolve → Validate → Consume pipeline
- **Visual Direction:** Three-stage sequential animation showing manifest being fetched, validated, and consumed
- **Status:** exists
- **Existing Asset:** `site/public/animations/um-core-flow-pilot.svg`
- **Priority:** critical

### 1.3 Overlay Lanes Integration

- **ID:** `um-overlay-lanes-pilot`
- **Style:** animated-svg
- **Subject:** How different integration lanes connect to one shared UM envelope
- **Visual Direction:** Central manifest with branching lanes for different use cases
- **Status:** exists
- **Existing Asset:** `site/public/animations/1.3-overlay-lanes.svg`
- **Priority:** critical

### 1.4 System Overview

- **ID:** `universal-manifest-overview-template`
- **Style:** static-diagram (planned upgrade to animated)
- **Subject:** Complete system architecture showing components and relationships
- **Visual Direction:** Dark background, clean lines; should be upgraded to animated form per WO-0042
- **Status:** exists
- **Existing Asset:** `site/public/diagrams/1.4-system-overview.svg`
- **Priority:** high

---

## Category 2: Visual Vocabulary (Reusable Elements)

These are foundational visual elements reused across all other visuals. **Build these first.**

### 2.1 Manifest Card

- **ID:** `visual-manifest-card`
- **Style:** illustration, icon
- **Subject:** The manifest itself as a tangible object
- **Visual Direction:** Glowing card with seal, UMID visible, floats slightly, rotates gently when idle, glows brighter when active
- **Status:** needs-creation
- **Priority:** critical

### 2.2 Shards (Fold-Out Panels)

- **ID:** `visual-shards`
- **Style:** animated-illustration
- **Subject:** Compartments folding out from manifest, each with distinct icon
- **Visual Direction:** Bright-blue panels with icons — silhouette (profile), device/screen (device), building/shield (venue), controller/trophy (game), badge/certificate (credentials). Mechanical smooth fold-out animation.
- **Status:** needs-creation
- **Priority:** high

### 2.3 Pointers (Tether Lines)

- **ID:** `visual-pointers`
- **Style:** animated-illustration
- **Subject:** Luminous arrows/beams extending from manifest to external systems
- **Visual Direction:** Thin bright-blue luminous arrows with pulsing animation, data-packets traveling along arrows when fetched
- **Status:** needs-creation
- **Priority:** high

### 2.4 Consent Locks

- **ID:** `visual-consent-locks`
- **Style:** animated-illustration
- **Subject:** Lock icons on shard panels indicating permission state
- **Visual Direction:** Green (unlocked/allowed), red (locked/denied), gray (not-set/denied-by-default). Toggle flip animation with click sound, denial flash, approval glow.
- **Status:** needs-creation
- **Priority:** high

### 2.5 TTL Timer

- **ID:** `visual-ttl-timer`
- **Style:** animated-illustration
- **Subject:** Countdown timer or hourglass showing validity window
- **Visual Direction:** Timer in top-right corner, starts bright-blue, transitions to amber (last 20%), then red at expiry. Manifest becomes translucent/gray when expired.
- **Status:** needs-creation
- **Priority:** medium

### 2.6 UMID Serial Number

- **ID:** `visual-umid`
- **Style:** illustration
- **Subject:** Serial number display on manifest
- **Visual Direction:** Engraved along bottom edge as formatted URN (urn:uuid:...), glows during resolver lookup with search beam
- **Status:** needs-creation
- **Priority:** medium

### 2.7 Resolver Service

- **ID:** `visual-resolver`
- **Style:** animated-illustration
- **Subject:** myum.net resolver as secure storage
- **Visual Direction:** Locker room or filing cabinet with glowing slots, each containing a manifest. Query illuminates matching slot, manifest slides out. Deep blue-gray interior with bright-blue accents.
- **Status:** needs-creation
- **Priority:** medium

### 2.8 Validation Checkpoint

- **ID:** `visual-validation`
- **Style:** animated-illustration
- **Subject:** Manifest passing through validation scanner
- **Visual Direction:** Scanner gate with sweeping beam, green checkmark (pass) or red X (fail). Scanning hum sound, approval/denial tones.
- **Status:** needs-creation
- **Priority:** medium

---

## Category 3: Character Illustrations

Four named characters used across animation scripts and journeys. Must have consistent appearance everywhere.

### 3.1 Alex (The Creator)

- **ID:** `character-alex`
- **Style:** character-illustration
- **Subject:** Young adult freelance artist
- **Visual Direction:** Creative casual clothing, carries tablet/sketchpad, manifest floating near shoulder or glowing in pocket, enthusiastic personality
- **Status:** needs-creation
- **Priority:** medium

### 3.2 Jordan (The Venue Operator)

- **ID:** `character-jordan`
- **Style:** character-illustration
- **Subject:** Professional gallery/venue manager
- **Visual Direction:** Professional but approachable, standing at gallery entrance or control panel, environment has validation scanners and displays, practical security-conscious personality
- **Status:** needs-creation
- **Priority:** medium

### 3.3 Sam (The App Developer)

- **ID:** `character-sam`
- **Style:** character-illustration
- **Subject:** Software developer building with UM
- **Visual Direction:** Hoodie, laptop, coffee, surrounded by floating code snippets and API endpoints, at desk with multiple screens, efficiency-driven personality
- **Status:** needs-creation
- **Priority:** medium

### 3.4 Riley (The Privacy Guardian)

- **ID:** `character-riley`
- **Style:** character-illustration
- **Subject:** Privacy advocate controlling permissions
- **Visual Direction:** Composed, deliberate, manifest with many visible red locks, interacts carefully with consent toggles, protective thoughtful personality
- **Status:** needs-creation
- **Priority:** medium

---

## Category 4: Animation Scripts (Explainer Videos)

Full-length animated explainer storyboards. Each is a multi-scene narrative.

### 4.1 "What Is Universal Manifest?" (60-90s)

- **ID:** `anim-script-what-is-um`
- **Style:** animated-svg, motion-graphics
- **Scenes:** 5 — Problem (fragmentation) → Metaphor (Swiss Army Knife) → How It Works (4 beats) → Promise (before/after) → CTA
- **Visual Direction:** Dark background, manifest glows warm white/gold, consent toggles (green/red/gray), shards with distinct accent colors, Stripe/Notion-style
- **Status:** needs-creation
- **Priority:** critical
- **Source:** `docs/scripts/script-what-is-um.md`

### 4.2 "How Universal Manifest Works" (90-120s)

- **ID:** `anim-script-how-it-works`
- **Style:** animated-svg, motion-graphics
- **Scenes:** 6 — Meet the Manifest → Shards (tools) → Consent (locks) → Publishing/Resolving → Validation → Result
- **Visual Direction:** Swiss Army Knife transformation, mechanical fold-out animations, validation checkpoint gates, metallic clicks, clean electronic track
- **Status:** needs-creation
- **Priority:** critical
- **Source:** `docs/scripts/script-how-it-works.md`

### 4.3 "Why Universal Manifest Matters" (60-90s)

- **ID:** `anim-script-why-it-matters`
- **Style:** animated-svg, vignette-driven
- **Scenes:** 7 — Intro → Gallery (Alex) → Smart Glasses (Riley) → Virtual World (Nova) → Proof (Sam) → New Device → Close
- **Visual Direction:** Cinematic micro-stories, Apple/Notion style, confident visual tone, each vignette self-contained, punchy reveals
- **Status:** needs-creation
- **Priority:** high
- **Source:** `docs/scripts/script-why-it-matters.md`

### 4.4 "A Day with Universal Manifest" (2-3min)

- **ID:** `anim-script-day-in-the-life`
- **Style:** animated-svg, lifestyle-video
- **Scenes:** 6 — Morning (update) → Midday (gallery) → Afternoon (app) → Evening (VR) → Night (review) → Close
- **Visual Direction:** Warm personal grounded tone, technology recedes into background, human-centered, Arc Browser/Notion lifestyle feel
- **Status:** needs-creation
- **Priority:** high
- **Source:** `docs/scripts/script-day-in-the-life.md`

---

## Category 5: Scenario Animations (WO-0042 Upgrades)

Existing animations that need regeneration or are missing entirely.

### 5.1 Object Model Structure

- **ID:** `scenario-01-um-object-model`
- **Style:** static-diagram
- **Subject:** Visual breakdown of manifest structure — @context, @id, @type, shards, claims, consents, pointers
- **Status:** exists
- **Existing Asset:** `site/public/diagrams/5.1-object-model.svg`
- **Priority:** high

### 5.2 Consent Policy Flow

- **ID:** `scenario-03-consent-policy-flow`
- **Style:** animated-svg
- **Subject:** How consent toggles gate access to shards and data
- **Status:** exists
- **Existing Asset:** `site/public/animations/5.2-consent-policy-flow.svg`
- **Priority:** high

### 5.3 User Journey Sequence

- **ID:** `scenario-04-user-journey-sequence`
- **Style:** animated-svg, sequence-diagram
- **Subject:** End-to-end user flow from manifest creation to consumption
- **Status:** exists
- **Existing Asset:** `site/public/animations/5.3-user-journey-sequence.svg`
- **Priority:** high

### 5.4 Motion Tutorial (Objects and Icons)

- **ID:** `scenario-06-motion-tutorial-objects-and-icons`
- **Style:** animated-svg
- **Subject:** Tutorial showing how visual objects and icons move/interact
- **Status:** exists
- **Existing Asset:** `site/public/animations/5.4-motion-tutorial.svg`
- **Priority:** medium

---

## Category 6: Tool Explainers (WO-0043)

### 6.1 Workbench Explainer

- **ID:** `scenario-07-workbench-explainer`
- **Style:** animated-svg
- **Subject:** Editor lifecycle — import → edit → validate → export
- **Status:** exists
- **Existing Asset:** `site/public/animations/6.1-workbench-explainer.svg`
- **Priority:** high

### 6.2 Verification Harness Explainer

- **ID:** `scenario-08-harness-explainer`
- **Style:** animated-svg
- **Subject:** Fixture load → quick checks → resolver probe → evidence capture
- **Status:** exists
- **Existing Asset:** `site/public/animations/6.2-harness-explainer.svg`
- **Priority:** high

---

## Category 7: Integration Lane Animations (Existing Lanes)

### 7.1 Social Profile

- **ID:** `scenario-09-social-integration`
- **Style:** animated-svg
- **Subject:** Portable social profiles between platforms via publicProfile shard
- **Status:** exists
- **Existing Asset:** `site/public/animations/7.1-social-integration.svg`
- **Priority:** high

### 7.2 Proof-of-Personhood

- **ID:** `scenario-10-pop-integration`
- **Style:** animated-svg
- **Subject:** Multi-provider personhood verification through UM claims
- **Status:** exists
- **Existing Asset:** `site/public/animations/7.2-pop-integration.svg`
- **Priority:** high

### 7.3 OMATrust

- **ID:** `scenario-11-omatrust-integration`
- **Style:** animated-svg
- **Subject:** Trust attestations and reputation claims in manifests
- **Status:** exists
- **Existing Asset:** `site/public/animations/7.3-omatrust-integration.svg`
- **Priority:** high

### 7.4 RP1 Spatial Fabric

- **ID:** `scenario-12-rp1-integration`
- **Style:** animated-svg
- **Subject:** Spatial fabric identity and permissions
- **Status:** exists
- **Existing Asset:** `site/public/animations/7.4-rp1-integration.svg`
- **Priority:** high

### 7.5 Smart Glasses AR

- **ID:** `scenario-13-smart-glasses-integration`
- **Style:** animated-svg
- **Subject:** AR recording consent controls via manifest
- **Status:** exists
- **Existing Asset:** `site/public/animations/7.5-smart-glasses-integration.svg`
- **Priority:** high

### 7.6 Metaverse

- **ID:** `scenario-14-metaverse-integration`
- **Style:** animated-svg
- **Subject:** Portable avatar and identity across virtual worlds
- **Status:** exists
- **Existing Asset:** `site/public/animations/7.6-metaverse-integration.svg`
- **Priority:** high

### 7.7 Chia VC

- **ID:** `scenario-15-chia-vc-integration`
- **Style:** animated-svg
- **Subject:** Blockchain-based verifiable credentials in UM manifests
- **Status:** exists
- **Existing Asset:** `site/public/animations/scenario-15-chia-vc-integration.svg`
- **Priority:** high

---

## Category 8: New Integration Lane Visuals

### 8.1 Healthcare Patient Consent

- **ID:** `integration-healthcare-patient-consent`
- **Style:** animated-svg, flowchart
- **Subject:** Patient sharing emergency contacts and allergy info with clinic via UMID
- **Visual Direction:** Patient manifest with allergyAlerts and emergencyContact shards, consent toggles for health.shareEmergencyInfo and health.shareAllergies, clinic system checking consent before displaying
- **Status:** exists
- **Existing Asset:** `site/public/animations/8.1-healthcare-consent.svg`
- **Priority:** medium
- **Source:** `integrations/healthcare-patient-consent.md`

### 8.2 Education Credentials

- **ID:** `integration-education-credentials`
- **Style:** animated-svg, flowchart
- **Subject:** Job applicant sharing UMID with employer to verify degree and skills
- **Visual Direction:** Student manifest with academicCredential and skillAttestation shards, employer checking edu.verifyDegree consent, verification endpoints for transcript and certifications
- **Status:** exists
- **Existing Asset:** `site/public/animations/8.2-education-credentials.svg`
- **Priority:** medium
- **Source:** `integrations/education-credentials.md`

### 8.3 Smart Home Device Management

- **ID:** `integration-smart-home`
- **Style:** animated-svg, flowchart
- **Subject:** New smart device reading home manifest and applying household privacy policies
- **Visual Direction:** Home network manifest with homePolicy shard, new device enrolling and inheriting consent settings (home.shareUsageData denied, home.allowRemoteAccess denied)
- **Status:** exists
- **Existing Asset:** `site/public/animations/8.3-smart-home.svg`
- **Priority:** medium
- **Source:** `integrations/smart-home.md`

---

## Category 9: Commercial Journey Maps

### 9.1 Freelance Creator Journey

- **ID:** `journey-creator`
- **Style:** journey-map, sequential-diagram
- **Subject:** Alex creating manifest → UMID submission → gallery fetch → art display → portfolio update propagation
- **Status:** exists
- **Existing Asset:** `site/public/diagrams/9.1-creator-journey.svg`
- **Priority:** medium
- **Source:** `docs/journeys/commercial/creator-journey.md`

### 9.2 Venue Operator Journey

- **ID:** `journey-venue-operator`
- **Style:** journey-map, sequential-diagram
- **Subject:** Jordan onboarding artists and devices — UMID input → manifest fetch → validation → content display → device enrollment → TTL expiry cleanup
- **Status:** exists
- **Existing Asset:** `site/public/diagrams/9.2-venue-operator-journey.svg`
- **Priority:** medium
- **Source:** `docs/journeys/commercial/venue-operator-journey.md`

### 9.3 App Developer Journey

- **ID:** `journey-app-developer`
- **Style:** journey-map, sequential-diagram
- **Subject:** Sam integrating UM into social platform — TS helper install → UMID resolution → shard reading → consent checking → signature verification → consent revocation handling
- **Status:** exists
- **Existing Asset:** `site/public/diagrams/9.3-app-developer-journey.svg`
- **Priority:** medium
- **Source:** `docs/journeys/commercial/app-developer-journey.md`

### 9.4 Privacy-Conscious User Journey

- **ID:** `journey-privacy-user`
- **Style:** journey-map, sequential-diagram
- **Subject:** Riley controlling consent — manifest creation (all denied) → selective grants → platform checks → AR enforcement → activity log review → TTL expiry as retention policy
- **Status:** exists
- **Existing Asset:** `site/public/diagrams/9.4-privacy-user-journey.svg`
- **Priority:** medium
- **Source:** `docs/journeys/commercial/privacy-journey.md`

### 9.5 Enterprise Integrator Journey

- **ID:** `journey-enterprise-integrator`
- **Style:** journey-map, sequential-diagram
- **Subject:** Morgan building venue management software — consumer implementation → device enrollment shards → OMATrust claims → multi-provider personhood → integration template contribution
- **Status:** exists
- **Existing Asset:** `site/public/diagrams/9.5-enterprise-journey.svg`
- **Priority:** low
- **Source:** `docs/journeys/commercial/enterprise-journey.md`

---

## Category 10: Technical Diagrams

### 10.1 Manifest Lifecycle

- **ID:** `manifest-lifecycle`
- **Style:** sequence-diagram
- **Subject:** Create → Publish → Resolve → Validate → Consume (five-stage lifecycle with data flow between issuer, resolver, consumer)
- **Status:** exists
- **Existing Asset:** `site/public/diagrams/10.1-manifest-lifecycle.svg`
- **Priority:** high
- **Source:** `docs/explainers/full-briefing.md`

### 10.2 Default-Deny Consent Model

- **ID:** `consent-default-deny`
- **Style:** flowchart, decision-tree
- **Subject:** Consent name lookup → present? → value = allowed? → grant/deny. Default branch to "deny" for missing consent.
- **Status:** exists
- **Existing Asset:** `site/public/diagrams/10.2-default-deny-consent.svg`
- **Priority:** high
- **Source:** `docs/explainers/full-briefing.md`, `docs/journeys/commercial/privacy-journey.md`

### 10.3 TTL and Expiry Enforcement

- **ID:** `ttl-expiry`
- **Style:** animated-diagram, timeline
- **Subject:** issuedAt → expiresAt window, countdown timer, manifest becoming invalid (gray/translucent) at expiry
- **Status:** exists
- **Existing Asset:** `site/public/diagrams/10.3-ttl-expiry.svg`
- **Priority:** high
- **Source:** `docs/explainers/full-briefing.md`

### 10.4 Shard Modularity

- **ID:** `shard-modularity`
- **Style:** static-diagram
- **Subject:** How different shards compose into one manifest — publicProfile, deviceIdentity, venuePolicy, claims as visually distinct sections
- **Status:** exists
- **Existing Asset:** `site/public/diagrams/10.4-shard-modularity.svg`
- **Priority:** medium
- **Source:** `docs/explainers/full-briefing.md`

### 10.5 Pointer vs. Embedded Data

- **ID:** `pointer-resolution`
- **Style:** comparison-diagram
- **Subject:** Difference between copying data into manifest vs. storing pointer to canonical source. Metaphor: photocopy vs. business card with URL.
- **Status:** exists
- **Existing Asset:** `site/public/diagrams/10.5-pointer-vs-embedded.svg`
- **Priority:** medium
- **Source:** `docs/explainers/full-briefing.md`

### 10.6 Signature Verification (v0.2)

- **ID:** `signature-verification-v02`
- **Style:** flowchart
- **Subject:** Manifest with signature → strip signature field → canonicalize with JCS → verify Ed25519 with public key → valid/invalid result
- **Status:** exists
- **Existing Asset:** `site/public/diagrams/10.6-signature-verification.svg`
- **Priority:** medium
- **Source:** `docs/explainers/full-briefing.md`, `docs/journeys/commercial/app-developer-journey.md`

---

## Category 11: Comparison & Positioning Diagrams

### 11.1 UM vs. Other Standards

- **ID:** `standards-comparison`
- **Style:** comparison-table, venn-diagram
- **Subject:** How UM relates to VCs, DIDComm, OIDC, Solid — overlap and complementarity
- **Visual Direction:** Matrix or Venn showing: VCs (individual claims), DIDComm (messaging), Solid (storage), OIDC (auth), UM (portable state container)
- **Status:** exists
- **Existing Asset:** `site/public/diagrams/11.1-um-vs-standards.svg`
- **Priority:** low
- **Source:** `docs/explainers/full-briefing.md`

### 11.2 Progressive Adoption Levels

- **ID:** `progressive-adoption`
- **Style:** staircase-diagram, progression-chart
- **Subject:** Level 1 (parse) → Level 2 (validate) → Level 3 (consume shards) → Level 4 (issue) → Level 5 (sign/verify)
- **Visual Direction:** Ascending staircase or building blocks, each level building on previous
- **Status:** exists
- **Existing Asset:** `site/public/diagrams/11.2-progressive-adoption.svg`
- **Priority:** medium
- **Source:** `docs/explainers/full-briefing.md`, `docs/journeys/commercial/app-developer-journey.md`

---

## Category 12: Icon Sets

### 12.1 Core Concept Icons

- **ID:** `icon-set-core-concepts`
- **Style:** icon-set
- **Subject:** Icons for UMID, TTL, shards, pointers, consents, claims, subject, resolver
- **Visual Direction:** Consistent line-based or filled style, bright-blue accent, recognizable at small sizes
- **Status:** needs-creation
- **Priority:** high

### 12.2 Shard Type Icons

- **ID:** `icon-set-shard-types`
- **Style:** icon-set
- **Subject:** Profile (silhouette), device (screen), venue (building/shield), game (controller/trophy), credentials (badge/certificate)
- **Visual Direction:** Simple recognizable symbols for use on fold-out panels in animations
- **Status:** needs-creation
- **Priority:** high

### 12.3 Integration Lane Icons

- **ID:** `icon-set-integration-lanes`
- **Style:** icon-set
- **Subject:** One icon per lane — social, proof-of-personhood, OMATrust, RP1, smart glasses, metaverse, Chia, healthcare, education, smart home
- **Visual Direction:** Distinct visual identity per lane, consistent size/style
- **Status:** needs-creation
- **Priority:** medium

---

## Category 13: Real-World Scenario Illustrations

### 13.1 Gallery Use Case

- **ID:** `scenario-gallery`
- **Style:** illustrated-scenario
- **Subject:** Alex entering gallery, manifest communication beam, screens lighting up with art, consent check visible
- **Status:** needs-creation
- **Priority:** medium
- **Source:** `docs/explainers/full-briefing.md`, `docs/scripts/script-why-it-matters.md`

### 13.2 AR Privacy Scenario

- **ID:** `scenario-ar-privacy`
- **Style:** illustrated-scenario
- **Subject:** Riley's face blurred in AR glasses due to consent denial, shield icon indicator
- **Status:** needs-creation
- **Priority:** medium
- **Source:** `docs/explainers/full-briefing.md`, `docs/scripts/script-why-it-matters.md`

### 13.3 Cross-Platform Gaming

- **ID:** `scenario-gaming`
- **Style:** illustrated-scenario
- **Subject:** Player profile/avatar moving between two visually distinct game worlds, manifest as connecting element
- **Status:** needs-creation
- **Priority:** low
- **Source:** `docs/explainers/full-briefing.md`

### 13.4 Offline Device Enrollment

- **ID:** `scenario-offline-device`
- **Style:** illustrated-scenario
- **Subject:** Remote venue device operating with cached manifest, no internet, TTL countdown, automatic expiry cleanup
- **Status:** needs-creation
- **Priority:** low
- **Source:** `docs/explainers/full-briefing.md`

---

## Summary

| Metric | Count |
|--------|-------|
| **Total assets** | 56 |
| Exist (no work needed) | 32 |
| Need creation | 24 |

**By priority:**

| Priority | Count |
|----------|-------|
| Critical | 6 |
| High | 23 |
| Medium | 23 |
| Low | 4 |

**By style:**

| Style | Count |
|-------|-------|
| animated-svg | 28 |
| illustration / illustrated-scenario | 12 |
| icon-set | 3 |
| flowchart / decision-tree | 5 |
| sequence-diagram | 3 |
| journey-map | 5 |
| character-illustration | 4 |
| static-diagram | 4 |
| comparison-diagram | 2 |

## Recommended Build Order

1. **Icon Sets** (Category 12) — foundational elements reused everywhere
2. **Visual Vocabulary** (Category 2) — manifest card, shards, pointers, consent locks, TTL timer, resolver, validation checkpoint
3. **Characters** (Category 3) — Alex, Jordan, Sam, Riley with consistent appearance
4. **Technical Diagrams** (Category 10) — manifest lifecycle, consent model, TTL enforcement
5. **Animation Scripts** (Category 4) — the four explainer videos
6. **Scenario Animations** (Category 5) — WO-0042 regeneration work
7. **Integration Lane Animations** (Categories 7-8) — existing lane upgrades + new lanes
8. **Journey Maps** (Category 9) — commercial journey visualizations
9. **Comparison/Positioning** (Category 11) — standards comparison, adoption levels
10. **Scenario Illustrations** (Category 13) — real-world vignettes
