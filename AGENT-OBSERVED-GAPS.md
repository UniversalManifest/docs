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
