# WO-0030 — Animated SVG explainer prompt pack and production pipeline

**Status:** COMPLETED
**Created:** 2026-02-22

## Objective

Create a production-ready prompt/system package for an external animation-strong model to generate high-quality, full-size animated SVG explainers that make Universal Manifest understandable and adoptable for first-time audiences.

This is not a "single graphic" task; it is a multi-step design + implementation + testing pipeline for reusable motion explainers tied to real UM architecture, journeys, and integration lanes.

## Why this work matters

Current docs have strong technical depth but insufficient visual narrative for first-time understanding and adoption decisions. UM needs clear motion explainers that show:

- what UM is as a portable object/system.
- how data moves through resolve/verify/project flows.
- how user journeys map to implementation behavior.
- how overlay lanes (social, personhood, OMATrust, RP1, smart glasses, metaverse, Chia) connect to the same core envelope.

## Mandatory context grounding (source-of-truth corpus)

All prompts and generated visual specs must be grounded in these project sources:

- Vision and strategy:
  - `docs/PROJECT-VISION.md`
  - `docs/STATE-OF-THE-PROJECT.md`
  - `docs/DECISIONS.md`
  - `docs/DEPTH-AND-SCOPE.md`
- Normative and conformance contract:
  - `spec/v0.1/schema.json`
  - `spec/v0.1/schema.jsonld`
  - `spec/v0.2/schema.json`
  - `spec/v0.2/schema.jsonld`
  - `site/src/content/docs/spec/v0.1.md`
  - `site/src/content/docs/spec/v0.2.md`
  - `site/src/content/docs/conformance/v0.1.md`
  - `site/src/content/docs/conformance/v0.2.md`
- Proof and journey evidence:
  - `docs/journeys/README.md`
  - `docs/journeys/journey-04-umid-resolution-myum.md`
  - `docs/journeys/journey-06-public-profile-projection.md`
  - `docs/journeys/J10-multi-provider-personhood-coexistence.md`
  - `docs/journeys/J11-omatrust-attestation-interoperability.md`
- Integration lanes:
  - `integrations/social.md`
  - `integrations/proof-of-personhood.md`
  - `integrations/oma-trust.md`
  - `integrations/rp1-spatial-fabric.md`
  - `integrations/smart-glasses-ar.md`
  - `integrations/metaverse.md`
  - `integrations/chia-vc.md`
- UX/tool surfaces where explainers will attach:
  - `site/src/content/docs/getting-started/universal-manifest-overview.md`
  - `site/src/content/docs/index.md`
  - `site/src/content/docs/getting-started/workbench.md`
  - `site/src/content/docs/proof/harness.md`
  - `site/public/workbench/index.html`
  - `site/public/harness/index.html`
- K2B and synthesis context:
  - `.dev/ai/specs/2026-02-19-ia-delta-from-full-corpus.md`
  - `docs/reports/2026-02-20-master-forward-worklist.md`
  - `.dev/ai/reports/2026-02-20-k2b-integration-completeness-report.md`

## Scope

In scope:
- define a reusable prompt architecture for external animation model generation.
- produce a prompt pack for multiple animation scenarios.
- define technical constraints for SVG output quality, accessibility, and performance.
- define integration points in docs pages with fallback behavior.
- create QA checklist and acceptance gates for animation outputs.

Out of scope:
- replacing normative text with animation-only explanations.
- rewriting core UM spec semantics.

## Required deliverables

### 1) Prompt system package

Create a documented prompt set with:
- base system prompt (style guardrails + domain constraints).
- scenario prompts (one per animation story).
- adaptation prompts (short-form variants for hero, inline section, and full-page tutorial loops).

Expected output path:
- `.dev/ai/prompts/animation/`

### 2) Scenario prompt catalog (minimum set)

Minimum scenarios required:
- UM object model explainer (manifest as portable physical/data object).
- Resolve/verify/project runtime flow (UMID -> resolver -> verification -> projection).
- Consent and policy flow (what is shared, when, and why).
- User journey explainer (from issuer to consumer to display/service).
- Overlay lanes map (social, personhood, OMATrust, RP1, smart glasses, metaverse, Chia) anchored to one core envelope.
- Motion tutorial sequence showing unique iconography, object relationships, and timed text reveals.

### 3) Technical output spec

Define hard requirements for generated SVGs:
- responsive full-width behavior without layout shift.
- deterministic animation timing and loop controls.
- reduced-motion fallback.
- semantic labeling for accessibility.
- file size/performance budget for docs page load.

Expected output path:
- `docs/design/ANIMATED-SVG-SPEC.md`

### 4) Integration plan for docs

Create insertion plan for where each animation lands:
- overview page hero explainer.
- first-time onboarding page.
- selected integration/journey pages.

Expected output paths:
- `docs/design/ANIMATION-PLACEMENT-PLAN.md`
- `docs/design/ANIMATION-QA-CHECKLIST.md`

## Quality and narrative rules

- visuals must explain real UM architecture, not generic "web3/network" abstractions.
- motion should teach causality and sequence, not decorative movement.
- iconography must distinguish core components (manifest, subject, claims, consent, pointers, facets, resolver, verifier, consumers, overlay lanes).
- text overlays must use precise UM terminology aligned with spec/docs.
- generated narratives must be traceable back to source files listed above.

## Acceptance criteria

- [x] Prompt pack exists with base prompt + scenario prompts + adaptation prompts.
- [x] Prompt pack explicitly references the required source corpus and terminology.
- [x] At least 6 scenario prompts are delivered and independently executable.
- [x] Technical SVG spec exists with accessibility + performance constraints.
- [x] Placement plan exists with page-level mapping and rationale.
- [x] QA checklist exists and is runnable by another agent/model without extra context.
- [x] At least 2 pilot animations are generated and reviewed in local docs integration.
- [x] Build/test verification passes after pilot integration.

## Validation commands

- `cd site && npm run build`
- `cd site && npm run dev`
- `agent-browser --session um-animcheck open http://127.0.0.1:4300/`
- `agent-browser --session um-animcheck snapshot -i`

## Execution notes for assigned agents

- Do not invent architecture claims; derive from source documents.
- Preserve normative/non-normative boundaries defined in existing docs.
- Use motion to support adoption and implementation understanding, not to replace technical depth.
- Prioritize explainability for first-time readers while preserving fidelity for implementers.

## Completion evidence

- Prompt package:
  - `.dev/ai/prompts/animation/README.md`
  - `.dev/ai/prompts/animation/SYSTEM-PROMPT-UM-ANIMATION.md`
  - `.dev/ai/prompts/animation/SCENARIO-01-um-object-model.md`
  - `.dev/ai/prompts/animation/SCENARIO-02-resolve-verify-project-flow.md`
  - `.dev/ai/prompts/animation/SCENARIO-03-consent-policy-flow.md`
  - `.dev/ai/prompts/animation/SCENARIO-04-user-journey-sequence.md`
  - `.dev/ai/prompts/animation/SCENARIO-05-overlay-lanes-map.md`
  - `.dev/ai/prompts/animation/SCENARIO-06-motion-tutorial-objects-and-icons.md`
  - `.dev/ai/prompts/animation/ADAPTATION-HERO-SHORT.md`
  - `.dev/ai/prompts/animation/ADAPTATION-INLINE-MEDIUM.md`
  - `.dev/ai/prompts/animation/ADAPTATION-FULLPAGE-LOOP.md`
- Technical design artifacts:
  - `docs/design/ANIMATED-SVG-SPEC.md`
  - `docs/design/ANIMATION-PLACEMENT-PLAN.md`
  - `docs/design/ANIMATION-QA-CHECKLIST.md`
- Pilot animations and integration:
  - `site/public/animations/um-core-flow-pilot.svg`
  - `site/public/animations/um-overlay-lanes-pilot.svg`
  - `site/src/content/docs/index.md`
  - `site/src/content/docs/getting-started/universal-manifest-overview.md`
- Pilot review report:
  - `docs/reports/2026-02-22-wo-0030-pilot-animation-review.md`
