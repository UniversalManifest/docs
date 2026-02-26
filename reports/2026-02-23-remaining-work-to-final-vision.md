# Universal Manifest -- Remaining Work to Final Vision

**Date:** 2026-02-25
**Author:** Independent gap analysis agent (Claude Opus 4.6)
**Scope:** Comprehensive gap inventory between current project state and the complete vision for a world-class, publicly releasable 1.0 standard.

---

## 1. Executive Summary

The Universal Manifest project has accomplished an impressive amount in a short timeframe: 41 of 43 work orders are either completed or declared complete, the v0.1 structural validation suite passes (40/40 fixtures), production deployment is live on both `universalmanifest.net` and `myum.net`, and the documentation site is built and deployed. The onboarding documentation was recently rewritten for plain-language clarity (WO-0039).

However, a thorough gap analysis reveals that **the project is approximately 60-65% of the way to a credible public 1.0 release**. The remaining 35-40% breaks down as follows:

- **Critical gaps** (would be embarrassing at a standards conference): Missing LICENSE file, no CONTRIBUTING.md, no CHANGELOG, no SECURITY policy, no issue templates, v0.1 schema `$id` still points to `localartist.network`, the TS package naming uses `@localartistnetwork/` instead of a neutral name, no npm publication, no multi-implementation interoperability evidence, and the `concepts.md` page contains JSON examples with comments (invalid JSON).
- **High gaps** (would undermine adoption credibility): No API reference documentation for the TS helper, journey runner design fragility (J01-J03 share a single `npm test` gate), no formal RFC/change-proposal mechanism, no explicit security considerations document, no migration guide from v0.1 to v0.2, and Astro build warnings persist.
- **Medium gaps** (quality polish needed): Two animation work orders not started (WO-0042, WO-0043), no SEO metadata beyond basic Starlight defaults, no changelog/release-notes page on the site, no explicit error catalog for the resolver, and human-reader testing remains unperformed.
- **Low gaps** (nice-to-have for excellence): Wrangler version outdated, no automated link checking in CI, no performance/load testing for the resolver, no i18n considerations documented.

The project's internal governance framework (done-done definition, evidence packs, journey proofs) is actually well above average for open-source standards projects. The primary risk is that **the open-source community-facing infrastructure is essentially absent** -- there is no LICENSE, no contribution guide, no code of conduct, and no issue templates. Without these, the project cannot credibly be called "open" regardless of technical quality.

---

## 2. Gap Inventory

### 2.1 Open-Source Community Infrastructure (CRITICAL)

| ID | Gap | Severity | Effort |
|----|-----|----------|--------|
| OSS-001 | No LICENSE file exists anywhere in the repository | CRITICAL | 1 hour |
| OSS-002 | No CONTRIBUTING.md -- external developers have no guide for contributing | CRITICAL | 4 hours |
| OSS-003 | No CODE_OF_CONDUCT.md | HIGH | 1 hour |
| OSS-004 | No SECURITY.md or security reporting policy | CRITICAL | 2 hours |
| OSS-005 | No CHANGELOG.md or release history | HIGH | 4 hours |
| OSS-006 | No GitHub issue templates (`.github/ISSUE_TEMPLATE/`) | HIGH | 2 hours |
| OSS-007 | No GitHub pull request template (`.github/PULL_REQUEST_TEMPLATE.md`) | MEDIUM | 1 hour |
| OSS-008 | No GitHub Discussions or community channel documented | MEDIUM | 1 hour |
| OSS-009 | README.md contains local absolute paths (`/Users/grig/...`) visible to external readers | HIGH | 1 hour |

### 2.2 Spec Completeness

| ID | Gap | Severity | Effort |
|----|-----|----------|--------|
| SPEC-001 | v0.1 `schema.json` `$id` still references `localartist.network` instead of `universalmanifest.net` | CRITICAL | 1 hour |
| SPEC-002 | v0.1 `schema.jsonld` namespace URL uses `universalmanifest.net` but the `schema.json` does not match -- internal inconsistency | HIGH | 1 hour |
| SPEC-003 | No explicit error taxonomy/catalog -- spec says "reject" but does not define what a conformance error response looks like | MEDIUM | 1 day |
| SPEC-004 | v0.1 spec does not define behavior when `@type` is an empty array (schema requires `minItems: 1` but spec text does not mention this) | LOW | 2 hours |
| SPEC-005 | v0.2 remains explicitly "draft" -- no timeline or criteria for promotion to stable | MEDIUM | 4 hours |
| SPEC-006 | No explicit v0.1-to-v0.2 migration guide exists | HIGH | 1 day |
| SPEC-007 | The `pointers` schema uses `"type": "array", "items": { "type": "object" }` -- completely untyped objects with no guidance on expected shape | MEDIUM | 1 day |
| SPEC-008 | The `claims`, `consents`, `devices` arrays are similarly untyped -- the schema enforces nothing about their contents | MEDIUM | 1 day |
| SPEC-009 | No normative `@type` value validation in schema -- the schema allows any string for `@type` even though spec text says "MUST include `um:Manifest`" | LOW | 4 hours |
| SPEC-010 | Well-known registry (REGISTRY.md) is non-normative and never referenced from the published site docs | MEDIUM | 2 hours |

### 2.3 Conformance Coverage

| ID | Gap | Severity | Effort |
|----|-----|----------|--------|
| CONF-001 | No clock-skew / future-dated `issuedAt` invalid fixture (CONFORMANCE.md section 2.3 mentions this SHOULD check) | MEDIUM | 2 hours |
| CONF-002 | No fixture for missing `manifestVersion` field | HIGH | 1 hour |
| CONF-003 | No fixture for empty `subject` field (only `missing-subject` exists) | LOW | 1 hour |
| CONF-004 | v0.2 has only 1 valid fixture (`minimal-signed-manifest.jsonld`) -- a single valid example is insufficient to demonstrate the profile works across different payloads | HIGH | 1 day |
| CONF-005 | No v0.2 valid fixture with shards, pointers, or claims alongside a signature | HIGH | 4 hours |
| CONF-006 | No fixture testing revocation-aware verification behavior (CONFORMANCE v0.2 section 2.2 defines this) | MEDIUM | 1 day |
| CONF-007 | No fixture testing that `statusRef`/`revocationCursor` fields do not affect canonicalization | MEDIUM | 4 hours |
| CONF-008 | No negative test for tampering (valid signature over modified payload) | HIGH | 4 hours |
| CONF-009 | The conformance fixture lists in `spec/v0.1/CONFORMANCE.md` do not include all the stub fixtures that exist under `examples/v0.1/stubs/` (7+ stubs missing from the list) | MEDIUM | 2 hours |
| CONF-010 | No conformance test for resolver behavior (the `site/src/content/docs/conformance/resolver.md` page exists but may lack executable test fixtures) | MEDIUM | 1 day |

### 2.4 Documentation Quality

| ID | Gap | Severity | Effort |
|----|-----|----------|--------|
| DOC-001 | `concepts.md` contains JSON with `//` comments (lines 72, 99) -- this is invalid JSON and will confuse implementers who copy-paste | CRITICAL | 1 hour |
| DOC-002 | No API reference documentation for the TypeScript helper package (`packages/universal-manifest/`) | HIGH | 1 day |
| DOC-003 | No explicit "Errors and Troubleshooting" page on the docs site | MEDIUM | 4 hours |
| DOC-004 | The "Reference Implementation" integration page is `hidden: true` in sidebar -- effectively invisible to site visitors unless they know the URL | MEDIUM | 1 hour |
| DOC-005 | The published spec page (`spec/v0.1.md`) still uses the term "portable state capsule" in its opening line | LOW | 30 min |
| DOC-006 | No architecture diagram showing the relationship between spec, resolver, tooling, and site | MEDIUM | 4 hours |
| DOC-007 | Integration pages (metaverse, RP1, smart-glasses) are speculative/aspirational with no concrete implementation evidence beyond fixture stubs | LOW | N/A (future) |
| DOC-008 | No page on the docs site explaining the v0.2 signature profile in implementer-friendly terms (current site page is a copy of the spec-level doc) | HIGH | 1 day |
| DOC-009 | `STATE-OF-THE-PROJECT.md` contains stale historical sections (dated 2026-02-19, 2026-02-20) that add noise without value for current readers | LOW | 2 hours |
| DOC-010 | The site has no search-engine optimization beyond Starlight defaults -- no custom `<meta>` descriptions on most pages, no Open Graph tags | MEDIUM | 4 hours |

### 2.5 TypeScript Tooling

| ID | Gap | Severity | Effort |
|----|-----|----------|--------|
| TS-001 | Package name is `@localartistnetwork/universal-manifest` -- should be a neutral name for a cross-ecosystem standard | CRITICAL | 2 hours |
| TS-002 | Package is `private: true` -- cannot be installed by external developers | HIGH | 2 hours (when publishing criteria are met) |
| TS-003 | No JSDoc comments on any exported functions/types | HIGH | 4 hours |
| TS-004 | No README.md in the package directory | HIGH | 2 hours |
| TS-005 | The JCS canonicalization implementation (`canonicalizeJson`) uses `localeCompare` for key sorting -- this is locale-dependent and technically incorrect for RFC 8785 which requires Unicode code-point ordering | CRITICAL | 4 hours |
| TS-006 | The `canonicalizeJson` function does not handle IEEE 754 special values (NaN, Infinity) per RFC 8785 requirements | HIGH | 4 hours |
| TS-007 | No unit tests for the canonicalization function in isolation -- only tested indirectly through fixture validation | HIGH | 4 hours |
| TS-008 | Type names use `Lan` prefix (e.g., `LanEntityV01`, `LanShardV01`, `LanSignatureV01`) -- legacy naming from "Local Artist Network" | HIGH | 2 hours |
| TS-009 | No exported utility for creating/signing manifests -- only assertion/validation is implemented | MEDIUM | 1 day |
| TS-010 | No exported utility for canonicalizing a manifest (the `canonicalizeJson` function is not exported) | MEDIUM | 1 hour |

### 2.6 Resolver (`myum.net`)

| ID | Gap | Severity | Effort |
|----|-----|----------|--------|
| RES-001 | No write/publish API -- manifests can only be added via direct KV operations | HIGH | 2-3 days |
| RES-002 | No authentication mechanism for publishing manifests | HIGH | 2-3 days |
| RES-003 | No bulk/batch resolution endpoint | LOW | 1 day |
| RES-004 | No versioning strategy for the resolver contract itself (currently `myum-resolver/v0.1` with no upgrade path documented) | MEDIUM | 4 hours |
| RES-005 | Dev fixture (`DEV_FIXTURE_UMID`) is hardcoded in the production resolver source -- should be environment-gated | MEDIUM | 2 hours |
| RES-006 | No rate limiting or abuse protection | MEDIUM | 1 day |
| RES-007 | No monitoring/alerting infrastructure documented | LOW | 4 hours |
| RES-008 | No explicit privacy policy for the resolver (beyond the inline note in the `.well-known` response) | MEDIUM | 4 hours |

### 2.7 Site and Publishing

| ID | Gap | Severity | Effort |
|----|-----|----------|--------|
| SITE-001 | Astro build produces duplicate-id warnings for 10 content files | HIGH | 4 hours |
| SITE-002 | No changelog/release-notes page on the published site | HIGH | 4 hours |
| SITE-003 | No `robots.txt` customization | LOW | 1 hour |
| SITE-004 | Sitemap exists but no submission to search engines is documented | LOW | 1 hour |
| SITE-005 | The GitHub link in the site header points to `github.com/LocalArtistNetwork/universalmanifest` -- verify this is the correct and publicly accessible URL | HIGH | 1 hour |
| SITE-006 | No custom 404 page content (Starlight default only) | LOW | 2 hours |
| SITE-007 | Two animation work orders (WO-0042, WO-0043) remain NOT_STARTED | MEDIUM | 2-3 days |
| SITE-008 | `localartist.network` compatibility aliases referenced in docs but implementation status unknown | MEDIUM | 4 hours |

### 2.8 CI/CD

| ID | Gap | Severity | Effort |
|----|-----|----------|--------|
| CI-001 | CI workflow does not run the terminology guard (`npm run check:terminology`) | HIGH | 30 min |
| CI-002 | CI workflow does not run production endpoint smoke tests | MEDIUM | 30 min |
| CI-003 | No automated deployment pipeline -- deployment appears to be manual `wrangler pages deploy` commands | HIGH | 1 day |
| CI-004 | No branch protection rules documented or enforced | MEDIUM | 2 hours |
| CI-005 | No automated link checking for docs site content | MEDIUM | 4 hours |
| CI-006 | No code coverage reporting | LOW | 4 hours |
| CI-007 | CI runs `npm run build` but not `npm run build:clean` -- may miss duplicate-id warnings that only appear on clean builds | MEDIUM | 30 min |

### 2.9 Security

| ID | Gap | Severity | Effort |
|----|-----|----------|--------|
| SEC-001 | No SECURITY.md file for responsible disclosure | CRITICAL | 2 hours |
| SEC-002 | No security considerations section in the spec documents | HIGH | 1 day |
| SEC-003 | The v0.2 signature profile does not address key rotation/revocation in detail -- `statusRef` and `revocationCursor` are defined but no concrete protocol is specified | HIGH | 2-3 days |
| SEC-004 | No threat model document (what attacks does the manifest format protect against? what does it not protect against?) | HIGH | 1-2 days |
| SEC-005 | The JCS canonicalization implementation concern (TS-005: locale-dependent sorting) is a potential security vulnerability in signature verification | CRITICAL | 4 hours |
| SEC-006 | No guidance on manifest size limits (a 100MB manifest would pass validation) | MEDIUM | 2 hours |
| SEC-007 | No guidance on nested depth limits for shards/entities | LOW | 2 hours |

### 2.10 Governance

| ID | Gap | Severity | Effort |
|----|-----|----------|--------|
| GOV-001 | No formal RFC/proposal mechanism for spec changes | HIGH | 1 day |
| GOV-002 | No explicit deprecation timeline or sunset process for v0.x versions | MEDIUM | 4 hours |
| GOV-003 | Decisions.md records internal project decisions but has no mechanism for external community input | HIGH | 4 hours |
| GOV-004 | No explicit maintainer list or governance structure (who decides what goes into the spec?) | HIGH | 4 hours |
| GOV-005 | Done-done framework is thorough but has never been formally executed with a signed evidence pack | MEDIUM | 1 day |
| GOV-006 | No process for external parties to propose well-known registry entries | MEDIUM | 4 hours |

### 2.11 Production Readiness (1.0-specific)

| ID | Gap | Severity | Effort |
|----|-----|----------|--------|
| PROD-001 | Zero external implementations exist -- all testing is single-implementation | CRITICAL | weeks-months |
| PROD-002 | No independent interoperability testing between two different implementations | CRITICAL | weeks-months |
| PROD-003 | No conformance test suite that can be run by external implementers without cloning this repo | HIGH | 1-2 weeks |
| PROD-004 | Package not published to npm -- external devs cannot `npm install` anything | HIGH | 2 hours (when ready) |
| PROD-005 | No formal version numbering beyond `0.1.0` in `package.json` -- no git tags, no releases | HIGH | 2 hours |
| PROD-006 | No performance benchmarks or scalability considerations documented | LOW | 1-2 days |
| PROD-007 | Human-reader validation has never been performed | MEDIUM | 1 day (requires human) |

---

## 3. Quality Assessment by Area

### 3.1 Spec Completeness -- Rating: 3.5/5

**Strengths:** v0.1 required fields are well-defined. JSON-LD context and JSON Schema exist. Unknown-field tolerance is clearly specified. TTL semantics are explicit. v0.2 signature profile (JCS + Ed25519) is a pragmatic, well-reasoned choice.

**Gaps:** The v0.1 `schema.json` `$id` still references the legacy domain. The optional sections (`claims`, `consents`, `devices`, `pointers`) are essentially untyped black boxes with no schema enforcement beyond "array of objects." The v0.2 spec is draft with no promotion criteria. No v0.1-to-v0.2 migration guide. The well-known registry is non-normative and not linked from the site.

### 3.2 Conformance Coverage -- Rating: 3/5

**Strengths:** 11 v0.1 invalid fixtures cover the most important structural failures. 8 v0.2 invalid fixtures cover signature-related failures well. The `validate-examples.mjs` script is clean and well-structured.

**Gaps:** Only 1 valid v0.2 fixture (minimal payload only). No fixtures for tampering detection (modified payload with original signature). No clock-skew fixtures. No revocation-aware verification fixtures. The v0.1 conformance fixture list is incomplete (misses several stubs). No conformance test runner that external implementers can use independently.

### 3.3 Documentation Quality -- Rating: 3.5/5

**Strengths:** The WO-0039 onboarding rewrite significantly improved first-read pages. The concepts page now has good structure with plain-language definitions and concrete examples. The site navigation (sidebar) is well-organized. Publishing, governance, and proof sections are present.

**Gaps:** `concepts.md` contains invalid JSON (comments). No API reference for the TS package. The reference-runtime integration page is hidden. No architecture overview diagram. No search-engine optimization. No changelog page on the site. The spec page for v0.2 on the site is mostly the raw spec text, not an implementer-friendly guide.

### 3.4 Tooling -- Rating: 2.5/5

**Strengths:** The TS helper covers v0.1 structural validation and v0.2 signature verification. The validation script is functional. The journey runner provides executable proof. The terminology guard (WO-0039) is a good quality gate.

**Gaps:** The package uses a legacy name (`@localartistnetwork/`). Types use legacy `Lan` prefix. No JSDoc documentation. The JCS canonicalization uses `localeCompare` (technically incorrect for RFC 8785). No unit tests for canonicalization in isolation. No signing/creation utilities -- only validation. The package is private and cannot be installed externally. No exported canonicalization function for implementers.

### 3.5 Resolver -- Rating: 3/5

**Strengths:** Clean, well-structured Cloudflare Worker implementation. Good HTTP semantics (CORS, ETag, proper status codes). The `.well-known/myum-resolver.json` discovery endpoint is a nice touch. Contract.md exists. Both standard and base64url UMID encoding are supported.

**Gaps:** No write/publish API. No authentication. No rate limiting. Dev fixture is hardcoded in production code. No bulk operations. No explicit upgrade path for the resolver contract. No monitoring documentation.

### 3.6 Site/Publishing -- Rating: 3.5/5

**Strengths:** Astro/Starlight site is professionally structured. Production deployment on Cloudflare Pages is operational. The sidebar organization is logical. Spec artifacts are published at stable URLs. CORS is configured correctly.

**Gaps:** Duplicate-id build warnings persist. No changelog page. GitHub link may point to incorrect/inaccessible URL. The legacy `localartist.network` compatibility story is documented but implementation status is unclear. Two animation work orders not started.

### 3.7 CI/CD -- Rating: 2.5/5

**Strengths:** A CI workflow exists that runs on PRs and pushes to main. It builds the site, runs package tests, runs journeys, and uploads artifacts.

**Gaps:** No automated deployment. No terminology guard in CI. No production smoke tests in CI. No link checking. No branch protection. Does not run `build:clean`. No code coverage.

### 3.8 Community/Adoption -- Rating: 1/5

**Strengths:** The project has good technical substance for adoption.

**Gaps:** No LICENSE file. No CONTRIBUTING.md. No CODE_OF_CONDUCT. No SECURITY policy. No issue templates. No PR template. No community channel. The README contains local filesystem paths. The package is private and unpublished. No external implementations exist. The GitHub URL in the site may not be publicly accessible.

### 3.9 Security -- Rating: 2/5

**Strengths:** The v0.2 signature profile is well-designed conceptually. Revocation direction is documented. The profile identification mechanism (algorithm + canonicalization pair) is forward-compatible.

**Gaps:** No SECURITY.md. No security considerations in the spec. No threat model. The JCS implementation has a potential correctness issue (locale-dependent sorting). No key rotation protocol. No manifest size limits. No nested depth guidance.

### 3.10 Governance -- Rating: 3/5

**Strengths:** Decisions.md is comprehensive and well-maintained. The done-done framework is unusually thorough for an open-source project. The critical-path document is clear. Work order tracking is disciplined.

**Gaps:** No RFC/proposal mechanism. No external participation pathway. No maintainer list or governance charter. No process for external registry contributions. The done-done framework has never been formally executed to completion.

### 3.11 Production Readiness -- Rating: 1.5/5

**Strengths:** The spec is coherent and the v0.1 contract is stable. Production infrastructure exists.

**Gaps:** Zero external implementations. No interoperability evidence. No published npm package. No git tags or releases. No conformance test suite for external use. No performance benchmarks. The maturity framework defines "World-ready" as requiring 3+ independent implementations, which is not close.

---

## 4. Recommended Work Orders

### WO-0044: Open-Source Community Infrastructure

**Objective:** Add all standard open-source community files required for a credible public repository.

**Scope:**
- Create `LICENSE` (choose license -- Apache 2.0 or CC-BY-4.0 for spec, MIT or Apache 2.0 for code)
- Create `CONTRIBUTING.md` with contribution workflow, coding standards, and CLA/DCO requirements
- Create `CODE_OF_CONDUCT.md` (Contributor Covenant or equivalent)
- Create `SECURITY.md` with responsible disclosure process
- Create `.github/ISSUE_TEMPLATE/` with bug report, feature request, and spec change templates
- Create `.github/PULL_REQUEST_TEMPLATE.md`
- Clean up `README.md` to remove local paths and add standard badges
- Rename or alias the package to a neutral name

**Estimated effort:** 1-2 days

### WO-0045: Schema and Naming Normalization

**Objective:** Resolve all legacy `localartist.network` and `Lan*` naming inconsistencies.

**Scope:**
- Update `spec/v0.1/schema.json` `$id` from `localartist.network` to `universalmanifest.net`
- Rename exported TypeScript types from `Lan*` to `Um*` or `UniversalManifest*`
- Rename package from `@localartistnetwork/universal-manifest` to a neutral name (e.g., `@universalmanifest/core` or `universal-manifest`)
- Verify all schema references are consistent across v0.1 and v0.2
- Document the `localartist.network` -> `universalmanifest.net` migration in `CHANGELOG.md`

**Estimated effort:** 1 day

### WO-0046: JCS Canonicalization Correctness and Testing

**Objective:** Ensure the JCS (RFC 8785) implementation is specification-compliant and independently testable.

**Scope:**
- Replace `localeCompare` with codepoint-order comparison for key sorting per RFC 8785
- Handle IEEE 754 special values (NaN, Infinity, -0) per RFC 8785
- Add unit tests for the canonicalization function using the RFC 8785 test vectors
- Export the canonicalization function for use by external implementers
- Add a signing utility function alongside the existing verification

**Estimated effort:** 1-2 days

### WO-0047: Security Documentation and Threat Model

**Objective:** Document security considerations, threat model, and operational security guidance.

**Scope:**
- Add security considerations section to both v0.1 and v0.2 spec docs
- Create a threat model document covering: replay attacks, manifest tampering, key compromise, revocation bypass, denial of service (oversized manifests), and privacy leakage
- Document manifest size limits and nested depth guidance
- Document key rotation and revocation operational guidance for v0.2
- Add security considerations to the resolver contract

**Estimated effort:** 2-3 days

### WO-0048: Conformance Suite Expansion

**Objective:** Expand conformance fixtures to cover edge cases, adversarial scenarios, and multi-payload v0.2 signing.

**Scope:**
- Add v0.2 valid fixtures: manifest with shards + signature, manifest with pointers + signature
- Add tampering fixture: valid signature over modified payload
- Add clock-skew fixture: `issuedAt` in the future
- Add missing `manifestVersion` fixture
- Add `statusRef`/`revocationCursor` fixture (verify they do not affect canonicalization)
- Update CONFORMANCE.md fixture lists to include all existing stubs
- Create a standalone conformance test runner that external implementers can use

**Estimated effort:** 3-5 days

### WO-0049: CI/CD Hardening

**Objective:** Make CI comprehensive and add automated deployment.

**Scope:**
- Add `npm run check:terminology` to CI workflow
- Switch CI to use `build:clean` instead of `build`
- Add automated link checking for docs content
- Add deployment automation (Cloudflare Pages deploy on merge to main)
- Document branch protection rules and enforce them
- Add production smoke test as a post-deploy step

**Estimated effort:** 1-2 days

### WO-0050: API Reference and Developer Experience

**Objective:** Make the TS helper package usable and documented for external developers.

**Scope:**
- Add JSDoc to all exported functions and types
- Create `packages/universal-manifest/README.md` with usage examples
- Add a "TypeScript Helper" page to the docs site
- Generate API reference documentation (TypeDoc or similar)
- Add examples of programmatic manifest creation and validation
- Prepare package for npm publication (update package name, add `publishConfig`, set `private: false`)

**Estimated effort:** 2-3 days

### WO-0051: Governance and External Participation Framework

**Objective:** Enable external community participation in spec evolution.

**Scope:**
- Create a governance charter defining decision-making process, roles, and responsibilities
- Create an RFC template for spec change proposals
- Document the process for external parties to propose well-known registry entries
- Add a maintainer/committer list
- Consider establishing a mailing list or GitHub Discussions for community engagement

**Estimated effort:** 2-3 days

### WO-0052: Fix Invalid JSON in Documentation

**Objective:** Remove JavaScript-style comments from JSON examples in documentation.

**Scope:**
- Fix `concepts.md` lines 72 and 99 where `//` comments appear in JSON code blocks
- Audit all other documentation pages for JSON examples with comments
- Add a CI check that validates JSON examples in documentation

**Estimated effort:** 2 hours

---

## 5. Prioritized Roadmap

### Phase A: Must-Have for Credible Public Release

These items would be embarrassing if missing when the project is presented publicly or linked from a standards body.

| Priority | Item | WO | Effort |
|----------|------|-----|--------|
| A.1 | Add LICENSE file | WO-0044 | 1 hour |
| A.2 | Add SECURITY.md | WO-0044 | 2 hours |
| A.3 | Add CONTRIBUTING.md | WO-0044 | 4 hours |
| A.4 | Fix v0.1 schema.json `$id` to `universalmanifest.net` | WO-0045 | 1 hour |
| A.5 | Fix JSON comments in `concepts.md` | WO-0052 | 30 min |
| A.6 | Fix JCS canonicalization to use codepoint ordering | WO-0046 | 4 hours |
| A.7 | Clean README.md (remove local paths) | WO-0044 | 1 hour |
| A.8 | Rename exported types from `Lan*` prefix | WO-0045 | 2 hours |
| A.9 | Add CODE_OF_CONDUCT.md | WO-0044 | 1 hour |
| A.10 | Add issue templates | WO-0044 | 2 hours |

**Estimated total Phase A effort:** 2-3 days

### Phase B: Important for Adoption

These items are needed for developers to actually adopt the standard.

| Priority | Item | WO | Effort |
|----------|------|-----|--------|
| B.1 | Security considerations in spec docs | WO-0047 | 1 day |
| B.2 | Threat model document | WO-0047 | 1-2 days |
| B.3 | API reference documentation for TS helper | WO-0050 | 2-3 days |
| B.4 | JSDoc on all exported functions | WO-0050 | 4 hours |
| B.5 | Additional v0.2 valid fixtures | WO-0048 | 1 day |
| B.6 | Tampering and adversarial fixtures | WO-0048 | 4 hours |
| B.7 | Rename package to neutral name | WO-0045 | 2 hours |
| B.8 | Add terminology guard to CI | WO-0049 | 30 min |
| B.9 | v0.1 to v0.2 migration guide | WO-0045 | 1 day |
| B.10 | CHANGELOG.md | WO-0044 | 4 hours |
| B.11 | Fix Astro duplicate-id warnings | -- | 4 hours |
| B.12 | Canonicalization unit tests | WO-0046 | 4 hours |
| B.13 | Governance charter and RFC mechanism | WO-0051 | 2-3 days |
| B.14 | Automated deployment pipeline | WO-0049 | 1 day |

**Estimated total Phase B effort:** 2-3 weeks

### Phase C: Nice-to-Have for Excellence

These items raise the quality bar significantly but are not blockers.

| Priority | Item | WO | Effort |
|----------|------|-----|--------|
| C.1 | Standalone conformance test suite for external implementers | WO-0048 | 1-2 weeks |
| C.2 | npm package publication | WO-0050 | 2 hours |
| C.3 | Signing/creation utility in TS package | WO-0050 | 1 day |
| C.4 | Animation enhancement (WO-0042, WO-0043) | existing | 2-3 days |
| C.5 | Architecture overview diagram | -- | 4 hours |
| C.6 | Human-reader validation testing | -- | 1 day |
| C.7 | SEO optimization for docs site | -- | 4 hours |
| C.8 | Resolver write/publish API | WO-0047+ | 2-3 days |
| C.9 | Resolver rate limiting | -- | 1 day |
| C.10 | Changelog/release-notes page on site | WO-0044 | 4 hours |
| C.11 | CI link checking | WO-0049 | 4 hours |
| C.12 | Update wrangler version | -- | 2 hours |

**Estimated total Phase C effort:** 3-4 weeks

### Phase D: Future Vision

These items are required for "World-ready" (Maturity C) but depend on external adoption.

| Priority | Item | Effort |
|----------|------|--------|
| D.1 | At least 3 independent implementations | months |
| D.2 | At least 2 implementations outside originating ecosystem | months |
| D.3 | Cross-implementation interoperability test events | weeks per event |
| D.4 | Formal evidence pack for done-done Maturity C | 1-2 weeks |
| D.5 | Long-term governance capacity demonstration | ongoing |
| D.6 | Data Integrity proof profile (future alternative to JCS+Ed25519) | weeks |
| D.7 | Multi-language SDK implementations (Python, Go, Rust) | weeks each |
| D.8 | Formal standards body submission (if desired) | months |

---

## 6. 1.0 Readiness Checklist

Binary yes/no criteria for "is this ready for a public 1.0 announcement?"

| # | Criterion | Status | Notes |
|---|-----------|--------|-------|
| 1 | LICENSE file exists | NO | No license file in repo |
| 2 | CONTRIBUTING.md exists | NO | No contribution guide |
| 3 | SECURITY.md exists | NO | No security policy |
| 4 | README.md contains no local filesystem paths | NO | Contains `/Users/grig/...` |
| 5 | All schema `$id` fields reference canonical domain | NO | v0.1 still references `localartist.network` |
| 6 | Package name is domain-neutral | NO | Uses `@localartistnetwork/` |
| 7 | All exported types use neutral naming | NO | `Lan*` prefix throughout |
| 8 | JCS canonicalization is RFC 8785 compliant | NO | Uses `localeCompare` |
| 9 | v0.1 spec contract is complete and unambiguous | MOSTLY | Optional sections are undertyped |
| 10 | v0.2 signature profile is testable and passing | YES | WO-0040 confirmed working |
| 11 | Conformance fixtures cover happy path + errors + adversarial | PARTIAL | Missing tampering, clock-skew, multi-payload v0.2 |
| 12 | Documentation is newcomer-friendly | MOSTLY | WO-0039 improved significantly; JSON comments remain |
| 13 | API reference exists for TS helper | NO | No JSDoc, no generated docs |
| 14 | Security considerations are documented | NO | No security section in spec |
| 15 | CI runs all quality checks | PARTIAL | Missing terminology guard, link checking |
| 16 | Production endpoints are operational | YES | 9/9 smoke tests pass |
| 17 | At least one external implementation exists | NO | Zero external implementations |
| 18 | Package is publishable to npm | NO | Private, legacy naming |
| 19 | Changelog/release history exists | NO | No CHANGELOG |
| 20 | Git tags/releases exist | NO | No tags |
| 21 | Governance structure is explicit | PARTIAL | Decisions.md is good; no governance charter |
| 22 | Issue templates exist | NO | No templates |
| 23 | `localartist.network` compatibility is implemented or documented as not needed | UNKNOWN | Doc exists but implementation status unclear |
| 24 | All site build warnings resolved | NO | 10 duplicate-id warnings |
| 25 | Threat model exists | NO | No threat model |

**Summary: 3 YES, 4 MOSTLY/PARTIAL, 1 UNKNOWN, 17 NO**

The project is not ready for a 1.0 announcement. The critical blockers are open-source infrastructure (LICENSE, CONTRIBUTING, SECURITY), naming normalization (legacy references throughout), JCS compliance, and zero external adoption evidence.

**Realistic path to 1.0:**
- Phase A (2-3 days) resolves the embarrassment-level issues
- Phase B (2-3 weeks) resolves the adoption-blocking issues
- After Phase B, the project could credibly announce as a "v0.1 public draft for early adopter feedback"
- Phases C and D are required before a "v1.0" claim is appropriate under the project's own maturity framework

---

**End of gap analysis.**
