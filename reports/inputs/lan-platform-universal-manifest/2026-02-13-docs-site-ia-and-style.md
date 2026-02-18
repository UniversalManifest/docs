# UniversalManifest.net Documentation IA + Editorial Style

Date: 2026-02-13  
Work Order: `WO-lan-universal-manifest-professional-docs-site-and-publishing`  
Status: COMPLETE

## 1) Information Architecture

Top-level navigation for `universalmanifest.net` docs experience:

- `/universal-manifest` — orientation, scope, maturity, key references
- `/universal-manifest/spec` — normative contract and stub manifest catalog
- `/universal-manifest/integrations` — implementation paths (LAN + future systems)
- `/universal-manifest/governance` — decision process, release discipline, compatibility policy
- `/universal-manifest/roadmap` — done-done criteria, active milestones, closure path

Rationale:

- lead with orientation before deep specification details
- keep normative and non-normative boundaries explicit
- ensure implementers can quickly find entry points for build decisions

## 2) Editorial Style Rules (Linux Foundation-grade target)

Voice:

- precise, declarative, and implementation-oriented
- avoid hype language and future promises without conditions
- use RFC-style requirement language only where normative intent exists

Content chunking:

- one intent per page with explicit “why this matters”
- short sections with action-first headings
- references listed by canonical file path for auditability

Normative conventions:

- “MUST/MUST NOT/SHOULD/MAY” only in spec/conformance pages
- non-normative guidance labeled as “integration guidance” or “roadmap”
- keep policy, architecture, and operational runbooks in separate documents

## 3) Implemented Site Surfaces

- `/Users/grig/work/lan/lan-platform/packages/site-client/src/pages/universalManifest/UmDocsHomePage.tsx`
- `/Users/grig/work/lan/lan-platform/packages/site-client/src/pages/universalManifest/UmDocsSpecPage.tsx`
- `/Users/grig/work/lan/lan-platform/packages/site-client/src/pages/universalManifest/UmDocsIntegrationsPage.tsx`
- `/Users/grig/work/lan/lan-platform/packages/site-client/src/pages/universalManifest/UmDocsGovernancePage.tsx`
- `/Users/grig/work/lan/lan-platform/packages/site-client/src/pages/universalManifest/UmDocsRoadmapPage.tsx`
- `/Users/grig/work/lan/lan-platform/packages/site-client/src/pages/universalManifest/content.ts`

## 4) Source-of-Truth Inputs

- `/Users/grig/work/repo/universalmanifest/spec/`
- `/Users/grig/work/repo/universalmanifest/docs/`
- `/Users/grig/work/repo/universalmanifest/integrations/`
- `/Users/grig/work/lan/lan-platform/UNIVERSAL-MANIFEST.md`
- `/Users/grig/work/lan/lan-platform/.dev/ai/reports/universal-manifest/2026-02-13-spec-scope-and-done-definition.md`

## 5) Immediate Follow-up

- Split docs-only domain theming from LAN demo styling if this site becomes standalone.
- Add automated “broken reference” and “content freshness” checks in CI.
