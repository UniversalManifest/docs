# WO-0039 Phase 1: Onboarding Language Source Map and Rewrite Plan

**Date**: 2026-02-23
**Work Order**: WO-0039 (Onboarding Plain-Language Rewrite and Source Propagation Hardening)
**Phase**: 1 -- Jargon/Source-Map Inventory (READ-ONLY research)
**Scope**: The four first-read onboarding files, plus propagation into surrounding docs

---

## 1. Jargon Term Inventory

### Legend

- **Category**:
  - `UNDEFINED_JARGON` -- term used without any prior definition
  - `INSIDER_FRAMING` -- language that assumes familiarity with internal project context
  - `CIRCULAR_DEFINITION` -- term defined using other undefined terms
  - `ASSUMED_KNOWLEDGE` -- concept that presupposes technical background not all readers share

- **Severity**:
  - `CRITICAL` -- blocks comprehension of what UM is or why to use it
  - `HIGH` -- substantially impairs understanding of a first-read section
  - `MEDIUM` -- confusing but does not block the overall message
  - `LOW` -- minor friction, acceptable for a technical audience

### 1.1 Complete term table (all four onboarding files)

| # | Term / Phrase | File(s) : Line(s) | Category | Severity | Recommended Action |
|---|---|---|---|---|---|
| 1 | **"portable state capsule"** | `index.md:3,6`; `overview.md:8` | UNDEFINED_JARGON | CRITICAL | REWRITE to plain English ("a portable document format for passing identity and permission data between systems") |
| 2 | **"integration pair"** | `overview.md:34` | UNDEFINED_JARGON | CRITICAL | REPLACE_WITH "each time two systems need to share data" |
| 3 | **"facets"** (no definition before use) | `overview.md:10,38`; `index.md:15`; `quick-start.md:20,32`; `concepts.md:10` | UNDEFINED_JARGON | CRITICAL | DEFINE_INLINE on first use: "Facets are named, optional sub-sections within a manifest that group related data (for example, a `publicProfile` facet and a `deviceRegistration` facet)." |
| 4 | **"UMID"** (acronym before expansion) | `overview.md:41`; `index.md:13,18`; `quick-start.md:18`; `concepts.md:7` | UNDEFINED_JARGON | CRITICAL | DEFINE_INLINE on first use: "UMID (Universal Manifest Identifier) -- the unique `@id` of a manifest" |
| 5 | **"convergence profile"** | `overview.md:12` | INSIDER_FRAMING | HIGH | REMOVE or REWRITE: "UM re-uses existing standards (JSON-LD, W3C Verifiable Credentials patterns) rather than inventing from scratch" |
| 6 | **"CEO-directed integration lanes"** | `overview.md:18` | INSIDER_FRAMING | HIGH | REMOVE from onboarding; reframe as "Current integration targets include:" |
| 7 | **"RP1 spatial fabric"** | `overview.md:21` | UNDEFINED_JARGON + INSIDER_FRAMING | HIGH | REPLACE_WITH a plain description or remove from first-read page; move to integrations page only |
| 8 | **"envelope"** (used without definition) | `overview.md:38`; `index.md:26`; `quick-start.md:20` | UNDEFINED_JARGON | HIGH | DEFINE_INLINE: "The manifest acts as an envelope -- a wrapper with standard header fields (`@id`, `subject`, TTL) that can carry different kinds of payload data inside." |
| 9 | **"resolver"** / **"resolver domain"** | `overview.md:30,41,63`; `index.md:18`; `quick-start.md:61,63`; `concepts.md:18` | UNDEFINED_JARGON | HIGH | DEFINE_INLINE: "A resolver is a web service that looks up a manifest by its UMID (for example, `myum.net/{UMID}`)." |
| 10 | **"pointers"** (vague definition) | `overview.md:10,38`; `index.md:15`; `quick-start.md:20,33`; `concepts.md:11` | UNDEFINED_JARGON | HIGH | DEFINE_INLINE: "Pointers are references (URLs) to authoritative data stored elsewhere, so you link to data instead of copying it." |
| 11 | **"canonical data" / "canonical sources"** | `quick-start.md:20,33`; `concepts.md:11` | ASSUMED_KNOWLEDGE | HIGH | DEFINE_INLINE: "Canonical means the single authoritative source of a piece of data (for example, a user profile on their home server)." |
| 12 | **"trusted context"** | `index.md:8` | UNDEFINED_JARGON | HIGH | REWRITE: "enough verified information for the receiving system to act" |
| 13 | **"per-integration payload design"** | `index.md:8` | UNDEFINED_JARGON | HIGH | REPLACE_WITH "building a custom data format for every pair of systems that need to talk" |
| 14 | **"envelope contract"** | `index.md:26` | UNDEFINED_JARGON | HIGH | REPLACE_WITH "a single shared document format" |
| 15 | **"brittle mappings"** | `overview.md:34` | UNDEFINED_JARGON | MEDIUM | REPLACE_WITH "fragile, hard-to-maintain data translations" |
| 16 | **"TTL"** (before expansion) | `overview.md:38`; `quick-start.md:18,27`; `concepts.md:8` | ASSUMED_KNOWLEDGE | MEDIUM | DEFINE_INLINE on first use: "TTL (time-to-live) -- the `issuedAt`/`expiresAt` window during which a manifest is considered valid" |
| 17 | **"normative"** / **"normative requirements"** / **"normative artifacts"** | `overview.md:24`; `quick-start.md:38` | ASSUMED_KNOWLEDGE | MEDIUM | REPLACE_WITH "required by the spec" or "official spec artifacts"; avoid standards jargon in onboarding |
| 18 | **"fixtures"** | `overview.md:60`; `quick-start.md:36,44` | ASSUMED_KNOWLEDGE | MEDIUM | REPLACE_WITH "test examples" or DEFINE_INLINE: "Fixtures are pre-built example manifests you can use for testing." |
| 19 | **"harness"** / **"Interactive harness loader"** | `quick-start.md:53,55` | UNDEFINED_JARGON | MEDIUM | REPLACE_WITH "interactive test tool" or DEFINE_INLINE: "The harness is a browser-based tool that loads and displays manifest examples." |
| 20 | **"freshness for use"** | `quick-start.md:27`; `concepts.md:8` | UNDEFINED_JARGON | MEDIUM | REWRITE: "whether the manifest has expired" or "whether the manifest is still within its valid time window" |
| 21 | **"projections"** | `concepts.md:10` | UNDEFINED_JARGON | MEDIUM | DEFINE_INLINE: "A projection is a view of a manifest tailored for a specific context (for example, showing only public fields on a display screen)." |
| 22 | **"composable"** (used without explaining how) | `overview.md:10`; `quick-start.md:32`; `concepts.md:10` | UNDEFINED_JARGON | MEDIUM | DEFINE_INLINE: "Composable means you can mix and match facets independently -- include only the ones relevant to your use case." |
| 23 | **"Metaverse Universal Manifest (MUM)"** | `overview.md:16` | INSIDER_FRAMING | MEDIUM | REMOVE from onboarding or reduce to a single sentence: "UM evolved from earlier metaverse-focused work." No need to name MUM. |
| 24 | **"local-first"** | `overview.md:30`; `index.md:3,27` | ASSUMED_KNOWLEDGE | MEDIUM | DEFINE_INLINE: "Local-first means the system can work with cached data even when offline, using TTL to know when to refresh." |
| 25 | **"bounded caching"** | `index.md:27` | UNDEFINED_JARGON | MEDIUM | DEFINE_INLINE: "Bounded caching means caching data only until its TTL expires." |
| 26 | **"unknown-field tolerance"** | `index.md:28`; `concepts.md:9` | ASSUMED_KNOWLEDGE | MEDIUM | REWRITE: "systems must safely ignore fields they do not recognize, so older consumers do not break when new fields are added" |
| 27 | **"signature profile"** | `index.md:29` | ASSUMED_KNOWLEDGE | MEDIUM | DEFINE_INLINE: "A signature profile defines how a manifest is cryptographically signed and verified (v0.2 uses JCS + Ed25519)." |
| 28 | **"domain split"** | `index.md:42` | UNDEFINED_JARGON | MEDIUM | DEFINE_INLINE: "The spec site (`universalmanifest.net`) and the resolver (`myum.net`) are separate by design." Explain WHY. |
| 29 | **"Workbench"** (used before any context) | `overview.md:62` | UNDEFINED_JARGON | MEDIUM | DEFINE_INLINE: "The Workbench is a browser-based tool for creating, editing, and validating manifests." |
| 30 | **"consumer checks"** / **"minimum viable consumer"** | `overview.md:59`; `quick-start.md:22` | ASSUMED_KNOWLEDGE | MEDIUM | DEFINE_INLINE: "A consumer is any system that reads and acts on a manifest. Consumer checks are the minimum validations it must perform." |
| 31 | **"proof journeys"** / **"endpoint smoke"** | `overview.md:61` | UNDEFINED_JARGON | MEDIUM | DEFINE_INLINE: "Proof journeys are end-to-end tests that verify a real implementation. Endpoint smoke tests verify that published URLs return correct data." |
| 32 | **"publishing patterns"** | `overview.md:63` | UNDEFINED_JARGON | MEDIUM | REWRITE: "how to host and version your manifest artifacts for production use" |
| 33 | **"JSON-LD context artifact"** | `quick-start.md:40` | ASSUMED_KNOWLEDGE | MEDIUM | REPLACE_WITH "JSON-LD vocabulary file" and add parenthetical: "(defines the meaning of fields in the manifest)" |
| 34 | **"structural schema artifact"** | `quick-start.md:41` | ASSUMED_KNOWLEDGE | MEDIUM | REPLACE_WITH "JSON Schema file" and add parenthetical: "(validates the structure of a manifest)" |
| 35 | **"well-known discovery document"** | `quick-start.md:42` | ASSUMED_KNOWLEDGE | MEDIUM | DEFINE_INLINE: "A `.well-known` URL is a standard convention (RFC 8615) for auto-discovery of configuration data." |
| 36 | **"interoperable state transfer"** | `overview.md:28` | UNDEFINED_JARGON | MEDIUM | REPLACE_WITH "passing data between different systems reliably" |
| 37 | **"deterministic resolver contracts"** | `overview.md:30` | UNDEFINED_JARGON | MEDIUM | REPLACE_WITH "resolver services that always behave the same way for the same input" |
| 38 | **"forward compatibility"** | `overview.md:39`; `quick-start.md:19` | ASSUMED_KNOWLEDGE | LOW | DEFINE_INLINE: "Forward compatibility means older consumers can safely process manifests that include newer fields they do not understand." |
| 39 | **"JSON-LD"** | `quick-start.md:18`; `overview.md:40` | ASSUMED_KNOWLEDGE | LOW | Acceptable for technical audience; optionally add "(a JSON format with linked-data semantics)" on first use |
| 40 | **"issuer-minted"** | `concepts.md:7` | UNDEFINED_JARGON | MEDIUM | REWRITE: "created by the system or organization that produces the manifest" |
| 41 | **"urn:uuid"** | `concepts.md:7` | ASSUMED_KNOWLEDGE | LOW | DEFINE_INLINE: "a standard URI format for universally unique identifiers" |
| 42 | **"overbuilding"** | `concepts.md:13` | UNDEFINED_JARGON | MEDIUM | REPLACE_WITH "adding unnecessary complexity" or "over-engineering" |
| 43 | **"multiple ecosystems"** | `concepts.md:13` | UNDEFINED_JARGON | LOW | REPLACE_WITH specific examples: "across web apps, mobile apps, AR devices, and IoT systems" |
| 44 | **"Done-Done"** | `index.md:44` | INSIDER_FRAMING | LOW | Acceptable as a named page; optionally add "(release-readiness checklist)" |
| 45 | **"overlay-lanes map"** | `overview.md:47` | UNDEFINED_JARGON | MEDIUM | DEFINE_INLINE or REWRITE heading: "Integration overview (animated diagram)" |
| 46 | **"shape + intent fixtures"** | `stub-manifests.md:7` | UNDEFINED_JARGON | MEDIUM | REWRITE: "example documents showing the intended structure, not final schemas" |
| 47 | **"ontology"** | `stub-manifests.md:7` | ASSUMED_KNOWLEDGE | LOW | REPLACE_WITH "vocabulary" or "field definitions" |
| 48 | **"signage runtime"** | `stub-manifests.md:22` | INSIDER_FRAMING | MEDIUM | REPLACE_WITH "digital signage display software" |
| 49 | **"venue edge"** | `stub-manifests.md:18` | INSIDER_FRAMING | MEDIUM | DEFINE_INLINE: "A venue edge is a local server or device at a physical location that processes manifests." |
| 50 | **"safe public projection for screens"** | `stub-manifests.md:20` | UNDEFINED_JARGON | MEDIUM | REWRITE: "a manifest containing only the fields safe to display publicly" |
| 51 | **"future profile projection surface"** | `stub-manifests.md:21` | UNDEFINED_JARGON | MEDIUM | REWRITE: "a manifest shaped for social-profile display" |

---

## 2. Source Propagation Map

This section traces where each problematic term propagates beyond the four first-read files. Only user-facing documentation under `site/` and `docs/` is listed; audit/report files that merely discuss the jargon are excluded.

### 2.1 "portable state capsule"

| File | Line(s) |
|---|---|
| `site/src/content/docs/index.md` | 3 (description meta), 6 |
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 8 |
| `site/src/content/docs/integrations/social.md` | 37 |
| `site/src/content/docs/spec/v0.1.md` | 5 |
| `site/src/content/docs/spec/v0.2.md` | 5, 35 |
| `site/public/diagrams/universal-manifest-overview-template.svg` | 24 |
| `site/astro.config.mjs` | 9 (site description) |
| `spec/v0.1/README.md` | 5 |
| `spec/v0.2/SIGNATURE-PROFILE.md` | 74 |
| `README.md` (repo root) | 9 |
| `docs/DEPTH-AND-SCOPE.md` | 19, 207 |
| `docs/CRUCIAL-DETAILS.md` | 6 |
| `docs/STUB-MANIFESTS.md` | 57, 571 |
| `docs/site/EDITORIAL-STYLE-GUIDE.md` | 18 |

**Status**: Pervasive. Appears in 14+ files. The term itself is NOT inherently bad -- it just needs to be defined on first use in onboarding pages. The editorial style guide (line 18) explicitly endorses it as the "core concept", which means the guide itself needs a note requiring an inline definition.

### 2.2 "integration pair"

| File | Line(s) |
|---|---|
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 34 |

**Status**: Appears in exactly ONE user-facing file (the overview). Easy to fix with a single edit.

### 2.3 "brittle mappings"

| File | Line(s) |
|---|---|
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 34 |

**Status**: Co-occurs with "integration pair" in the same sentence. Fix together.

### 2.4 "convergence profile"

| File | Line(s) |
|---|---|
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 12 |

**Status**: Appears in exactly ONE user-facing file. Easy to remove or replace.

### 2.5 "CEO-directed integration lanes"

| File | Line(s) |
|---|---|
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 18 |
| `site/src/content/docs/integrations/rp1-spatial-fabric.md` | 8 |
| `site/src/content/docs/integrations/smart-glasses-ar.md` | 8 |

**Status**: Three files. The onboarding page is the critical fix; the integration pages can keep a softer version.

### 2.6 "RP1 spatial fabric"

| File | Line(s) |
|---|---|
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 21 |
| `site/src/content/docs/integrations/rp1-spatial-fabric.md` | 2, 3, 8, 12, 15, 25, 45, 46 |
| `site/src/content/docs/integrations/social.md` | 101 |

**Status**: Has its own dedicated integration page. Should be removed from the overview first-read page and kept only in the integrations section.

### 2.7 "MUM" / "Metaverse Universal Manifest"

| File | Line(s) |
|---|---|
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 16 |
| `site/src/content/docs/integrations/metaverse.md` | 12 |

**Status**: Two files. Remove the named acronym from onboarding; keep brief lineage mention in integrations.

### 2.8 "envelope" (without definition)

| File | Line(s) |
|---|---|
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 38 |
| `site/src/content/docs/getting-started/quick-start.md` | 20 |
| `site/src/content/docs/getting-started/stub-manifests.md` | 22 |
| `site/src/content/docs/index.md` | 26 |
| `site/src/content/docs/spec/v0.1.md` | 39 |
| `site/src/content/docs/spec/v0.2.md` | 9, 37 |
| `site/src/content/docs/conformance/v0.1.md` | 53 |
| `site/src/content/docs/conformance/v0.2.md` | 36 |
| `site/src/content/docs/integrations/oma-trust.md` | 14 |
| `site/src/content/docs/integrations/rp1-spatial-fabric.md` | 25 |
| `site/src/content/docs/integrations/reference-runtime.md` | 50, 55 |
| `site/src/content/docs/governance/decisions.md` | 26 |
| `site/src/content/docs/governance/done-done.md` | 72 |

**Status**: Widely used (13+ files). Define it once in the first onboarding file, then use consistently. Deeper pages can use it freely once it is established.

### 2.9 "facets"

| File | Line(s) |
|---|---|
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 10, 38 |
| `site/src/content/docs/getting-started/quick-start.md` | 20, 32 |
| `site/src/content/docs/getting-started/concepts.md` | 10 |
| `site/src/content/docs/getting-started/stub-manifests.md` | 33 |
| `site/src/content/docs/getting-started/critical-path.md` | 32 |
| `site/src/content/docs/index.md` | 15 |
| `site/src/content/docs/spec/v0.1.md` | 34, 56 |
| `site/src/content/docs/integrations/metaverse.md` | 24 |
| `site/src/content/docs/integrations/smart-glasses-ar.md` | 42 |
| `site/src/content/docs/integrations/oma-trust.md` | 18 |
| `site/src/content/docs/integrations/rp1-spatial-fabric.md` | 45 |

**Status**: Core term, used in 11+ files. Must be defined on first encounter (overview.md or index.md).

### 2.10 "pointers"

| File | Line(s) |
|---|---|
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 10, 38 |
| `site/src/content/docs/getting-started/quick-start.md` | 20, 33 |
| `site/src/content/docs/getting-started/concepts.md` | 11 |
| `site/src/content/docs/getting-started/stub-manifests.md` | 34 |
| `site/src/content/docs/getting-started/critical-path.md` | 32 |
| `site/src/content/docs/index.md` | 15 |
| `site/src/content/docs/spec/v0.1.md` | 10, 38, 56, 94 |
| `site/src/content/docs/integrations/metaverse.md` | 24 |
| `site/src/content/docs/integrations/social.md` | 54 |
| `site/src/content/docs/integrations/oma-trust.md` | 18 |

**Status**: Core term, used in 10+ files. Must be defined on first encounter.

### 2.11 "UMID"

| File | Line(s) |
|---|---|
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 41 |
| `site/src/content/docs/getting-started/quick-start.md` | 18 |
| `site/src/content/docs/getting-started/concepts.md` | 7 |
| `site/src/content/docs/index.md` | 13, 18 |
| (Also appears widely in spec, conformance, publishing, and proof pages) |

**Status**: Core acronym. Must be expanded on first use: "UMID (Universal Manifest Identifier)".

### 2.12 "resolver"

| File | Line(s) |
|---|---|
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 30, 41, 63 |
| `site/src/content/docs/getting-started/quick-start.md` | 61, 63 |
| `site/src/content/docs/getting-started/concepts.md` | 18 |
| `site/src/content/docs/getting-started/critical-path.md` | 17, 71 |
| `site/src/content/docs/index.md` | 18 |
| (Also appears widely in conformance, publishing, and proof pages) |

**Status**: Core term. Define it early in the onboarding path.

### 2.13 "normative"

| File | Line(s) in getting-started |
|---|---|
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 24 |
| `site/src/content/docs/getting-started/quick-start.md` | 38 |
| `site/src/content/docs/getting-started/workbench.md` | 29, 35 |

**Status**: Standards jargon. Replace with "required by the spec" in onboarding pages.

### 2.14 "local-first"

| File | Line(s) |
|---|---|
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 30 |
| `site/src/content/docs/getting-started/stub-manifests.md` | 39 |
| `site/src/content/docs/index.md` | 3, 27 |
| `site/src/content/docs/conformance/v0.1.md` | 10 |
| `site/src/content/docs/spec/v0.1.md` | 14 |

**Status**: Used in 5 onboarding-adjacent files. Define on first use.

### 2.15 "TTL" (before expansion)

| File | Line(s) in getting-started |
|---|---|
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 38 |
| `site/src/content/docs/getting-started/quick-start.md` | 18, 27 |
| `site/src/content/docs/getting-started/concepts.md` | 8 |
| `site/src/content/docs/getting-started/critical-path.md` | 30 |
| `site/src/content/docs/getting-started/stub-manifests.md` | 32 |
| `site/src/content/docs/getting-started/workbench.md` | 21 |

**Status**: Used in 6 getting-started files. Expand on first use.

### 2.16 "fixtures"

| File | Line(s) in getting-started |
|---|---|
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | 60 |
| `site/src/content/docs/getting-started/quick-start.md` | 36, 44 |
| `site/src/content/docs/getting-started/critical-path.md` | 15, 43, 44, 58 |
| `site/src/content/docs/getting-started/stub-manifests.md` | 7, 12, 14, 16, 18-25, 44, 50 |

**Status**: Pervasive in getting-started. Either define it on first encounter or use "test examples" consistently.

---

## 3. Rewrite Plan

### 3.1 File: `site/src/content/docs/index.md` (Landing Page)

**Current problems:**

1. Opening line ("portable state capsule standard") uses undefined jargon as the primary definition.
2. Line 8 attempts to clarify "in practical terms" but introduces MORE jargon: "trusted context", "per-integration payload design".
3. "UMID" introduced on line 13 without expanding the acronym.
4. "facets, pointers, claims, and consents" listed on line 15 without any definitions.
5. "resolver domain" on line 18 -- unexplained architectural detail.
6. "envelope contract" on line 26 -- undefined.
7. "local-first with bounded caching" on line 27 -- buzzwords.
8. "unknown-field tolerance" on line 28 -- not explained for newcomers.
9. "v0.2 signature profile" on line 29 -- not defined.
10. "Domain Split" on line 42 -- unexplained navigation target.
11. "Done-Done" on line 44 -- insider name for a release checklist.

**Proposed approach:**

- Rewrite the opening 2 lines to be plain English: say WHAT it is (a document format), WHO it helps (developers building systems that need to share user/device/app data), and WHY it exists (to avoid reinventing custom data formats for every pair of systems).
- Move the "core model" list (lines 12-15) into short, self-contained definitions. Each bullet should define its term before using it.
- Push architectural details (resolver domain, domain split) to a brief "Architecture at a glance" sub-section or defer entirely to deeper pages.
- Replace "envelope contract" with "a single shared document format".
- Add one-sentence definitions for "local-first", "bounded caching", "unknown-field tolerance", and "signature profile" -- or link to a concepts page that actually defines them properly.

**Key plain-language replacements:**

| Current | Replacement |
|---|---|
| "portable state capsule standard" | "a portable document format for sharing identity and state between systems" |
| "trusted context" | "verified information" |
| "per-integration payload design" | "building a custom data format for every pair of systems" |
| "envelope contract" | "a single, shared document format" |
| "local-first with bounded caching" | "works offline using cached data, with automatic expiration" |
| "unknown-field tolerance" | "safely ignores fields it does not recognize" |

---

### 3.2 File: `site/src/content/docs/getting-started/universal-manifest-overview.md` (Overview)

**Current problems:**

1. Line 8: "portable state capsule" -- opening definition is jargon.
2. Line 10: "composable facets" -- undefined on first use.
3. Line 12: "convergence profile" -- insider standards language.
4. Lines 14-16: MUM lineage section -- insider history irrelevant to a first-time reader.
5. Line 18: "CEO-directed integration lanes" -- organizational framing that means nothing to an external developer.
6. Line 21: "RP1 spatial fabric" -- undefined technology with no link or explanation.
7. Line 24: "normative requirements" -- standards jargon.
8. Line 28: "interoperable state transfer" -- jargon.
9. Line 30: "deterministic resolver contracts" -- jargon.
10. Line 34: "integration pair" -- the most-flagged term; completely undefined.
11. Line 34: "brittle mappings" -- jargon.
12. Line 38: "stable envelope" -- undefined.
13. Line 38: "TTL" -- acronym before expansion.
14. Line 41: "UMID" -- acronym before expansion.
15. Lines 59-63: "How to start" section -- nearly every step uses undefined jargon ("consumer checks", "fixtures", "proof journeys", "endpoint smoke", "Workbench", "resolver and publishing patterns").
16. Line 47: "Overlay-lanes map" heading -- undefined concept.

**Proposed approach:**

- Rewrite the opening paragraph (lines 8-10) from scratch. Lead with the problem ("When systems need to share data about a user, device, or app, they usually invent a custom format. UM replaces that with one standard document.").
- Remove "convergence profile" entirely. Replace with a single plain-language sentence.
- Move or dramatically reduce the "Origin and lineage" section. A new adopter does not need to know about MUM. Optionally keep one sentence.
- Replace "CEO-directed integration lanes" with "Current integration targets" and remove organizational context.
- Either remove "RP1 spatial fabric" from this page or replace with a 3-word plain description ("3D/spatial computing systems") with a link to the integration page.
- Rewrite "What problem it solves" (lines 32-41) to lead with a concrete scenario, not jargon.
- Rewrite "How to start" (lines 56-63) so every step is self-contained and uses plain language.

**Key plain-language replacements:**

| Current | Replacement |
|---|---|
| "portable state capsule format" | "a portable document format for sharing identity, permissions, and data references between systems" |
| "composable facets" | "optional, named data sections" |
| "convergence profile over existing standards" | "builds on existing standards like JSON-LD rather than inventing from scratch" |
| "CEO-directed integration lanes" | "Current integration targets" |
| "RP1 spatial fabric style systems" | "3D/spatial computing platforms" (with link) |
| "normative requirements" | "required by the spec" |
| "integration pair tends to invent custom payloads and brittle mappings" | "every time two systems need to share data, they tend to build custom, fragile formats from scratch" |
| "stable envelope" | "a standard document wrapper with fixed header fields" |
| "resolvable runtime lookup" | "you can fetch any manifest by its URL" |
| "endpoint smoke" | "endpoint smoke tests (verifying published URLs respond correctly)" |

---

### 3.3 File: `site/src/content/docs/getting-started/concepts.md` (Concepts)

**Current problems:**

1. Entire file is a 5-item bullet list of undefined terms, each "defined" with more undefined terms.
2. "UMID: the manifest `@id` (issuer-minted; v0.1 recommends `urn:uuid:<uuidv4>`)" -- circular: uses `@id`, "issuer-minted", and `urn:uuid` without explanation.
3. "TTL: `issuedAt`/`expiresAt` define freshness for use" -- does not explain what TTL stands for or what "freshness for use" means.
4. "Unknown-field tolerance" -- does not explain WHY this matters.
5. "Facets: small composable sections used for projections" -- "composable" and "projections" are undefined.
6. "Pointers: references to canonical data that lives elsewhere" -- "canonical" is undefined.
7. "avoid overbuilding" -- vague.
8. The closing line ("keep adoption possible across multiple ecosystems") is hand-wavy.
9. No examples. No code. No diagrams. No scenarios.

**Proposed approach:**

- Rewrite from scratch as a progressive-disclosure document.
- For each concept:
  - One plain-English sentence saying what it IS.
  - One sentence saying WHY it matters.
  - One concrete example (code snippet or scenario).
- Structure: lead with the manifest as a whole (what the document looks like), then introduce each part (UMID, TTL, facets, pointers, unknown-field tolerance).
- Add a minimal JSON example at the top showing a real manifest with labels pointing to each concept.
- End with a "now you know enough to read the Quick Start" transition.

**Key plain-language replacements:**

| Current | Replacement |
|---|---|
| "the manifest `@id` (issuer-minted)" | "a unique identifier assigned by whoever creates the manifest" |
| "`issuedAt`/`expiresAt` define freshness for use" | "two timestamps that define when the manifest was created and when it expires -- systems must reject expired manifests" |
| "small composable sections used for projections" | "optional named sections within a manifest that group related data; you include only the ones you need" |
| "references to canonical data that lives elsewhere" | "URLs pointing to the authoritative source of data (so you link to it instead of copying it)" |
| "avoid overbuilding" | "keep the format simple enough that any system can adopt it" |

---

### 3.4 File: `site/src/content/docs/getting-started/quick-start.md` (Quick Start)

**Current problems:**

1. Line 18: "JSON(-LD)" parenthetical -- awkward notation; just say "JSON-LD".
2. Line 18: "UMID" used without prior expansion on this page (though it links to concepts).
3. Line 20: "The manifest is **an envelope**" -- undefined metaphor.
4. Line 20: "canonical data elsewhere" -- "canonical" undefined.
5. Line 27: "freshness for use" -- undefined phrase.
6. Line 32: "composable fragments" -- what does composable mean?
7. Line 33: "canonical sources" -- undefined.
8. Line 38: "Normative artifacts" -- standards jargon.
9. Line 40: "JSON-LD context artifact" -- opaque label.
10. Line 41: "Structural schema artifact" -- opaque label.
11. Line 42: "Well-known discovery document" -- unexplained convention.
12. Line 44: "Fixtures (examples)" -- uses "fixtures" first, "examples" in parenthetical. Use "examples" first.
13. Line 53: "harness" -- undefined.
14. Line 57: "Workbench" -- brief context given but "guided import/edit/validate/export" is jargon-dense.
15. Line 61: "resolver implementation" -- undefined.

**Proposed approach:**

- This is the MOST actionable of the four files, so changes should be lighter. The numbered-step structure is good.
- For Step 1: Replace "Key takeaways you need" with a brief, self-contained summary that does not assume concepts.md was read.
- For Step 2: Keep the implementation checklist. Replace "freshness for use" with "check if the manifest has expired". Replace "composable fragments" with "optional data sections".
- For Step 3: Rename "Normative artifacts" to "Official spec files". Rename "Fixtures" to "Test examples". Add one-line descriptions of what each artifact IS.
- For the harness/Workbench section: Add one sentence explaining what the harness does before linking to it.

**Key plain-language replacements:**

| Current | Replacement |
|---|---|
| "The manifest is **an envelope**" | "The manifest is **a container**: it has standard header fields and can hold different kinds of data inside." |
| "canonical data elsewhere" | "data stored at its authoritative source" |
| "freshness for use" | "whether the manifest has expired" |
| "composable fragments" | "optional data sections" |
| "Normative artifacts (published)" | "Official spec files" |
| "JSON-LD context artifact" | "JSON-LD vocabulary file (defines what fields mean)" |
| "Structural schema artifact" | "JSON Schema validation file (checks document structure)" |
| "Well-known discovery document" | "Auto-discovery config file (`.well-known` URL, per RFC 8615)" |
| "Fixtures (examples)" | "Test examples (fixtures)" |
| "Interactive harness loader" | "Interactive test tool (loads and displays manifest examples)" |

---

## 4. Denylist for Guard Script

These terms/patterns MUST NOT appear in first-read surfaces (`site/src/content/docs/getting-started/*.md` and `site/src/content/docs/index.md`) **without an accompanying inline definition within 2 lines of first use**.

### 4.1 BANNED outright (remove or replace, never use in first-read pages)

| Pattern | Reason |
|---|---|
| `integration pair` | Completely undefined; no useful inline definition possible |
| `CEO-directed` | Insider organizational framing |
| `convergence profile` | Standards-insider jargon |
| `Metaverse Universal Manifest` or `MUM` (as a defined term) | Insider lineage; irrelevant to adopters |
| `RP1 spatial fabric` (without link to integration page) | Undefined product reference |
| `Lifelike Autonomy` or `LAN` (the project name, not the networking acronym) | Insider project name |

### 4.2 RESTRICTED (must be defined inline on first use, within 2 lines)

| Pattern | Required inline definition |
|---|---|
| `state capsule` | Must immediately explain what "state" means in this context and what "capsule" means |
| `facets` | Must define as "optional named sections within a manifest" |
| `pointers` | Must define as "URL references to data stored at its source" |
| `UMID` | Must expand as "UMID (Universal Manifest Identifier)" on first use |
| `TTL` | Must expand as "TTL (time-to-live)" on first use |
| `envelope` | Must define as "a container/wrapper with standard header fields" |
| `resolver` | Must define as "a service that looks up a manifest by its UMID" |
| `canonical` | Must define as "authoritative" or "the single source of truth" |
| `normative` | Must be replaced with "required by the spec" or defined inline |
| `fixtures` | Must be replaced with "test examples" or defined inline |
| `harness` | Must be replaced with "test tool" or defined inline |
| `local-first` | Must define as "works offline using cached data" |
| `bounded caching` | Must define alongside `local-first` |
| `forward compatibility` | Must define as "older consumers safely ignore newer fields" |
| `composable` | Must define as "mix-and-match; include only what you need" |
| `projections` | Must define as "views of a manifest tailored for a specific context" |
| `freshness for use` | Must be replaced with "whether the manifest has expired" |

### 4.3 Proposed guard script patterns (regex)

```bash
# BANNED patterns -- fail build if found in first-read files
BANNED_PATTERNS=(
  "integration pair"
  "CEO-directed"
  "convergence profile"
  "Metaverse Universal Manifest"
  "\\bMUM\\b"
  "RP1 spatial fabric"
  "Lifelike Autonomy"
  "\\bLAN\\b(?!.*Local Area Network)"
)

# RESTRICTED patterns -- warn if found without definition within 2 lines
RESTRICTED_PATTERNS=(
  "state capsule"
  "\\bfacets\\b"
  "\\bpointers\\b"
  "\\bUMID\\b"
  "\\bTTL\\b"
  "\\benvelope\\b"
  "\\bresolver\\b"
  "\\bcanonical\\b"
  "\\bnormative\\b"
  "\\bfixtures\\b"
  "\\bharness\\b"
  "local-first"
  "bounded caching"
  "forward compatibility"
  "\\bcomposable\\b"
  "\\bprojections?\\b"
  "freshness for use"
)

# First-read surface paths
FIRST_READ_PATHS=(
  "site/src/content/docs/index.md"
  "site/src/content/docs/getting-started/universal-manifest-overview.md"
  "site/src/content/docs/getting-started/concepts.md"
  "site/src/content/docs/getting-started/quick-start.md"
)
```

---

## 5. Additional Findings

### 5.1 Editorial Style Guide reinforces the problem

The editorial style guide at `docs/site/EDITORIAL-STYLE-GUIDE.md` (line 18) lists "portable state capsule" as the "core concept" for overview pages. This means the style guide itself needs updating to either:
- Define "portable state capsule" explicitly within the guide, OR
- Require that any page using the phrase must define it inline on first use.

The Terminology section (lines 52-55) defines only 3 terms: UMID, Resolver, and Standards site. It should be expanded to include ALL restricted terms from section 4.2.

### 5.2 No jargon originates from scripts or templates

Confirmed: no code in `packages/` or `services/` generates any of the problematic terms. All jargon is hand-authored in markdown. The fix is purely editorial.

### 5.3 SVG diagrams contain embedded jargon

`site/public/diagrams/universal-manifest-overview-template.svg` (line 24) contains: "Portable state capsule flow: issue once, resolve by UMID, consume across surfaces." This is text rendered in an SVG image. If the diagram is regenerated, the text should be updated to match the rewritten docs.

### 5.4 The `astro.config.mjs` site description uses jargon

`site/astro.config.mjs` (line 9) contains: `description: 'Portable state capsule standard (spec + conformance + publishing).'` This text may appear in HTML meta tags and search engine results. It should be updated to match the rewritten landing page.

### 5.5 The `spec/v0.1/README.md` uses jargon without definition

Line 5 says: "The Universal Manifest is a portable state capsule: a single document that can be moved between compatible apps/devices to convey identity references..." This is better than the onboarding docs because it at least attempts a colon-expansion, but "state capsule" is still not truly defined.

---

## 6. Summary Statistics

| Metric | Count |
|---|---|
| Total unique jargon terms/phrases identified | 51 |
| CRITICAL severity | 4 |
| HIGH severity | 13 |
| MEDIUM severity | 27 |
| LOW severity | 7 |
| Terms appearing in only 1 user-facing file | 6 (easy fixes) |
| Terms appearing in 5+ user-facing files | 12 (require consistent approach) |
| Banned terms for denylist | 6 patterns |
| Restricted terms for denylist | 17 patterns |
| Files requiring rewrite | 4 primary + editorial style guide + astro config |

---

**End of WO-0039 Phase 1 inventory. This report is complete and ready for the rewrite agent.**
