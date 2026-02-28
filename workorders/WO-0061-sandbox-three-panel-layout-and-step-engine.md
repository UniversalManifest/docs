# WO-0061 -- Sandbox Three-Panel Layout and Step Engine

**Status:** NOT_STARTED
**Created:** 2026-02-27
**Priority:** HIGHEST
**Blocks:** WO-0062, WO-0063, WO-0064, WO-0065, WO-0066, WO-0067
**Dependencies:** WO-0060 (browser validator and page scaffolds)
**Estimated effort:** 1 week
**Mandate:** [MANDATE-interactive-implementation-sandbox.md](/docs/MANDATE-interactive-implementation-sandbox.md)
**Proposal:** [PROPOSAL-interactive-implementation-sandbox.md](/.dev/ai/proposals/PROPOSAL-interactive-implementation-sandbox.md)

## Objective

Build the three-panel layout shell, the step-through engine, and the step control UI. This is the interactive framework that all scenarios plug into.

## Why this work matters

The three-panel layout and step-through mechanism are the core UX of the sandbox. Without them, scenarios have no way to be displayed or interacted with. This work order creates the reusable shell that every scenario renders inside.

## Scope

In scope:
- Three-panel CSS Grid layout (entity | consumer | protocol) with responsive breakpoints
- Step engine (`SandboxEngine` class) with state management, step transitions, and event system
- Step controller UI (prev/next/play/reset buttons, step indicator dots)
- Step bubble/annotation component with highlight system
- Manifest viewer component with JSON syntax highlighting
- Manifest editor component (textarea with validation feedback)
- Panel header components with icons and status indicators
- CSS custom properties for theming and category-specific colors
- Keyboard navigation (arrow keys for step, escape for modal)

Out of scope:
- Scenario modal (WO-0062)
- Individual scenario definitions (WO-0063 through WO-0066)
- Illustration SVGs (WO-0067)

## Execution phases

### Phase 1 -- Three-panel layout

- [ ] Create `site/src/components/sandbox/SandboxLayout.astro`:
  - CSS Grid with 3 columns (30% / 35% / 35%)
  - Responsive: tablet stacks consumer + protocol vertically; mobile uses tabs
  - Sticky header with scenario title, back button, and action buttons
  - Bottom control bar for step navigation
- [ ] Create `site/src/styles/sandbox/layout.css`:
  - Grid template with named areas
  - Breakpoints at 1200px and 768px
  - CSS custom properties for panel widths, gaps, and colors
- [ ] Create `site/src/styles/sandbox/panels.css`:
  - Panel card styles with rounded corners, subtle shadows
  - Panel headers with colored accent bars
  - Scrollable panel content areas

### Phase 2 -- Step engine

- [ ] Create `site/src/scripts/sandbox/engine.ts`:
  - `SandboxEngine` class with `SandboxState` management
  - `goToStep(n)` method that updates all three panels
  - `nextStep()` and `prevStep()` methods
  - `play()` auto-advance mode with configurable speed
  - `reset()` to restore original manifest and step position
  - `updateManifest(json)` for when the user edits the JSON
  - Event listener system for UI components to react to state changes
  - Step action execution with error handling (validation calls)
  - `StepResult` tracking per step (`idle | running | passed | failed | blocked`)
- [ ] Create `site/src/scripts/sandbox/highlight.ts`:
  - Minimal JSON syntax highlighting (strings, numbers, booleans, keys, brackets)
  - JSON path-based highlight overlay (highlight specific fields within rendered JSON)

### Phase 3 -- Panel components

- [ ] Create `site/src/components/sandbox/EntityPanel.astro`:
  - Displays entity summary (avatar, name, DID, version badge)
  - Displays manifest JSON (viewer mode or editor mode)
  - Highlight overlays on specific JSON paths per step
  - "Edit JSON" toggle button
- [ ] Create `site/src/components/sandbox/ConsumerPanel.astro`:
  - Displays consumer identity (icon, name, type)
  - Status area (receiving, processing, verified, rejected)
  - Progress bar
  - Consumer-specific rendering area (profile card, consent matrix, etc.)
- [ ] Create `site/src/components/sandbox/ProtocolPanel.astro`:
  - Step title and progress indicator
  - Validation check list (checklist with pass/fail/pending icons)
  - Code snippet area (for showing canonical JSON, signing input, etc.)
  - Bubble attachment point

### Phase 4 -- Step controls and bubbles

- [ ] Create `site/src/components/sandbox/StepController.astro`:
  - Prev/Next buttons with arrow icons
  - Play/Pause toggle button
  - Reset button
  - Step counter text ("Step 3 of 7")
  - Timeline dots (filled for completed, highlighted for current, empty for future)
- [ ] Create `site/src/components/sandbox/StepBubble.astro`:
  - Positioned relative to its target panel
  - Contains markdown-rendered explanation text
  - Has a pointer arrow toward the highlighted element
  - Animates in/out with 200ms fade + slide
- [ ] Create `site/src/components/sandbox/StepTimeline.astro`:
  - Horizontal dot timeline below the step counter
  - Clickable dots for direct navigation to any step
  - Color-coded: green (passed), red (failed), gray (future), blue (current)
- [ ] Create `site/src/styles/sandbox/steps.css` and `site/src/styles/sandbox/bubbles.css`

### Phase 5 -- Manifest viewer/editor

- [ ] Create `site/src/components/sandbox/ManifestViewer.astro`:
  - Read-only JSON display with syntax highlighting
  - Line numbers
  - JSON path-based highlight overlays (colored outlines around specified paths)
  - Collapsible sections for shards, claims, consents, etc.
- [ ] Create `site/src/components/sandbox/ManifestEditor.astro`:
  - Textarea with JSON syntax highlighting
  - Real-time JSON parsing feedback (valid/invalid indicator)
  - "Run with changes" button
  - "Revert" button
- [ ] Create `site/src/styles/sandbox/editor.css` and `site/src/styles/sandbox/highlight.css`

### Phase 6 -- Integration test with a dummy scenario

- [ ] Create a minimal test scenario that uses the layout, engine, and all components
- [ ] Verify: step navigation works (prev/next/direct click)
- [ ] Verify: play mode auto-advances
- [ ] Verify: edit mode allows JSON modification and re-runs validation
- [ ] Verify: responsive layout works at all breakpoints
- [ ] Verify: keyboard navigation (left/right arrows, escape)

## Key file paths (created)

- `/Users/grig/work/repo/universalmanifest/site/src/components/sandbox/SandboxLayout.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/components/sandbox/EntityPanel.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/components/sandbox/ConsumerPanel.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/components/sandbox/ProtocolPanel.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/components/sandbox/StepController.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/components/sandbox/StepBubble.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/components/sandbox/StepTimeline.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/components/sandbox/ManifestViewer.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/components/sandbox/ManifestEditor.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/engine.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/highlight.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/styles/sandbox/layout.css`
- `/Users/grig/work/repo/universalmanifest/site/src/styles/sandbox/panels.css`
- `/Users/grig/work/repo/universalmanifest/site/src/styles/sandbox/steps.css`
- `/Users/grig/work/repo/universalmanifest/site/src/styles/sandbox/bubbles.css`
- `/Users/grig/work/repo/universalmanifest/site/src/styles/sandbox/editor.css`
- `/Users/grig/work/repo/universalmanifest/site/src/styles/sandbox/highlight.css`

## Acceptance criteria

- [ ] Three-panel layout renders correctly at desktop (>1200px), tablet (768-1200px), and mobile (<768px)
- [ ] Step engine correctly advances through steps, tracks results, and updates panels
- [ ] Play mode auto-advances with a visible pause between steps
- [ ] Reset restores original manifest and returns to step 1
- [ ] JSON editor allows modification and "Run" re-executes from step 1
- [ ] Bubbles appear attached to the correct panel with explanation text
- [ ] Timeline dots are clickable and navigate to the selected step
- [ ] Keyboard navigation works (arrow keys, escape)
- [ ] A dummy scenario renders and is interactive end-to-end
- [ ] `npm run build:clean` succeeds

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
- `cd /Users/grig/work/repo/universalmanifest/site && npm run dev` (test at /sandbox/test/)
- Manual responsive testing at multiple viewport widths
