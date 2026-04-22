# 2026-04-22 Static Tool Surface Shell Alignment Closeout

## Purpose

This report closes the docs-side slice of `WO-0184`.

The paired implementation slice was already verified on a clean branch. This closeout captures the resulting route coverage, the preserved raw-payload boundaries, and the updated project-status posture after the shell-alignment pass.

## What changed

### 1. The remaining static tool-adjacent routes now share a deliberate shell strategy

`WO-0184` closed the outstanding route-level shell/framing gap for:

- `/404.html`
- `/proof/harness/`
- `/resolver/`
- `/resolver/ops/`
- `/resolver/result/`
- `/tools/concept-explorer/`

Those surfaces no longer present as isolated sprint-era fragments. They now sit within the same route-level alignment model used by the broader post-`WO-0177` public/tool-shell family.

### 2. Raw payloads were preserved instead of rewritten away

The implementation did not collapse the underlying static payloads into a single rewritten application.

Instead, the alignment keeps the higher-level public entry routes deliberate while preserving subordinate payload access where needed, including:

- `/resolver/app/`
- `/tools/concept-explorer/app/`

That preserves the static tool payload boundary while reducing route-level fragmentation.

### 3. The site-architecture queue narrowed cleanly

With `WO-0184` complete, the remaining active site-architecture lanes are now:

- `WO-0185` latest spec surface strategy and shell implementation
- `WO-0187` animation and diagram asset naming normalization

`WO-0188` remains the convergence lane that follows those remaining site-architecture outputs.

## Verification

Implementation evidence reviewed for this closeout:

- clean-branch implementation verification recorded for `WO-0184`
- `npm run build` passed in `site/`
- browser verification was clean for:
  - `/404.html`
  - `/proof/harness/`
  - `/resolver/`
  - `/tools/concept-explorer/`
- the concept explorer raw payload path issue was fixed so the app fetches its JSON from the correct subordinate location before the browser verification rerun

Docs-side verification completed for this closeout:

- status-layer coherence was checked across `docs/workorders/WO-0184-static-tool-surface-shell-alignment.md`, `docs/workorders/WO-INDEX.md`, `docs/CRITICAL-PATH.md`, and `docs/STATE-OF-THE-PROJECT.md`
- the closeout report path was added to the work-order index entry for `WO-0184`
- the remaining active site-architecture batch now reads consistently as `WO-0185` plus `WO-0187`, with `WO-0188` still waiting on those outputs

## Outcome

The static tool-surface shell-alignment lane is complete. The public/tool-shell model now extends across the remaining resolver, proof, concept-explorer, and 404 entry surfaces that were still structurally disconnected after the earlier reintegration waves, without removing the subordinate raw payloads those surfaces still depend on.
