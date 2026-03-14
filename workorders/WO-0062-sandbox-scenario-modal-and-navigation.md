# WO-0062 -- Sandbox Scenario Modal and Navigation

**Status:** COMPLETED
**Created:** 2026-02-27
**Priority:** HIGHEST
**Blocks:** WO-0063, WO-0064, WO-0065, WO-0066
**Dependencies:** WO-0061 (three-panel layout and step engine)
**Estimated effort:** 3-4 days
**Mandate:** [MANDATE-interactive-implementation-sandbox.md](/docs/MANDATE-interactive-implementation-sandbox.md)
**Proposal:** [PROPOSAL-interactive-implementation-sandbox.md](/.dev/ai/proposals/PROPOSAL-interactive-implementation-sandbox.md)

## Objective

Build the scenario selection modal (card grid), the search/filter system, and the navigation between scenario selection and sandbox step-through mode. This is the front door to the sandbox -- the first thing users see.

## Why this work matters

The mandate says: "Beautiful cards showing an image representing the scenario, a description of what that example of Universal Manifest is, and how it would work in the real world." The modal is the entry experience. It must be visually appealing, fast to browse, and easy to filter when the scenario list is long.

## Scope

In scope:
- Scenario modal overlay (full-screen on mobile, centered overlay on desktop)
- Card grid layout (3 columns desktop, 2 tablet, 1 mobile)
- Card component (illustration, title, description, step count, version badge)
- Category headers with horizontal separators
- Search input with real-time text filtering
- Category dropdown filter
- Spec version dropdown filter
- "Show more" expandable sections for categories with many scenarios
- Navigation: card click -> close modal -> load scenario in sandbox layout
- Back button: return to modal from sandbox
- URL routing: `/sandbox/` = modal, `/sandbox/{scenario-id}/` = sandbox with specific scenario
- Keyboard navigation: arrow keys between cards, Enter to select, Escape to close

Out of scope:
- Actual scenario definitions (WO-0063 through WO-0066)
- SVG illustrations (WO-0067; cards will use placeholder images until then)

## Execution phases

### Phase 1 -- Scenario card component

- [ ] Create `site/src/components/sandbox/ScenarioCard.astro`:
  - Illustration area (SVG or placeholder colored rectangle)
  - Title (bold, 1 line)
  - Description (2 lines, ellipsis overflow)
  - Footer: step count badge, version badge (v0.1 blue, v0.2 green)
  - Hover state: subtle lift shadow and border highlight
  - Focus state: visible outline for keyboard navigation
  - Click handler: navigates to scenario URL

### Phase 2 -- Scenario modal

- [ ] Create `site/src/components/sandbox/ScenarioModal.astro`:
  - Full-screen overlay with semi-transparent backdrop
  - Modal container with max-width (1200px), padding, and scroll
  - Header: title ("Choose a Scenario"), close button
  - Search bar with text input and filter dropdowns
  - Category sections with headers and card grids
  - "Show more" toggle for categories with >3 scenarios (collapsed by default for Integration Lanes, Edge Cases + Advanced)
  - Close on Escape key, close on backdrop click
- [ ] Create `site/src/styles/sandbox/modal.css`:
  - Overlay backdrop (rgba dark)
  - Modal container (white, rounded, shadowed)
  - Card grid (CSS Grid, responsive)
  - Search bar styles
  - Category header styles (horizontal rule + label)

### Phase 3 -- Search and filter

- [ ] Implement text search:
  - Filters cards by title and description text (case-insensitive)
  - Debounced (300ms) to avoid jank during typing
  - Shows "No results" message when no matches
- [ ] Implement category filter dropdown:
  - Options: All, Getting Started, Trust & Verification, Integration Lanes, Edge Cases, Advanced
  - Selecting a category scrolls to that section (if text search is empty) or filters cards
- [ ] Implement version filter dropdown:
  - Options: All, v0.1, v0.2
  - Filters cards by spec version

### Phase 4 -- Navigation integration

- [ ] `/sandbox/` (index.astro): renders the modal as the full page (not an overlay; it IS the page)
- [ ] `/sandbox/{scenario-id}/` (dynamic route): renders the three-panel sandbox
  - Loads scenario definition from the registry
  - "Back to Scenarios" button returns to `/sandbox/`
- [ ] URL updates on scenario selection (no full page reload -- use `history.pushState` for SPA-like navigation where possible, with fallback to standard navigation)
- [ ] Browser back button returns to modal

### Phase 5 -- Scenario registry integration

- [ ] Update `site/src/scripts/sandbox/scenarios/index.ts`:
  - Define the `ScenarioRegistry` that provides scenario metadata (title, description, category, version, illustration path) without loading the full step definitions
  - Support lazy loading: full scenario definition loaded only when the user selects a scenario
- [ ] Create placeholder scenarios (at least 3) in the registry for testing the modal, even before real scenario definitions exist

## Key file paths (created)

- `site/src/components/sandbox/ScenarioModal.astro`
- `site/src/components/sandbox/ScenarioCard.astro`
- `site/src/styles/sandbox/modal.css`
- Updated: `site/src/pages/sandbox/index.astro`
- Updated: `site/src/pages/sandbox/[...scenario].astro`
- Updated: `site/src/scripts/sandbox/scenarios/index.ts`

## Acceptance criteria

- [ ] Modal renders at `/sandbox/` with category sections and card grid
- [ ] Cards display illustration placeholder, title, description, step count, version badge
- [ ] Search filters cards in real-time by title and description
- [ ] Category dropdown filters cards to selected category
- [ ] Version dropdown filters cards to selected version
- [ ] Clicking a card navigates to `/sandbox/{scenario-id}/` and loads the sandbox layout
- [ ] "Back to Scenarios" button in the sandbox returns to the modal
- [ ] Browser back button works correctly between modal and sandbox
- [ ] Keyboard: arrow keys navigate cards, Enter selects, Escape closes/goes back
- [ ] Responsive: 3 columns desktop, 2 tablet, 1 mobile
- [ ] "Show more" works for collapsed category sections
- [ ] `npm run build:clean` succeeds
- [ ] At least 3 placeholder scenarios appear in the modal for testing

## Validation commands

- `cd site && npm run build:clean`
- `cd site && npm run dev` (test at /sandbox/)
- Manual testing: search, filter, card click, back navigation, keyboard navigation
