# CEO Mandate: Interactive Implementation Sandbox

**Date:** 2026-02-27
**Priority:** HIGHEST — This comes before all other work orders.
**Status:** MANDATE (not a proposal — this is a directive)

---

## The Core Problem

Nothing is more important than simple test systems that simulate what real users will use. Universal Manifest is a specification, not an implementation. Without functioning implementations that people can see, touch, and interact with, the spec is theoretical. I cannot express how important this is.

## What Must Be Built

A page on the Universal Manifest site (a subdirectory of `universalmanifest.net`) that is a **sandbox / play area** where you can see the spec in action.

### The Three-Panel Layout

- **Left panel:** The entity being represented with their Universal Manifest
- **Center panel:** The thing they are connecting to (the consuming system, the verifier, the resolver — whatever applies to the scenario)
- **Right panel:** What's happening behind the scenes — the protocol, the validation, the data flow

### Step-Through Interaction

- Users can **step through the sequence** at their own pace
- **Bubbles pop up** to explain what is going on at each step
- This is not a slideshow of graphics — this is **functioning code on the front end with JavaScript**
- If you change a value and press play again, the outcome changes
- The logic must use the **same validation logic** used by our actual validators (not a simulation of validation — real validation)

### Scenario Selection

- A **modal** pops up with **beautiful cards** showing:
  - An image representing the scenario
  - A description of what that example of Universal Manifest is
  - How it would work in the real world
- The list of scenarios will be long — design the modal to handle many entries gracefully
- When you click a card, it enters the **step-through mode** showing how that scenario works in real life

### Scenarios Must Be Real

Each scenario must be a **real, functioning implementation** — not a diagram, not a mockup, not a pre-recorded animation. The JavaScript running in the browser must:

- Parse real manifest JSON-LD
- Run real structural validation
- Run real signature verification (for v0.2 scenarios)
- Show real resolution behavior
- Reflect real conformance pass/fail outcomes

### Initial Scenario Set

The proposal must include a complete list of initial scenarios. These must cover the breadth of what Universal Manifest can do:

- Basic manifest creation and validation (v0.1)
- Manifest with facets and pointers
- Signed manifest creation and verification (v0.2)
- Resolver lookup (UMID to manifest)
- Integration lanes: social profile, IoT device, metaverse identity, smart glasses consent, RP1 spatial fabric, OMATrust, DID + VC
- Invalid manifest detection (missing fields, expired, tampered signature)
- Unknown field tolerance (forward compatibility proof)
- Cross-system projection (one manifest, multiple consumer views)

The exact list must be validated with me before implementation begins.

## Quality Bar

- This is the **first thing a potential adopter sees** when evaluating whether Universal Manifest is worth implementing
- It must be **beautiful** — not developer-tool ugly, not demo-day rough
- It must be **correct** — every validation result must match what the real conformance suite would produce
- It must be **educational** — someone who has never heard of Universal Manifest should understand what it does and why it matters after stepping through 2-3 scenarios

## Relationship to Existing Work Orders

WO-0053 (Standalone Conformance Test Suite) and WO-0054 (Reference Implementation Repository) describe related work, but they were written before this mandate and do not capture this vision. This mandate supersedes and expands those work orders. The conformance suite and reference implementation are inputs to this sandbox — the sandbox is the public-facing proof that the spec works.

## Execution Priority

This comes before:

- WO-0055 through WO-0059 (onboarding, feedback, governance)
- Any documentation clarity work
- Any governance completion work
- npm publication (explicitly deferred)

The only prerequisite is having the validation logic available in browser-compatible JavaScript, which largely already exists in `packages/universal-manifest/`.

## Deliverables Required Before Implementation

1. **Proposal** with full architecture, scenario list, and interaction design
2. **Visual sketches** (ASCII art, Mermaid diagrams, or wireframes) showing the three-panel layout, the scenario selection modal, and the step-through flow
3. **My approval** of the scenario list and visual flow before any code is written

---

**This is the thing that makes Universal Manifest real to the world. Everything else is paperwork until this exists.**
