# WO-0055 — Adopter Onboarding Document Package

**Status:** COMPLETED
**Created:** 2026-02-27
**Priority:** CRITICAL
**Blocks:** Gate G4 (Interoperability proof — enables external adopters to start)
**Dependencies:** WO-0053 (Conformance Test Suite), WO-0054 (Reference Implementation)
**Estimated effort:** 1-2 weeks

## Objective

Create a comprehensive "Implementation Guide" document package that an AI agent or human developer can consume to build a complete Universal Manifest implementation from scratch, without needing to read the entire spec repo or ask the UM maintainers for clarification.

## Why this work matters

Gate G4 requires 3+ independent implementations from 3+ organizations. The current documentation is excellent for understanding what UM is, but it does not provide a single, sequential "here is how to implement it" document. External adopters (especially AI agents working on behalf of developers) need:

1. A single entry-point document that covers everything needed to implement.
2. A decision tree for choosing conformance level.
3. Step-by-step instructions with code examples.
4. A handoff-ready format that can be passed between agents or team members.

Without this, each adopter independently discovers the implementation path by reading scattered spec files, increasing friction and reducing adoption velocity.

## Scope

In scope:

- "Universal Manifest Implementation Guide" — single comprehensive document.
- Decision tree: which conformance level to target (v0.1-baseline, v0.2-baseline, v0.2-extended).
- Step-by-step adoption walkthrough with code examples in multiple languages.
- FAQ for common implementation questions.
- Handoff-ready format optimized for agent-to-agent transfer (structured markdown with clear sections).
- Quick-reference card (single-page summary of required fields, validation rules, and conformance levels).

Out of scope:

- Writing implementations in multiple languages (that is the adopter's job).
- Modifying normative spec text.
- Building interactive tooling (covered by existing workbench).

## Execution phases

### Phase 1 — Implementation guide structure and core content

- [x] Create the implementation guide at `docs/guides/IMPLEMENTATION-GUIDE.md`:
  ```
  1. Introduction
     - What is Universal Manifest (one paragraph)
     - What this guide covers
     - Prerequisites
  2. Choose Your Conformance Level
     - Decision tree diagram
     - v0.1-baseline: what you need to implement
     - v0.2-baseline: what you additionally need
     - v0.2-extended: revocation-aware verification
  3. Step 1: Parse and Validate a Manifest
     - Required fields checklist
     - Unknown-field handling
     - TTL enforcement
     - Code examples (TypeScript, Python pseudocode, Go pseudocode)
  4. Step 2: Create a Manifest (Issuer)
     - Required fields and their semantics
     - ID generation guidance
     - Subject field guidance
     - TTL best practices
  5. Step 3: Sign a Manifest (v0.2)
     - JCS canonicalization
     - Ed25519 signing
     - Signature structure
     - Code examples
  6. Step 4: Verify a Manifest (v0.2)
     - Verification algorithm step-by-step
     - Error handling
     - Code examples
  7. Step 5: Run the Conformance Suite
     - How to get the suite
     - How to build an adapter
     - How to generate a report
  8. Common Pitfalls and FAQ
  9. Submitting Your Conformance Report
  ```

### Phase 2 — Decision tree for conformance levels

- [x] Create a visual decision tree (Excalidraw source + published SVG):
  - "Do you only consume manifests?" -> v0.1-baseline consumer
  - "Do you produce manifests?" -> v0.1-baseline issuer
  - "Do you need tamper protection?" -> v0.2-baseline
  - "Do you need revocation checking?" -> v0.2-extended
- [x] Include text-based fallback in the guide for non-visual consumption.

### Phase 3 — FAQ and common implementation questions

- [x] Compile and answer questions including:
  - "What JSON-LD processing do I need?" (Answer: none for basic conformance)
  - "Can I use a different signature algorithm?" (Answer: not for v0.2 conformance)
  - "How do I handle manifests with unknown fields?" (Answer: ignore them safely)
  - "What is the minimum manifest size I should support?" (Answer: up to 1 MB)
  - "How do I test my implementation?" (Answer: use the conformance suite from WO-0053)
  - "Can I extend the manifest with custom fields?" (Answer: yes, unknown fields are preserved)
  - "What about privacy/GDPR?" (Answer: use opaque IDs, minimal disclosure)
  - "How do I resolve a UMID?" (Answer: HTTP GET to myum.net/{UMID})
  - "What if the resolver is down?" (Answer: use cached manifest within TTL)

### Phase 4 — Quick-reference card

- [x] Single-page reference card (`docs/guides/QUICK-REFERENCE.md`):
  - Required fields table (field presenta, type, description).
  - Validation rules summary.
  - Signature verification algorithm in 5 numbered steps.
  - Conformance levels at a glance.
  - Key URLs (spec site, conformance suite, reference implementation).

### Phase 5 — Handoff format and agent-optimized packaging

- [x] Structure the guide with clear machine-readable sections:
  - Use consistent heading hierarchy.
  - Include structured metadata block at top (spec versions covered, last updated, suite version).
  - Mark normative vs. informative sections explicitly.
  - Include "copy-paste ready" code blocks with language tags.
- [x] Create a `docs/guides/AGENT-HANDOFF.md` that is a condensed, structured version optimized for agent-to-agent transfer:
  - Spec version, conformance levels, required fields, validation rules, signing algorithm.
  - All in a single document that can be included in an agent's context window.

### Phase 6 — Publish to docs site

- [x] Add implementation guide to the Starlight docs site navigation.
- [x] Add quick-reference card to the docs site.
- [x] Cross-link from existing getting-started and conformance pages.

## Key file paths (created/modified)

New files:
- `/Users/grig/work/repo/universalmanifest/docs/guides/IMPLEMENTATION-GUIDE.md`
- `/Users/grig/work/repo/universalmanifest/docs/guides/QUICK-REFERENCE.md`
- `/Users/grig/work/repo/universalmanifest/docs/guides/AGENT-HANDOFF.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/guides/implementation-guide.md` (Starlight page)
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/guides/quick-reference.md` (Starlight page)
- `/Users/grig/work/repo/universalmanifest/site/public/diagrams/conformance-decision-tree.svg`

Modified files:
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/` (cross-links)
- `/Users/grig/work/repo/universalmanifest/spec/v0.1/CONFORMANCE.md` (link to guide)
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md` (link to guide)

## Acceptance criteria

- [x] Implementation guide covers the complete path from "I have never seen UM" to "my implementation passes conformance."
- [x] Decision tree helps adopters choose the right conformance level in under 2 minutes.
- [x] Code examples are provided for at least TypeScript and one pseudocode language (Python or Go).
- [x] FAQ covers at least 8 common implementation questions with clear answers.
- [x] Quick-reference card fits on one printed page and includes all critical information.
- [x] Agent-handoff document can be consumed by an AI agent to produce a working implementation plan without additional context.
- [x] All documents are published to the docs site and cross-linked from existing navigation.
- [x] A test: give the agent-handoff document to a fresh AI agent and verify it can outline a correct implementation plan.

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean` (docs site builds with new pages)
- Manual review of implementation guide for completeness and accuracy.
- Agent-handoff test: provide `AGENT-HANDOFF.md` to a fresh agent session and evaluate the resulting plan.

## Dependencies and sequencing notes

- Depends on WO-0053 (conformance suite) for the "run conformance tests" section.
- Depends on WO-0054 (reference implementation) for code examples and as the primary "look at this for reference" link.
- WO-0057 (spec-vs-implementation clarity) should inform the guide's messaging about spec vs. implementation boundaries.
- WO-0058 (migration guide) is a companion document; the implementation guide should link to it for v0.1-to-v0.2 migration.

## Execution summary (2026-03-02)

Completed with deliverables:

- `/Users/grig/work/repo/universalmanifest/docs/guides/IMPLEMENTATION-GUIDE.md`
- `/Users/grig/work/repo/universalmanifest/docs/guides/QUICK-REFERENCE.md`
- `/Users/grig/work/repo/universalmanifest/docs/guides/AGENT-HANDOFF.md`
- `/Users/grig/work/repo/universalmanifest/docs/diagrams/conformance-decision-tree.excalidraw`
- `/Users/grig/work/repo/universalmanifest/site/public/diagrams/conformance-decision-tree.svg`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/guides/implementation-guide.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/guides/quick-reference.md`

Evidence:

- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/2026-03-02-wo-0055-execution-report.md`
- Agent Task ID preserved: `e0a7fe60_1772165606`
