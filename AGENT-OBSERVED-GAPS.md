# Agent-Observed Gaps (Append-only)

### 2026-02-11

**Observation:** reference implementation handoff references `.dev/ai/proposals/2026-02-11-universal-manifest-extraction.md`, but that file does not exist in the runtime repo.  
**Impact:** Medium  
**Category:** Missing Doc  
**Status:** Open

### 2026-02-11

**Observation:** reference implementation handoff mentions migrating `legacy-deep-dive-*.md` files, but the current reference implementation design library uses consolidated `legacy-*.md` filenames (no `legacy-deep-dive-*` present).  
**Impact:** Low  
**Category:** Inconsistency  
**Status:** Open

### 2026-03-16

**Observation:** `cd /Users/grig/work/repo/universalmanifest/site && npm run build` still emits unresolved Starlight `glob-loader` duplicate-id warnings on changed docs pages (`for-agents/external-agent-onboarding`, `about/agent-briefing`, `publishing/domain-split`) even though the source tree does not show obvious duplicate markdown files and the routes still build and serve correctly.  
**Impact:** Medium  
**Category:** Inconsistency  
**Status:** Open

### 2026-03-17

**Observation:** Resolution for the 2026-03-16 duplicate-id warning investigation: the affected site build is now clean of the Starlight `glob-loader` duplicate-id warning after updating `site/src/content.config.ts` to use Starlight `docsLoader()`. The issue was a content-loader upgrade gap, not a duplicate markdown-file collision.  
**Impact:** Medium  
**Category:** Inconsistency  
**Status:** Resolved

### 2026-03-17

**Observation:** After the `WO-0162` cleanup, the site build still emits three known non-blocking warnings: the sandbox scenario mixed static/dynamic import warning, the intentional Starlight `/` route-priority warning, and the Pagefind `/workbench/index/` no-outer-`<html>` warning. These no longer indicate a broken build, but they remain undocumented build-noise debt until each warning is fixed or explicitly accepted.  
**Impact:** Low  
**Category:** Quality Debt  
**Status:** Open

### 2026-03-17

**Observation:** Resolution for the remaining post-`WO-0162` site build warnings: the sandbox mixed-import warning and the Pagefind `/workbench/index/` warning are now removed, and the only remaining warning is the intentional Starlight `/` route-priority override created by the landing-first root page. This warning is now documented as an accepted condition rather than untracked build-noise debt.  
**Impact:** Low  
**Category:** Quality Debt  
**Status:** Resolved

### 2026-03-19

**Observation:** The remaining Starlight root-route warning is now gone. The old docs-root content was relocated from `/` to `/docs/overview/`, preserving the long-form overview while leaving the landing-first root page as the sole owner of `/`. `npm run build` in `/Users/grig/work/repo/universalmanifest/site` is now warning-free.  
**Impact:** Low  
**Category:** Quality Debt  
**Status:** Resolved
