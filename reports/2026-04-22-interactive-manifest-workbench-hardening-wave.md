# 2026-04-22 Interactive Manifest Workbench Hardening Wave

## Purpose

This report closes `WO-0193` by recording a bounded but real hardening slice for the interactive manifest workbench.

The chosen slice targeted the highest-value post-first-release safety gap: silent loss or misuse of unapplied edits in the guided editor and raw JSON editor.

## Hardened Gap

Before this slice:

- guided-form edits and raw JSON edits could be overwritten by template/load/reset actions without enough warning
- validate/copy/download/round-trip actions could run against the last applied manifest while the editor still contained unsaved changes
- workbench logic lived in a single large browser script, which made testing and maintenance harder than it needed to be

## What Changed

Updated or added:

- `site/public/workbench/workbench.js`
- `site/public/workbench/workbench-core.js`
- `site/public/workbench/app/index.html`
- `site/tests/workbench-core.test.js`
- `site/package.json`

The hardening slice introduced:

- extracted pure workbench core logic for validation, draft-state comparison, snapshot persistence, and optional-section trimming
- local draft autosave/restore using browser storage
- unsaved-change tracking across both the guided editor and raw JSON editor
- `beforeunload` protection
- explicit confirm guards before destructive actions
- explicit confirm guards before validate/copy/download/round-trip actions when unapplied edits exist
- visible draft-status messaging in the UI
- node-based automated tests for the extracted core module

## Verification

Executed during closeout:

- `npm --prefix /Users/grig/work/repo/universalmanifest/site run test:workbench`
  - Result: passed (`6/6`)
- `npm --prefix /Users/grig/work/repo/universalmanifest/site run build`
  - Result: passed
  - Residual warnings were the existing route-priority warnings for the Starlight catch-all route and were unrelated to this lane
- Browser sanity check against the built workbench at `http://127.0.0.1:4327/workbench/app/`
  - After editing `subject`, the UI reported: `Unsaved edits in guided editor. Autosaved locally ...`
  - Attempting `Clear` with unsaved edits triggered the confirm warning and preserved the edited value when canceled.
  - Attempting `Copy JSON` with unsaved edits triggered the expected warning that copy uses the last applied manifest only.

## Outcome

`WO-0193` is now complete.

The workbench is more reliable and maintainable because:

- users are warned before losing unapplied edits
- workbench actions no longer silently operate on stale applied state
- the core editing/validation logic is testable in isolation
- verification evidence exists for the new safety layer
