# Animated SVG Explainer Workflow

A standalone, portable guide for producing high-quality animated SVG explainers using a structured AI prompt-pack pipeline. This workflow was developed and proven on the Universal Manifest project (WO-0030), where it produced 29 production-quality animated SVGs that are currently live on universalmanifest.net (33 total including 2 test files and 2 pilot iterations). Any agent on any project can adapt this workflow.

For active/deprecated workflow status and asset lineage clarity, see:
`/Users/grig/work/repo/universalmanifest/docs/design/ANIMATION-WORKFLOW-AND-VERSION-STATUS.md`.

For replay/reproducibility operations, use only the canonical commands:

```bash
cd /Users/grig/work/repo/universalmanifest/site
npm run animation:replay:canonical -- --date YYYY-MM-DD
npm run animation:replay:verify -- --date YYYY-MM-DD
```

Do not run ad-hoc replay selection for canonical evidence.

---

## 1. Overview

### What this workflow produces

Self-contained animated SVG files that teach technical concepts through sequenced motion, readable labels, and consistent visual language. Each SVG is a single file with no external dependencies -- it can be dropped into any HTML page and works immediately.

### Why it works

The prompt-pack architecture separates concerns into three layers:

1. **System prompt** -- establishes visual style, color palette, technical constraints, and quality rules. Written once, reused across all animations.
2. **Scenario prompts** -- describe the specific story each animation tells, including required beats, labels, and timing. One per animation.
3. **Adaptation prompts** -- adjust output for different placements (homepage hero, inline section, full-page tutorial). Applied on top of a scenario prompt.

This layered approach ensures consistency across dozens of animations while allowing each one to tell a distinct story.

### Production track record

- 29 production SVGs generated and deployed across multiple work sessions
- All assets pass accessibility, performance, and visual clarity checks
- Total pipeline from concept to deployed asset: minutes per SVG, not hours
- Zero external dependencies in any output file

---

## 2. Design Principles

### Dark-theme technical aesthetic

All animations use a dark background (#0f172a) with light text and colored accents. This creates a premium, technical feel that works well on docs sites and avoids the "generic infographic" look.

### Motion explains, never decorates

Every moving element must teach something -- a sequence step, a causal relationship, a data flow direction. Purely decorative motion (spinning logos, floating particles, pulsing backgrounds) is prohibited.

### Cards and columns, not free-floating shapes

The layout uses card-based compositions with clear spatial grouping. Elements are organized in columns or rows with labeled sections. This produces clean, readable output that scales to mobile widths.

### Consistency over creativity

Every animation in a set should look like it belongs to the same family. The system prompt enforces this by locking down colors, fonts, spacing patterns, and animation techniques.

---

## 3. Color Palette

### Core palette (exact hex values)

| Token | Hex | Usage |
|-------|-----|-------|
| `--bg` | `#0f172a` | Full background fill |
| `--card` | `#1e293b` | Card/panel surfaces |
| `--border` | `#334155` | Card borders, dividers |
| `--ink` | `#f8fafc` | Primary text (headings, labels) |
| `--muted` | `#94a3b8` | Secondary text (descriptions, captions) |
| `--accent` | `#3b82f6` | Primary accent (links, highlights, step 1 elements) |
| `--accent-light` | `#60a5fa` | Lighter accent variant for field names |
| `--accent-bg` | `rgba(59,130,246,0.12)` | Accent background tint for pills/badges |
| `--green` | `#22c55e` | Success, allowed, consumption stage |
| `--green-bg` | `rgba(34,197,94,0.12)` | Green background tint |
| `--amber` | `#f59e0b` | Warning, validation, integrity checks |
| `--amber-bg` | `rgba(245,158,11,0.12)` | Amber background tint |
| `--violet` | `#8b5cf6` | Tertiary accent (external references, extensions) |
| `--violet-bg` | `rgba(139,92,246,0.12)` | Violet background tint |
| `--red` | `#ef4444` | Error, denied, blocked states |

### Semantic color usage

- **Blue accent** -- first stage, primary entities, navigation, identity fields
- **Amber** -- middle stage, validation, integrity, temporal bounds
- **Green** -- final stage, success, allowed consent, consumed data
- **Red** -- failure, denied consent, blocked paths
- **Violet** -- extension/external references, optional payload elements
- **Muted gray** -- descriptions, captions, secondary information

### Using CSS custom properties

Define colors as CSS custom properties in a `<style>` block inside `<defs>`. This makes the palette easy to adjust and keeps the SVG self-contained:

```xml
<defs>
  <style>
    :root {
      --bg: #0f172a;
      --card: #1e293b;
      --border: #334155;
      --ink: #f8fafc;
      --muted: #94a3b8;
      --accent: #3b82f6;
      --accent-light: #60a5fa;
      --accent-bg: rgba(59,130,246,0.12);
      --green: #22c55e;
      --green-bg: rgba(34,197,94,0.12);
      --amber: #f59e0b;
      --amber-bg: rgba(245,158,11,0.12);
    }
  </style>
</defs>
```

---

## 4. The Prompt Pack System

### Architecture

A prompt pack consists of three types of files:

```
prompts/animation/
  SYSTEM-PROMPT.md           # Style, constraints, quality rules
  SCENARIO-01-topic.md       # Story: what to animate
  SCENARIO-02-topic.md       # Story: what to animate
  ...
  ADAPTATION-HERO-SHORT.md   # Placement: homepage hero
  ADAPTATION-INLINE-MEDIUM.md  # Placement: docs section
  ADAPTATION-FULLPAGE-LOOP.md  # Placement: tutorial page
  README.md                  # Index and usage instructions
```

### System prompt structure

The system prompt must define:

1. **Output format** -- "You generate production-ready animated SVG files."
2. **Hard constraints** -- No JavaScript, no external dependencies, standalone SVG.
3. **Accessibility requirements** -- `<title>`, `<desc>`, reduced-motion fallback.
4. **Narrative quality rules** -- Explain causality, show sequence explicitly.
5. **Visual language** -- Color palette, card-based layout, responsive viewBox.
6. **Performance budget** -- File size targets per placement type.
7. **Domain terminology** -- Exact terms the animations must use.
8. **Source grounding check** -- Require the model to confirm it has read the source material.

### Scenario prompt structure

Each scenario prompt defines one animation story. Required sections:

1. **Title and purpose** -- What concept this animation teaches.
2. **Story objective** -- One sentence: what a viewer should understand after watching.
3. **Required beats** -- Numbered list of visual steps that must appear in order.
4. **Required labels/terminology** -- Exact text strings that must appear.
5. **Timing** -- Target loop duration (e.g., "16 to 22 second loop").
6. **Output constraints** -- Size limits, mobile readability notes.

Example scenario prompt:

```markdown
# Scenario: Authentication Flow Explainer

Generate a full-width animated SVG showing the authentication handshake.

## Story objective
Teach first-time readers how tokens are issued and validated.

## Required beats
1. Show client sending credentials to auth server.
2. Server validates and issues signed token.
3. Client presents token to resource server.
4. Resource server verifies signature and returns data.
5. Show failure branch for expired/invalid tokens.

## Required labels
- "Authenticate"
- "Issue Token"
- "Present"
- "Verify"
- "Reject / Retry"

## Timing
- 18 to 24 second loop.
```

### Adaptation prompt structure

Adaptation prompts modify a scenario's output for a specific placement context:

**Hero Short** (homepage):
- 10-14 second loop
- Minimal text (max 5 labels + 1 tagline)
- Prioritize readability at 320px width
- Under 160 KB

**Inline Medium** (documentation section):
- 14-20 second loop
- Include step numbers and compact legend
- Under 220 KB

**Full-Page Loop** (tutorial page):
- 24-36 second loop
- Include chapter markers (at least 4)
- Explicit restart marker and pause-safe end frame
- Under 320 KB

### Writing new prompts

When adding a new animation to the set:

1. Copy an existing scenario prompt as a template.
2. Replace the story objective, beats, and labels with your content.
3. Keep the timing and output constraints sections.
4. Ensure all required terminology matches your project's source-of-truth docs.
5. Test the prompt with the system prompt loaded first.

---

## 5. Production Pipeline

### Step-by-step process

#### Step 1: Define what to animate

Before writing any prompt, answer these questions:
- What concept does the viewer need to understand?
- What is the sequence or causal chain?
- What labels and terminology must appear?
- Where will this animation be placed (hero, inline, tutorial)?
- What source documents ground this content?

#### Step 2: Ground in source material

Read the relevant source documents for your project. The model generating the SVG must have access to accurate terminology, field names, and architectural relationships. Do not rely on the model's general knowledge -- feed it your specific docs.

#### Step 3: Load the system prompt

Provide the system prompt as context to the AI model before requesting any animation. The system prompt establishes all visual and technical constraints.

#### Step 4: Load the scenario prompt

Provide the specific scenario prompt that describes the animation story. If you need a new scenario, write one following the structure defined above.

#### Step 5: Apply an adaptation prompt (optional)

If the animation needs to fit a specific placement, apply the appropriate adaptation prompt on top of the scenario prompt.

#### Step 6: Generate the SVG

Request the AI model to generate the SVG. The output should be a complete, valid SVG file with all styles inline and no external dependencies.

#### Step 7: Run the QA checklist

Before accepting the output, verify against every item in the QA checklist (Section 9 below). Common failures that require regeneration:
- External font imports
- Missing `<title>` or `<desc>`
- Missing `prefers-reduced-motion` fallback
- Colors that do not match the palette
- File size over budget
- Text that is not readable at mobile widths

#### Step 8: Place in the repository

Save the SVG to your project's animations directory. Use a consistent naming scheme (e.g., `scenario-01-topic-name.svg`).

#### Step 9: Integrate into docs/site

Embed the SVG in the target page using an `<img>` tag or inline SVG. Verify the site builds cleanly after integration.

#### Step 10: Verify in browser

Open the page in a browser and confirm:
- Animation plays correctly and loops smoothly
- Text is readable on both desktop and mobile widths
- Reduced-motion fallback works (enable "prefers-reduced-motion: reduce" in browser dev tools)
- No layout shift when the SVG loads

---

## 6. Technical Constraints

### SVG requirements

- **Format**: Standalone valid SVG 1.1/2.0 markup
- **No JavaScript**: All animation via CSS `@keyframes` only
- **No SMIL**: Use CSS animations, not `<animate>` or `<animateTransform>` (SMIL is deprecated and inconsistently supported)
- **No external dependencies**: No `@import`, no linked fonts, no external stylesheets, no remote images
- **Self-contained styles**: All CSS in a `<style>` block inside `<defs>`
- **Explicit viewBox**: Always include `viewBox` attribute for responsive scaling
- **System fonts**: Use `font-family: system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, sans-serif`
- **Monospace fonts** (for code/field names): Use `font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace`

### Accessibility requirements

Every SVG must include:

```xml
<svg ... role="img" aria-labelledby="title desc">
  <title id="title">Short descriptive title</title>
  <desc id="desc">Longer description of what the animation shows and teaches.</desc>
  ...
</svg>
```

Every SVG must include a reduced-motion fallback:

```css
@media (prefers-reduced-motion: reduce) {
  .animated-element {
    animation: none !important;
    opacity: 1 !important;
    transform: none !important;
  }
  .flow-line {
    animation: none !important;
    stroke-dasharray: none;
  }
}
```

Additional accessibility rules:
- Text contrast ratio must be >= 4.5:1
- Visual order must match conceptual/reading order
- The SVG must be understandable as a static image when motion is disabled

### Performance budgets

| Placement type | Max file size | Max loop duration |
|----------------|---------------|-------------------|
| Hero (homepage) | 160 KB | 10-14 seconds |
| Inline (docs section) | 220 KB | 14-20 seconds |
| Full-page tutorial | 320 KB | 24-36 seconds |

Additional performance rules:
- Avoid expensive filter stacks (blur, complex compositing)
- Lightweight drop shadows via `<feDropShadow>` are acceptable
- Keep concurrent animation tracks minimal (3-5 simultaneous)
- No rapid flashing or high-frequency effects

### Cross-device behavior

- Must render clearly on desktop and mobile widths
- Must remain legible at 320px width and 2x pixel density
- Must not cause layout shift on page load
- Text must be readable without zooming on mobile

---

## 7. Animation Patterns

### Core techniques

All animations use CSS `@keyframes` defined in the `<style>` block. Here are the proven patterns:

#### Fade-up reveal (cards and sections)

```css
@keyframes fade-up {
  from { opacity: 0; transform: translateY(12px); }
  to { opacity: 1; transform: translateY(0); }
}

.stage { animation: fade-up 0.5s ease-out both; }
#stage-1 { animation-delay: 0.1s; }
#stage-2 { animation-delay: 0.35s; }
#stage-3 { animation-delay: 0.6s; }
```

Use for: revealing cards, columns, or sections in sequence. Stagger delays by 0.2-0.3s for readable pacing.

#### Slide-down reveal (layered structures)

```css
@keyframes slide-down {
  from { opacity: 0; transform: translateY(-8px); }
  to { opacity: 1; transform: translateY(0); }
}

.layer { animation: slide-down 0.5s ease-out both; }
#layer-header { animation-delay: 0.1s; }
#layer-integrity { animation-delay: 0.3s; }
#layer-payload { animation-delay: 0.5s; }
```

Use for: hierarchical structures where layers build from top to bottom.

#### Flow line (data movement between stages)

```css
@keyframes flow {
  from { stroke-dashoffset: 24; }
  to { stroke-dashoffset: 0; }
}

.flow-line {
  stroke-dasharray: 8 4;
  animation: flow 1s linear infinite;
}
```

Use for: showing data movement, connections between components, directional flow.

#### Pulse glow (active state indicators)

```css
@keyframes pulse-glow {
  0%, 100% { opacity: 0.5; }
  50% { opacity: 1; }
}

.glow-dot {
  animation: pulse-glow 2s ease-in-out infinite;
}
```

Use for: highlighting active endpoints, data transfer points, live indicators.

#### Simple fade-in (connectors and secondary elements)

```css
@keyframes fade-in {
  from { opacity: 0; }
  to { opacity: 1; }
}

.connectors { animation: fade-in 0.4s ease-out both; animation-delay: 0.8s; }
```

Use for: connector lines, legends, and secondary elements that should appear after main content.

### Timing guidelines

- Use `ease-out` for entrance animations (elements arriving)
- Use `linear` for continuous flow animations (data movement)
- Use `ease-in-out` for looping pulse/glow effects
- Stagger sequential reveals by 0.2-0.3 seconds
- Keep individual animation durations between 0.3s and 0.6s for reveals
- Use `both` for fill-mode on entrance animations (element stays visible after animation completes)

### SVG structural patterns

#### Card with accent bar

```xml
<g id="stage-1" class="stage">
  <rect x="50" y="80" width="265" height="260" class="card" filter="url(#card-shadow)" />
  <rect x="50" y="80" width="265" height="4" rx="2" fill="var(--accent)" />
  <!-- content inside -->
</g>
```

A thin colored bar at the top of each card visually codes the stage/category.

#### Icon circle with step number

```xml
<circle cx="182" cy="140" r="28" class="icon-resolve" />
<text x="182" y="147" class="step-num" fill="var(--accent-light)" text-anchor="middle">1</text>
```

Step numbers inside colored circles provide clear sequence markers.

#### Detail pills/badges

```xml
<rect x="100" y="274" width="70" height="22" rx="11" fill="var(--accent-bg)" />
<text x="135" y="289" font-size="11" font-weight="600" fill="var(--accent-light)" text-anchor="middle">@id</text>
```

Small rounded rectangles with monospace text for field names and technical labels.

#### Arrow markers for directional flow

```xml
<defs>
  <marker id="arr-accent" viewBox="0 0 10 10" refX="9" refY="5"
          markerWidth="6" markerHeight="6" orient="auto">
    <path d="M 0 1 L 8 5 L 0 9 z" fill="var(--accent)" />
  </marker>
</defs>

<line x1="315" y1="210" x2="400" y2="210"
      stroke="var(--accent)" stroke-width="1.5"
      class="flow-line" marker-end="url(#arr-accent)" />
```

#### Drop shadow filter

```xml
<filter id="card-shadow" x="-8%" y="-8%" width="116%" height="130%">
  <feDropShadow dx="0" dy="4" stdDeviation="8" flood-color="#000000" flood-opacity="0.3"/>
</filter>
```

Lightweight shadow that adds depth without heavy GPU cost.

---

## 8. Common Mistakes

These mistakes were discovered during the development of this pipeline. Each one produced SVGs that had to be archived and regenerated.

### External font imports (critical failure)

```css
/* DO NOT DO THIS */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
```

This breaks the self-contained requirement. The SVG will not render fonts correctly when served from a different domain, when offline, or in many SVG embedding contexts. Always use system font stacks.

### Wrong color palette

Early attempts used GitHub-inspired colors (`#0d1117`, `#58a6ff`, `#3fb950`) instead of the project palette (`#0f172a`, `#3b82f6`, `#22c55e`). While visually similar, this creates inconsistency across the animation set. Lock the palette in the system prompt and verify every output.

### SMIL animations instead of CSS

```xml
<!-- DO NOT DO THIS -->
<animate attributeName="opacity" from="0" to="1" dur="1s" />
```

SMIL is deprecated in several browsers and behaves inconsistently. Use CSS `@keyframes` exclusively.

### Missing reduced-motion fallback

Every animation must include `@media (prefers-reduced-motion: reduce)` that disables all motion. This is an accessibility requirement, not optional.

### Decorative-only motion

Spinning logos, floating particles, pulsing backgrounds, and other decorative motion add file size and distraction without teaching anything. If a moving element does not explain sequence or causality, remove it.

### Overly complex filter stacks

```xml
<!-- Avoid this pattern -->
<filter>
  <feGaussianBlur stdDeviation="20"/>
  <feComposite operator="over"/>
  <feBlend mode="screen"/>
</filter>
```

Heavy filter stacks increase GPU cost and can cause jank on mobile devices. A simple `<feDropShadow>` is sufficient for depth.

### Text too small for mobile

All text must be readable at 320px viewport width. Use minimum 11px for labels and 13px for descriptions. Test by resizing the browser window.

### Excalidraw export as production asset

Excalidraw-exported SVGs have different styling, lack the dark theme consistency, miss accessibility metadata, and do not include CSS animations or reduced-motion fallbacks. Excalidraw is useful for whiteboarding and exploration, but its exports are not production-ready for this pipeline. Convert concepts developed in Excalidraw into prompt-pack-generated SVGs for production use.

### Invented terminology or protocol behavior

The AI model will sometimes invent plausible-sounding but incorrect technical terms or protocol behavior. Every label in the output must be verified against the project's source-of-truth documents.

---

## 9. QA Checklist

Run this checklist for every generated animated SVG before accepting it.

### A) Source fidelity

- [ ] All technical terms match the project's source-of-truth documents.
- [ ] No invented protocol behavior or architecture that does not exist in the source.
- [ ] Normative vs non-normative boundaries are preserved (if applicable).

### B) Visual clarity

- [ ] Components are visually distinct from each other.
- [ ] Sequence is understandable without external narration.
- [ ] Text is readable on both desktop and mobile widths.
- [ ] Contrast is adequate (light text on dark background).

### C) Motion quality

- [ ] Every moving element supports explanation, not decoration.
- [ ] Timing is deterministic and loop-safe (smooth restart).
- [ ] No rapid flashing or distracting effects.
- [ ] CSS animations only (no SMIL `<animate>` elements).

### D) Accessibility

- [ ] `<title>` element is present with a descriptive short title.
- [ ] `<desc>` element is present with a longer description of what the animation teaches.
- [ ] `role="img"` and `aria-labelledby="title desc"` are on the root `<svg>` element.
- [ ] `@media (prefers-reduced-motion: reduce)` fallback disables all motion.
- [ ] Static understanding is still possible when motion is disabled.

### E) Performance

- [ ] File size is within budget for the placement type.
- [ ] No heavy filter stack (only lightweight drop shadows allowed).
- [ ] Page load remains stable (no visible layout jumps).
- [ ] SVG renders correctly when embedded via `<img>` tag.

### F) Self-containment

- [ ] No external font imports (`@import url(...)` is prohibited).
- [ ] No JavaScript.
- [ ] No external stylesheets or images.
- [ ] All styles are in a `<style>` block inside `<defs>`.
- [ ] SVG is valid standalone markup.

### G) Color system compliance

- [ ] Background: `#0f172a`
- [ ] Card surfaces: `#1e293b`
- [ ] Primary accent: `#3b82f6`
- [ ] Colors defined as CSS custom properties in `:root`.
- [ ] Color usage is semantically consistent with the palette rules.

### H) Integration

- [ ] SVG renders correctly in the target page.
- [ ] Site/project build passes after integration.
- [ ] No regression in other pages.

---

## 10. Reference Implementations

These SVGs from the Universal Manifest project serve as exemplars of the pipeline's output quality. Study their structure, style, and animation patterns when calibrating your own prompt pack.

### Core flow pipeline (3-stage linear flow)

**File:** `site/public/animations/um-core-flow-pilot.svg`

Demonstrates: card-based 3-column layout, flow lines with arrow markers, staggered fade-up reveals, pulse glow dots, accent-colored stage bars, detail pills, step-number circles.

### Object model structure (layered hierarchy)

**File:** `site/public/animations/scenario-01-object-model.svg`

Demonstrates: layered card layout (header/integrity/payload), slide-down reveals, dashed envelope boundary, field-name badges with monospace text, dependency connectors.

### Integration lane explainer (data flow with consent gating)

**File:** `site/public/animations/scenario-09-social-integration.svg`

Demonstrates: 3-column layout with source/gate/projection pattern, consent status indicators (green allowed, red denied), flow lines between columns, compact monospace field labels.

---

## 11. Adapting for Other Projects

This workflow is not specific to Universal Manifest. Any project that needs animated SVG explainers can use the same pipeline with these adjustments:

### Step 1: Define your color palette

Replace the UM color values with your project's brand colors. Keep the same semantic structure (background, card, border, ink, muted, accent, success, warning, error). Define them as CSS custom properties.

### Step 2: Write your system prompt

Copy the system prompt structure and replace:
- Domain terminology with your project's terminology
- Source grounding references with your project's source-of-truth documents
- Performance budgets if your targets differ

Keep the hard constraints (no JS, no external deps, accessibility requirements, CSS-only animation).

### Step 3: Write scenario prompts for your content

Follow the scenario prompt structure (story objective, required beats, required labels, timing). Write one prompt per animation you need.

### Step 4: Choose your adaptation prompts

The three adaptation prompts (hero, inline, full-page) work for most docs sites. Adjust timing and size budgets if needed.

### Step 5: Generate and QA

Follow the production pipeline steps. Use the QA checklist with your project's color values substituted.

### What to keep unchanged across projects

These elements are universal and should not be modified:
- System font stacks (no external font imports)
- Accessibility requirements (`<title>`, `<desc>`, `role="img"`, reduced-motion)
- CSS-only animation constraint (no JS, no SMIL)
- Card-based layout approach
- Self-contained SVG requirement
- The QA checklist structure

### What to customize per project

These elements should be adapted:
- Color palette hex values
- Domain terminology
- Source grounding corpus
- Specific scenario stories
- Performance budgets (if your project has different constraints)
- Naming conventions for output files

---

## 12. File Reference (Universal Manifest Project)

### Prompt pack

- System prompt: `.dev/ai/prompts/animation/SYSTEM-PROMPT-UM-ANIMATION.md`
- Scenario prompts: `.dev/ai/prompts/animation/SCENARIO-*.md`
- Adaptation prompts: `.dev/ai/prompts/animation/ADAPTATION-*.md`
- Prompt pack index: `.dev/ai/prompts/animation/README.md`

### Design documents

- Technical spec: `docs/design/ANIMATED-SVG-SPEC.md`
- QA checklist: `docs/design/ANIMATION-QA-CHECKLIST.md`
- Placement plan: `docs/design/ANIMATION-PLACEMENT-PLAN.md`
- This workflow: `docs/design/ANIMATED-SVG-WORKFLOW.md`

### Work orders

- WO-0030 (pipeline creation): `docs/workorders/WO-0030-animated-svg-explainer-prompt-pack-and-production-pipeline.md`
- WO-0042 (phase 1 execution): `docs/workorders/WO-0042-animation-upgrade-phase-1-core-replacements-and-missing-scenarios.md`
- WO-0043 (phase 2 execution): `docs/workorders/WO-0043-animation-upgrade-phase-2-tools-and-integration-lane-explainers.md`

### Output assets

- Production animations: `site/public/animations/`
- Overview diagram: `site/public/diagrams/universal-manifest-overview-template.svg`
- Archived early attempts: `site/public/animations/archive_bad_svgs/`

### Production asset inventory (29 production SVGs; 33 total)

| File | Type | Description |
|------|------|-------------|
| `um-core-flow-pilot.svg` | Core | Resolve/validate/consume pipeline |
| `um-overlay-lanes-pilot.svg` | Core | Overlay lanes anchored to core envelope |
| `scenario-01-object-model.svg` | Scenario | Manifest structure breakdown |
| `scenario-03-consent-policy-flow.svg` | Scenario | Consent toggle gating flow |
| `scenario-04-user-journey-sequence.svg` | Scenario | End-to-end issuer-to-consumer flow |
| `scenario-06-motion-tutorial.svg` | Scenario | Visual objects and icons tutorial |
| `scenario-07-workbench-explainer.svg` | Tool | Editor lifecycle (import/edit/validate/export) |
| `scenario-08-harness-explainer.svg` | Tool | Fixture load/quick checks/resolver probe |
| `scenario-09-social-integration.svg` | Integration | Social/profile projection via publicProfile shard |
| `scenario-10-pop-integration.svg` | Integration | Proof-of-personhood multi-provider flow |
| `scenario-11-omatrust-integration.svg` | Integration | OMATrust attestation interoperability |
| `scenario-12-rp1-integration.svg` | Integration | RP1 spatial fabric binding |
| `scenario-13-smart-glasses-integration.svg` | Integration | Smart glasses AR social layer |
| `scenario-14-metaverse-integration.svg` | Integration | Metaverse identity and lineage |
| `scenario-15-chia-vc-integration.svg` | Integration | Chia DID/VC credential bridge |
| `universal-manifest-overview-template.svg` | Diagram | Complete system architecture (in `diagrams/`) |
