# Animation QA Checklist

Use this checklist for every generated animated SVG before merge/deploy.

## A) Source fidelity

- [ ] Narrative terms match UM docs and spec (`@id`, `subject`, TTL fields, claims, consents, pointers, shards).
- [ ] No invented protocol behavior.
- [ ] Normative vs non-normative boundaries are preserved.

## B) Visual clarity

- [ ] Components are visually distinct.
- [ ] Sequence is understandable without narration.
- [ ] Text is readable on desktop and mobile.
- [ ] Contrast is adequate.

## C) Motion quality

- [ ] Motion supports explanation, not decoration.
- [ ] Timing is deterministic and loop-safe.
- [ ] No rapid flashing or distracting effects.

## D) Accessibility

- [ ] `<title>` and `<desc>` are present.
- [ ] Reduced-motion fallback is implemented.
- [ ] Static understanding is still possible when motion is reduced.

## E) Performance

- [ ] File size is within budget for placement type.
- [ ] No heavy filter stack.
- [ ] Page load remains stable (no visible layout jumps).

## F) Integration quality

- [ ] Asset path is under `/site/public/animations/`.
- [ ] Docs page renders correctly with and without animation support.
- [ ] Build passes: `cd /Users/grig/work/repo/universalmanifest/site && npm run build`.

## G) Review evidence

- [ ] Capture screenshot/video of rendered animation.
- [ ] Record reviewer notes and decision in a dated report.

