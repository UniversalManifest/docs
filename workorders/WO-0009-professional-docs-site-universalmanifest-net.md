# WO-0009 — Professional standards documentation site for `universalmanifest.net`

**Status:** NOT_STARTED  
**Created:** 2026-02-12

## Objective

Design and implement a production-ready documentation site experience for Universal Manifest at `universalmanifest.net`, with quality and structure comparable to Linux Foundation project documentation.

## Scope

In scope:

- Define documentation information architecture (IA) and sitemap
- Establish editorial style/voice guide for standards documentation
- Build site framework and content structure for:
  - Overview
  - Specification versions
  - Conformance
  - Integrations
  - Governance/roadmap
  - Getting started and implementer guides
- Integrate versioned spec artifacts routing under `/ns/universal-manifest/`
- Configure deployment pipeline for static publishing

Out of scope:

- Legal/trademark policy pages requiring external counsel
- Full marketing site and campaign content

## Deliverables

- IA + content map:
  - `docs/site/INFORMATION-ARCHITECTURE.md`
- Style guide:
  - `docs/site/EDITORIAL-STYLE-GUIDE.md`
- Site implementation scaffold:
  - `site/` (framework + config + content pages)
- Deployment docs:
  - `docs/site/DEPLOYMENT.md`

## Acceptance criteria

- [ ] Site has complete top-level navigation for standards consumers
- [ ] Content is chunked by audience (maintainers, implementers, evaluators)
- [ ] Versioned docs are discoverable and linked to concrete artifacts
- [ ] Conformance and adoption paths are first-class pages
- [ ] Build and deploy steps are reproducible from repository docs
- [ ] `universalmanifest.net` publishing path matches domain architecture policy

## Dependencies

- `docs/DOMAIN-ARCHITECTURE.md`
- `docs/PUBLISHING-AND-VERSIONING.md`
- `docs/RELEASING.md`

