# Animation QA Checklist

Use this checklist for every generated animated SVG before merge/deploy.

## A) Source fidelity

- [x] Narrative terms match UM docs and spec (`@id`, `subject`, TTL fields, claims, consents, pointers, shards).
- [x] No invented protocol behavior.
- [x] Normative vs non-normative boundaries are preserved.

## B) Visual clarity

- [x] Components are visually distinct.
- [x] Sequence is understandable without narration.
- [x] Text is readable on desktop and mobile.
- [x] Contrast is adequate (light text on #0f172a dark background).

## C) Motion quality

- [x] Motion supports explanation, not decoration.
- [x] Timing is deterministic and loop-safe.
- [x] No rapid flashing or distracting effects.
- [x] CSS animations only (no SMIL).

## D) Accessibility

- [x] `<title>` and `<desc>` are present on all SVGs.
- [x] `@media (prefers-reduced-motion: reduce)` fallback implemented on all SVGs.
- [x] Static understanding is still possible when motion is reduced.
- [x] `role="img"` and `aria-labelledby="title desc"` on all SVGs.

## E) Performance

- [x] File size is within budget for placement type (all under 50KB; largest ~16KB).
- [x] No heavy filter stack (only lightweight drop shadows).
- [x] Page load remains stable (no visible layout jumps).

## F) Integration quality

- [x] Asset paths under `/site/public/animations/` (and `/site/public/diagrams/` for overview).
- [x] Docs pages render correctly with and without animation support.
- [x] Build passes: `cd site && npm run build:clean`.

## G) Color system compliance

- [x] Background: #0f172a (dark)
- [x] Card: #1e293b
- [x] Accent/Primary: #3b82f6
- [x] Consent Allowed: #22c55e
- [x] Consent Denied: #ef4444
- [x] Consent Unset: #6b7280
- [x] Self-contained (no external dependencies)

## H) Asset inventory (WO-0042 + WO-0043)

### WO-0042 Phase 1 (core replacements + missing scenarios)

| Asset | Type | Status |
|-------|------|--------|
| `um-core-flow-pilot.svg` | Replaced pilot | PASS |
| `um-overlay-lanes-pilot.svg` | Replaced pilot | PASS |
| `universal-manifest-overview-template.svg` | Upgraded to animated | PASS |
| `scenario-01-object-model.svg` | New scenario | PASS |
| `scenario-03-consent-policy-flow.svg` | New scenario | PASS |
| `scenario-04-user-journey-sequence.svg` | New scenario | PASS |
| `scenario-06-motion-tutorial.svg` | New scenario | PASS |

### WO-0043 Phase 2 (tools + integration lanes)

| Asset | Type | Status |
|-------|------|--------|
| `scenario-07-workbench-explainer.svg` | Tool explainer (upgraded) | PASS |
| `scenario-08-harness-explainer.svg` | Tool explainer (upgraded) | PASS |
| `scenario-09-social-integration.svg` | Integration lane (new) | PASS |
| `scenario-10-pop-integration.svg` | Integration lane (upgraded) | PASS |
| `scenario-11-omatrust-integration.svg` | Integration lane (upgraded) | PASS |
| `scenario-12-rp1-integration.svg` | Integration lane (upgraded) | PASS |
| `scenario-13-smart-glasses-integration.svg` | Integration lane (upgraded) | PASS |
| `scenario-14-metaverse-integration.svg` | Integration lane (upgraded) | PASS |
| `scenario-15-chia-vc-integration.svg` | Integration lane (upgraded) | PASS |

## I) Review evidence

- [x] Build passes with 37 pages, 0 errors.
- [x] All SVGs verified for `<title>`, `<desc>`, and `prefers-reduced-motion`.
- [x] File sizes verified under budget.
