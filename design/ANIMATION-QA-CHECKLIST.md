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
- [x] Contrast is adequate.

## C) Motion quality

- [x] Motion supports explanation, not decoration.
- [x] Timing is deterministic and loop-safe.
- [x] No rapid flashing or distracting effects.

## D) Accessibility

- [x] `<title>` and `<desc>` are present.
- [x] Reduced-motion fallback is implemented.
- [x] Static understanding is still possible when motion is reduced.

## E) Performance

- [x] File size is within budget for placement type.
- [x] No heavy filter stack.
- [x] Page load remains stable (no visible layout jumps).

## F) Integration quality

- [x] Asset path is under `/site/public/animations/`.
- [x] Docs page renders correctly with and without animation support.
- [x] Build passes: `cd /Users/grig/work/repo/universalmanifest/site && npm run build`.

## G) Review evidence

- [ ] Capture screenshot/video of rendered animation.
- [ ] Record reviewer notes and decision in a dated report.

