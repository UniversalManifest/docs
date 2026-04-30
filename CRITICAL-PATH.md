# Universal Manifest — Critical Path

This document captures the minimal execution sequence to make Universal Manifest broadly adoptable and eventually “world-ready”.

“World-ready” is not a vibe. It requires passing the gates in `docs/DONE-DONE-DEFINITION.md` with evidence.

## Current Execution Focus -- Home Cluster Complete; Manual Phase 9; v0.2 Published

Goal: preserve the completed state after the content-first `Home`-cluster wave, keep Phase 9 truthfully manual after the 2026-04-28 revert, and carry the repo from the completed v0.2 publication wave into the next post-publication phase.

Immediate rule:

- the primary public menu should remain limited to `Home` and `Latest Spec`
- the homepage should stay low-noise and plain-language
- the latest spec must remain obviously one click away at `/spec/latest/`
- the homepage should route into a `Home` cluster rather than trying to summarize everything itself
- the explorer should remain use-case-first, with metaverse portaling as the lead lane
- audience landing pages should be separate downstream surfaces, not homepage clutter
- reintegrated reading pages should stay under the shared public shell rather than reviving sprint-era visual fragmentation
- tool and proof entry routes should return under a deliberate shared shell without replacing the calm MVP front door

These rules still hold after v0.2 publication: the home page now has a restrained publication callout, `/spec/latest/` remains obvious, and the durable `/spec/v0.2/` route exists without expanding the calm public menu.

Completed execution sequence:

1. `WO-0196` defined the page architecture and source map for the `Home` cluster.
2. `WO-0197` and `WO-0198` defined the audience-family and explorer schema layers.
3. `WO-0199` and `WO-0200` produced the lead metaverse and EU SSI content packs.
4. `WO-0201` completed the remaining first-rollout audience/use-case content family.
5. `WO-0202` implemented the shared `Home`-cluster tab shell and subordinate routes.
6. `WO-0203` and `WO-0204` implemented the explorer and audience-family public surfaces.
7. `WO-0205` closed the wave with harmonization and publication-readiness verification.

Status: WO-0171 completed the homepage/spec route split. WO-0172 through WO-0174 then established and verified the two-page MVP, WO-0175 extracted the first reusable `UM UI` system, WO-0176 completed the first reader reintegration wave (`/docs/`, `/about/why-um/`, `/about/one-pager/`, `/use-cases/`), WO-0177 completed the first tool/proof reintegration wave (`/learning/`, `/sandbox/`, `/workbench/`), WO-0178 closed the outstanding `/spec/latest/` inline TOC bug, WO-0179 added the canonical full-project/property/surface map, and WO-0180 through WO-0182 established the post-map surface classification and keep/merge/alias/retire strategy. `WO-0183` through `WO-0194` then closed the remaining site-architecture and standards/proof hardening queue. `WO-0195` defined the `Home`-cluster sitemap, domain audit, audience-layer split, and metaverse-first explorer strategy. `WO-0196` through `WO-0205` then delivered the page architecture, audience strategy, explorer schema, content packs, route implementation, and harmonized publication-ready `Home` cluster. `WO-0206` through `WO-0209` completed the first late-April drift-governance follow-up. `WO-0219`, `WO-0241`, and `WO-0242` completed the integration-lane reference, public-route, and dedicated-journey consolidation, bringing the executable proof suite to 27 passing journeys. `WO-0220` executed the operator-gated `spec-v0.2` tag and GitHub release on 2026-04-30, and `WO-0221` through `WO-0226` completed the public spec, discovery, migration, conformance, governance, changelog, home-announcement, and announcement-copy publication surfaces. `WO-0227` and `WO-0228` are obsolete after the 2026-04-28 revert, `WO-0229` closed the authority-doc reconciliation, `WO-0230` defined Phase 19, `WO-0231` closed the v0.2 publication wave with an evidence pack, `WO-0214` is deferred to Phase 19 external-human validation activation, and reverted workflow-era WOs `WO-0210`, `WO-0211`, `WO-0227`, `WO-0228`, `WO-0233`, `WO-0238`, and `WO-0240` are audit-only `OBSOLETE` records that must not be executed.

Current critical path:

1. `WO-0220` through `WO-0226` are complete: the release exists, `/spec/latest/` and `/spec/v0.2/` carry the published posture, machine-readable surfaces declare v0.2 current/stable, and the migration/conformance/governance/announcement paths are linked.
2. `WO-0227` and `WO-0228` are obsolete and must not be executed in their reverted workflow-era form.
3. `WO-0229` is complete: authority docs now reflect the published-v0.2 state.
4. `WO-0230` is complete: Phase 19 is defined with non-conflicting queue stubs starting at `WO-0243`.
5. `WO-0231` is complete: the publication closeout evidence pack is recorded at `docs/reports/2026-04-30-v0-2-publication-evidence-pack.md`.

Cleanup context that affects sequencing:

- The 2026-04-28 revert removed the unauthorized workflow layer, so Phase 9 is currently manual-only.
- `WO-0232`, `WO-0234`, and `WO-0237` remain useful historical records, but their workflow changes are not the live state after the revert.
- Obsolete WOs listed above should not be used as shortcuts for reintroducing automation; any future automation work must be re-scoped cleanly.

## Phase 0 — Define “done” (gates + evidence) -- COMPLETE

- Read: `docs/DONE-DONE-DEFINITION.md`
- Use: `docs/DONE-DONE-CHECKLIST.md`
- Capture: `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`

Status: Done-done framework established and in active use across all phases.

## Phase 1 — Make v0.1 adoptable (minimal contract) -- COMPLETE

Goal: third parties can adopt UM without choosing your identity provider, storage, or framework.

Must-have:

- clear v0.1 contract (required fields + TTL semantics)
- unknown-field tolerance (forward compatibility)
- fixtures: valid + invalid + near-real stubs
- conformance checklist + basic validator tooling

Status: v0.1 contract is adoptable. 32 v0.1 fixtures (valid, invalid, stubs) committed. Conformance checklist and validator tooling shipped.

## Phase 2 — Harden interoperability (v0.2 signature profile) -- COMPLETE

Goal: two independent implementations can sign/verify the same payload the same way.

Must-have:

- signature profile (canonicalization + signing + verification rules)
- signed fixtures and invalid-signature fixtures
- a reference verifier (small, testable, not a framework)

Status: v0.2 signature profile (JCS + Ed25519) is published with 15 fixtures. Ed25519 signature verification confirmed working (WO-0040). Conformance suite expanded with adversarial cases (WO-0048).

## Phase 3 — Publish like a real standard (`universalmanifest.net`) -- COMPLETE

Goal: newcomers can understand and adopt the spec quickly, and the URLs are stable.

Must-have:

- spec/docs site with clear navigation and a first-time reader path
- stable URLs for schema/context artifacts
- versioning + immutability policy

Status: `universalmanifest.net` is live on Cloudflare Pages with stable URLs, adopter-first sidebar navigation, and first-time reader overview.

## Phase 4 — Make UMIDs resolvable (`myum.net/{UMID}`) -- COMPLETE

Goal: a consumer can resolve a manifest by UMID with a deterministic contract (headers, caching, errors, privacy posture).

Must-have:

- resolver endpoint contract + examples
- minimum privacy posture (what is public vs not, and why)
- tests that exercise resolution end-to-end

Status: `myum.net` resolver is live on Cloudflare Workers + KV. J03 reliability hardened (WO-0019). Production smoke passes 9/9 endpoints.

## Phase 5 — Prove it across surfaces (reference implementation + cross-runtime) -- COMPLETE

Goal: demonstrate the spec is not “just for reference implementation” while still letting reference implementation be a primary design driver.

Must-have:

- reference implementation integration recipe
- at least one cross-runtime adopter journey (e.g., profile projection)
- journeys act as proof, not marketing

Status: 27 executable journeys passing. Multiple integration lanes documented with fixture-backed proof, including GPC runtime-signal handling, RP1 fail-closed hardening, data-firewall UX, smart-home, healthcare-consent, and education-credential proof lanes.

## Phase 6 — Full-corpus synthesis before IA and journey expansion -- COMPLETE

Goal: ensure IA, onboarding, and journey planning are derived from the full source corpus with explicit conflict decisions.

Must-have:

- no deferred sources in active corpus batch (all selected sources dispositioned)
- explicit cross-source conflict register with decisions and action targets
- synthesis output that maps source signals into IA/journey/workbench directives
- follow-on implementation WO for corpus-to-artifact execution

Status: Corpus-derived IA/journey/workbench deltas executed and closed (WO-0016, WO-0017).

## Phase 7 — Onboarding clarity + interactive adopter tooling -- COMPLETE

Goal: first-time adopters can understand UM quickly and validate real manifests without writing custom tooling first.

Must-have:

- clear “What is Universal Manifest?” overview for first-contact readers
- visual onboarding diagrams maintained with source assets
- interactive manifest workbench (import, create, validate, export)
- explicit boundaries between reference tooling and normative spec contract

Status: First-time overview shipped. Interactive manifest workbench shipped and verified (WO-0014). Teaching scripts and explainer ecosystem established.

## Phase 8 — Lineage-grounded expansion lanes -- COMPLETE

Goal: scale beyond baseline adoption while preserving origin context and integration boundaries.

Must-have:

- explicit lineage reference to the MUM origin document in source-of-truth docs
- metaverse integration lane documentation
- RP1 spatial-fabric integration lane documentation with source-ingestion plan
- smart-glasses social-layer integration lane documentation with consent-first behavior
- clear rule that normative contract changes still require versioned spec/conformance updates

Status: All integration lanes documented with fixtures and proof journeys (WO-0018 through WO-0024, WO-0027). 13 integration lanes total including OMATrust, proof-of-personhood, DID + VC, education, healthcare, and smart home.

## Phase 9 — Drift governance and closure-regression checks -- ACTIVE (manual-only)

Goal: keep completion claims true over time by running recurring drift and regression checks with explicit WO trigger thresholds.

Cadence and owner:

- weekly drift/governance run by active maintainer or delegated agent
- required before new completion claims or milestone closure statements

Mandatory command set:

1. strict K2B gate validation:
   - `bash ~/.agents/scripts/validate-k2b-gates.sh <repo-root> --artifact-root .dev/ai --strict`
2. journey parity check:
   - `cd packages/universal-manifest && npm run journeys`
3. production route checks:
   - `curl -I https://universalmanifest.net/`
   - `curl -I https://universalmanifest.net/getting-started/workbench/`
   - `curl -I https://universalmanifest.net/proof/harness/`
4. docs link-hygiene scan:
   - `rg -n '/harness/|/proof/|/getting-started/|/spec/|/conformance/|/workbench/|/integrations/' site/src/content/docs --glob '*.md' | rg -v '\\]\\([^)]+'`

Follow-on WO trigger thresholds:

- open a new WO immediately if any mandatory command fails
- open a new WO if status docs contradict active WO status or production reality
- open a new WO if newly ingested corpus signals require IA/spec/proof deltas beyond trivial wording edits

Runbook and current execution posture:

- `WO-0208` documented the recovery/runbook path and briefly added `.github/workflows/phase-9-gate.yml`, but that workflow was removed in revert commit `e493b3e` on 2026-04-28.
- The strict K2B gate (`~/.agents/scripts/validate-k2b-gates.sh ... --strict`) remains a manual maintainer step because its inputs are gitignored `.dev/ai/` artifacts that must not be vendored into the tracked surface. See `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md` section 2.1 for the rationale and the reference restoration procedure (worked example: `WO-0206`).
- Recovery for any mandatory-command failure is procedurally documented in `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md`.
- There is currently no tracked CI or scheduled automation enforcing the non-K2B portion of Phase 9. Treat the full mandatory command set as manual until a fresh WO explicitly reintroduces automation.

Current Phase 9 status:

- `WO-0206` is completed. The strict K2B gate passes against `.dev/ai` with 41 pass, 0 warn, 0 fail, and the rest of the mandatory command set passed on 2026-04-24.
- `WO-0207` through `WO-0209` are completed.
- `WO-0208` now stands as a historical runbook/automation attempt rather than live workflow state.
- `WO-0210` and `WO-0211` are obsolete because the workflow they extended no longer exists after the 2026-04-28 revert.
- Before the 2026-04-30 v0.2 publication, Phase 9 was verified-clean in its manual posture: publication readiness was GO, `WO-0220` rechecked immutable artifact hashes before release execution, and no reverted workflow automation was treated as live.

## Phase 10 — Interactive Sandbox (WO-0060-0068) -- COMPLETED, HIGHEST PRIORITY

Per CEO mandate ([`docs/MANDATE-interactive-implementation-sandbox.md`](MANDATE-interactive-implementation-sandbox.md)), this phase superseded all other execution priorities.

Goal: provide a hands-on interactive sandbox where adopters can explore real manifests, see validation in action, and understand the spec through guided scenarios.

Delivered:

- sandbox foundation with browser-based Ed25519 validator (54/54 parity with Node)
- three-panel layout (entity | consumer | protocol) with step engine
- scenario modal with card grid, search, filters, and keyboard navigation
- 25 interactive scenarios across 5 categories:
  - Getting Started (GS-01 through GS-04): first-time user onboarding
  - Trust and Verification (TV-01 through TV-05): real Ed25519, tamper detection
  - Integration Lanes (IL-01 through IL-08): social, smart glasses, metaverse, spatial, and more
  - Edge Cases (EC-01 through EC-04): failure mode demonstrations
  - Advanced (AD-01 through AD-04): cross-system projection, revocation, full v0.2
- 25 SVG illustrations (self-contained, accessible, dark theme)
- CI parity testing (54/54) and scenario smoke testing (183/183)

Status: All 9 work orders (WO-0060 through WO-0068) completed and verified.

## Phase 11 — Sandbox V2 Redesign (WO-0069-0080) -- COMPLETED

Goal: redesign the sandbox UI with a two-entity interaction model, hierarchy explorer, protocol lens, and enhanced visual design.

Delivered:

- HierarchyExplorer: reusable collapsible JSON tree-view (WO-0069)
- DetailsCard: dual-mode hierarchy/JSON toggle (WO-0070)
- SessionStateIndicator + V2 types (WO-0071)
- EntityColumn: symmetrical entity panel (WO-0072)
- ProtocolLens: step-by-step interaction viewer (WO-0073)
- SubjectPanel: exchanged object display (WO-0074)
- SandboxLayoutV2: new CSS Grid layout (WO-0075)
- SandboxEngineV2: two-entity state management (WO-0076)
- Scenario detail page rewrite (WO-0077)
- Getting Started scenario migration (WO-0078)
- Remaining scenario migration: TV, IL, EC, AD (WO-0079)
- Responsive polish, animations, accessibility audit (WO-0080)

Status: All 12 work orders completed. Build and browser verification completed, and the redesign is live on production routes.

## Phase 12 — External Adopter Verification Wave (WO-0053-0059) -- COMPLETED

Goal: enable third-party adoption by providing standalone conformance tools, reference implementations, onboarding materials, and clear spec-vs-implementation boundaries. Blocks Gates G4 and G6.

Must-have:

- standalone conformance test suite (WO-0053, CRITICAL, blocks Gate G4)
- reference implementation repository (WO-0054, CRITICAL, blocks Gate G4)
- adopter onboarding document package (WO-0055, CRITICAL, blocks Gate G4)
- adopter feedback loop and contract system (WO-0056, HIGH, blocks Gate G4 + G6)
- spec-vs-implementation documentation clarity (WO-0057, HIGH, blocks Gate G4)
- v0.1-to-v0.2 migration guide (WO-0058, HIGH, blocks Gate G6)
- governance completion: breaking-change, deprecation, incident policies (WO-0059, CRITICAL, blocks Gate G6 + World-ready)

Status: Completed. WO-0053 through WO-0059 were delivered and verified with evidence on 2026-03-02, including standalone conformance tooling, reference implementation publication, adopter onboarding package, migration guide, and governance completion.

## Phase 13 — Teaching Scripts and Visual Identity System -- IN_PROGRESS

Goal: create a comprehensive teaching and communication ecosystem with staged explanation scripts and a consistent visual identity.

Delivered so far:

- teaching scripts system with staged explanations for 30-second, 3-minute, and 15-minute audiences ([`docs/teaching-scripts/`](teaching-scripts/))
- Capsule-Pod iconic representation approved as the UM visual identity ([`docs/teaching-scripts/01-ICONIC-REPRESENTATION.md`](teaching-scripts/01-ICONIC-REPRESENTATION.md))
- 20 script ideas defined ([`docs/teaching-scripts/03-SCRIPT-IDEAS.md`](teaching-scripts/03-SCRIPT-IDEAS.md))
- 5 explainer documents at various depth levels ([`docs/explainers/`](explainers/))
- 4 animation scripts ([`docs/scripts/`](scripts/))
- 29 production animated SVGs plus 2 pilot files on universalmanifest.net

Status: Stage 3 (script ideas and visual identity established). Ongoing refinement.

## Phase 14 — Code Examples Ecosystem -- COMPLETE

Goal: provide runnable code examples and a demo application so adopters can learn by doing.

Delivered:

- 12 runnable code examples covering hello-world, validation, signing, facets, resolution, projection, device registration, consent enforcement, unknown-field tolerance, and multi-manifest aggregation ([`examples/code/`](../examples/code/))
- browser-based and Python validation examples ([`examples/code/browser-validate/`](../examples/code/browser-validate/), [`examples/code/python-validate/`](../examples/code/python-validate/))
- full demo application with server and library ([`examples/demo-app/`](../examples/demo-app/))

Status: Completed (WO-0044).

## Phase 15 — Portable Identity Profile + Metaverse Go-Now Program Execution -- COMPLETE

Goal: close both immediate execution tracks with adopter-ready guidance, synchronized evidence, and publication-ready docs/site updates without changing UM normative contract boundaries.

Delivered:

- Portable Identity Profile Go-Now completion (`PIP-GN-01` through `PIP-GN-06`):
  - integration lane + site mirror,
  - fixture and journey evidence packs,
  - registry key-family expansion,
  - implementation-path guide and site publication,
  - governance synchronization updates.
- Metaverse Universal Manifest Go-Now completion (`MUM-GN-01` through `MUM-GN-06`):
  - integration hardening and scenario coverage,
  - registry + fixtures + journey suite evidence,
  - synchronization-profile guide and site publication,
  - governance synchronization updates.

Primary evidence:

- `docs/workorders/WO-0125-portable-identity-profile-go-now-execution-and-integration-pages.md`
- `docs/workorders/WO-0126-metaverse-universal-manifest-go-now-execution-and-integration-pages.md`
- `docs/reports/2026-03-05-portable-identity-profile-comprehensive-human-review-report.md`
- `docs/reports/2026-03-05-metaverse-universal-manifest-comprehensive-human-review-report.md`
- `docs/reports/2026-03-05-gn06-conformance-npm-test.txt`
- `docs/reports/2026-03-05-gn06-journeys-run.txt`
- `docs/reports/2026-03-05-gn06-site-build-clean.txt`

Status: Completed (WO-0125, WO-0126). Next path is Research-First execution (`PIP-RS-*`, `MUM-RS-*`) under existing promotion gates.

## Phase 16 — Privacy Signal Standards Alignment (GPC) -- COMPLETE

Goal: execute the GPC integration direction from standards review into reference proof without expanding the core UM contract prematurely.

Delivered:

- standards review and overlap/gap analysis closure (`WO-0127`)
- published GPC integration lane docs for repo + site
- runtime normalization helpers for `Sec-GPC` and `navigator.globalPrivacyControl`
- `/.well-known/gpc.json` support-resource parsing helpers
- optional UM evidence projection helpers for consent/pointer representation
- dedicated GPC fixture pack under `examples/integrations/gpc/`
- GPC evidence-projection manifest fixture
- `J21` executable journey proof for runtime-authoritative behavior and scope-limited supersession

Primary evidence:

- `docs/workorders/WO-0127-gpc-standards-integration-review-and-gap-analysis.md`
- `docs/workorders/WO-0128-gpc-go-now-runtime-mapping-fixtures-and-proof.md`
- `integrations/gpc-global-privacy-control.md`
- `packages/universal-manifest/src/index.ts`
- `docs/reports/2026-03-06-gpc-go-now-npm-test.txt`
- `docs/reports/2026-03-06-gpc-go-now-journeys.txt`
- `docs/journeys/_artifacts/2026-03-06T07-50-34-715Z-journey-report.json`

Status: Completed (WO-0127, WO-0128). Next path is broader privacy-signal research/promotion work only if explicitly approved.

## Phase 17 — Localized Source Follow-on and Research-First Promotion Gates -- COMPLETED

Goal: convert the newly localized architecture corpus into durable integration guidance where the path is already clear, and into explicit Research-First decision packages where protocol or runtime selection would otherwise be premature.

Delivered:

- composite-stack and active-runtime architecture clarification (`WO-0130`)
- DID + VC and metaverse lane refresh with stronger volatility and non-lock-in boundaries (`WO-0131`)
- Research-First decision package for protocol volatility, proximity credentials, and federation/bridge strategy (`WO-0132`)
- protocol recommendation governance and standards-currency matrix (`WO-0133`)
- proximity credential boundary assessment (`WO-0134`)
- federation and bridge strategy decision package (`WO-0135`)
- OMB/wiki spatial-fabric source crosscheck (`WO-0136`)
- role-based runtime and synchronization guidance refresh (`WO-0137`)
- RP1/MSF primary-source refresh and integration-depth pass (`WO-0138`)

Primary evidence:

- `docs/workorders/WO-0130-composite-architecture-and-active-runtime-alignment.md`
- `docs/workorders/WO-0131-did-vc-and-metaverse-lane-refresh-from-localized-corpus.md`
- `docs/workorders/WO-0132-research-first-protocol-volatility-proximity-and-federation-gaps.md`
- `docs/workorders/WO-0133-protocol-recommendation-governance-and-standards-currency-matrix.md`
- `docs/workorders/WO-0134-proximity-credential-and-presentation-profile-assessment.md`
- `docs/workorders/WO-0135-federation-and-bridge-strategy-decision-package.md`
- `docs/workorders/WO-0136-omb-wiki-spatial-fabric-source-refresh-and-primary-source-crosscheck.md`
- `docs/workorders/WO-0137-role-based-runtime-federation-and-bridge-guidance-refresh.md`
- `docs/workorders/WO-0138-rp1-msf-primary-source-refresh-and-integration-depth-pass.md`
- `docs/reports/2026-03-06-protocol-volatility-proximity-and-federation-research-first-decision-package.md`
- `docs/reports/2026-03-06-protocol-recommendation-governance-and-standards-currency-matrix.md`
- `docs/reports/2026-03-06-proximity-credential-and-presentation-profile-assessment.md`
- `docs/reports/2026-03-06-federation-and-bridge-strategy-decision-package.md`
- `docs/reports/2026-03-06-omb-wiki-spatial-fabric-crosscheck.md`
- `docs/reports/2026-03-06-rp1-msf-primary-source-refresh-and-integration-depth-pass.md`

Status: Completed. The earlier follow-on queue named here (WO-0142, WO-0143, WO-0145) has since been closed in the formal work-order files; stale status summaries should not be treated as an active queue.

## Phase 18 — RP1/MSF Adversarial Hardening -- COMPLETED

Goal: prove fail-closed behavior for stale attachment routing evidence and expired or revoked session-context pointers without expanding the UM core contract.

Delivered:

- positive-path RP1 fixture strengthened with attachment/session freshness metadata
- adversarial RP1 fixtures for stale attachment traversal and revoked session-context replay
- `J22` executable journey proof for fail-closed RP1/MSF behavior
- RP1 integration repo/site pages refreshed with explicit freshness/revocation guidance
- RP1 sandbox narratives refreshed to reflect attachment freshness and session-context safety
- governance/state synchronization and decision records for the hardening model

Primary evidence:

- `docs/workorders/WO-0139-rp1-msf-adversarial-attachment-and-session-hardening.md`
- `docs/reports/2026-03-06-rp1-msf-adversarial-attachment-and-session-hardening.md`
- `examples/v0.1/stubs/rp1-spatial-fabric-stale-attachment-manifest.jsonld`
- `examples/v0.1/stubs/rp1-spatial-fabric-revoked-session-manifest.jsonld`
- `docs/journeys/J22-rp1-attachment-freshness-and-session-safety.md`
- `docs/journeys/_artifacts/2026-03-06T18-57-58-721Z-journey-report.json`

Status: Completed. The earlier follow-on work orders referenced here (WO-0142, WO-0143, WO-0145) have since been completed; this section is retained for historical sequencing, not as an active execution queue.

## Phase 19 — Post-publication adopter feedback and v0.3 input -- DEFINED

Goal: use the published v0.2 surface as the stable baseline for adopter feedback, publication closeout evidence, and the next round of spec-input triage.

Queue ID reconciliation:

- `WO-0230` originally said to start Phase 19 follow-on IDs at `WO-0232`, but `WO-0232` through `WO-0242` already exist in the repository.
- Phase 19 queue-definition stubs therefore start at the next available range, `WO-0243+`.
- These are queue stubs only. Full WO files should be drafted later if/when each item is accepted for execution.

Deferred item catalog from the 2026-04-24 publication-readiness scan:

1. Tier 2 assurance / cryptographic binding: public deferral for v0.3+.
2. Tier 3 assurance / multi-party ceremony: public deferral for v0.4+.
3. Data Integrity / RDF profile: `spec/v0.2/SIGNATURE-PROFILE.md` section 8 says this is future, not v0.2.
4. Additional integrity profiles beyond JCS + Ed25519: deferred by the WO-0190 decision closure and the v0.2 signature profile.
5. Revocation as a normative requirement: currently optional/extension-lane behavior, not a v0.2 baseline requirement.
6. Encrypted inline facets: guidance-only optional privacy path, not a required v0.2 profile.
7. Broader cross-DID binding tiers: research/future scope beyond the v0.2 Tier 1 baseline.

Phase 19 goal queue:

- `WO-0243` — Post-publication external-human reader validation activation (P2): promote the existing `WO-0214` plan now that v0.2 is published, assemble the cohort, and produce the external-reader evidence pack if candidates are available.
- `WO-0244` — Adopter-feedback loop activation against published v0.2 (P1): reactivate the `WO-0056` feedback/SLA/spec-improvement machinery against the published spec, migration guide, conformance suite, and implementation guidance.
- `WO-0245` — Tier 2 cryptographic identity-binding research package (P2): evaluate whether cryptographic binding is mature enough for a v0.3 candidate profile, with explicit promotion/permanent-deferral criteria.
- `WO-0246` — Tier 3 multi-party ceremony research package (P3): define what evidence would be required before multi-party ceremony support can move from future signal to spec candidate.
- `WO-0247` — Data Integrity / RDF profile decision package (P2): assess whether RDF graph-signing semantics are needed beyond the current JCS + Ed25519 interoperability baseline.
- `WO-0248` — Additional integrity-profile registry decision package (P3): decide whether post-quantum, alternate-canonicalization, or multi-proof profile discovery belongs in the next spec cycle or remains deferred.
- `WO-0249` — Revocation-as-normative decision package (P2): determine whether `statusRef` / `revocationCursor` behavior should stay optional or become a conformance requirement in a future version.
- `WO-0250` — Encrypted inline facet promotion decision (P3): decide whether encrypted inline facets remain guidance-only or need fixtures, lifecycle conformance, and normative text.
- `WO-0251` — Broader cross-DID binding tier scope decision (P3): evaluate cross-DID binding growth beyond the v0.2 Tier 1 baseline and align it with the Tier 2/Tier 3 research track.

Phase 19 operating rules:

- Use `docs/governance/SPEC-IMPROVEMENT-QUEUE.md` as the adopter-feedback routing surface before changing normative spec text.
- Convert concrete post-publication feedback into scoped WOs, RFCs, or permanent-deferral decisions; do not reopen the v0.2 publication wave broadly.
- Treat identity binding, RDF/Data Integrity profiles, revocation, encrypted inline facets, and cross-DID binding as v0.3+ inputs unless an explicit decision package promotes them.
- Keep `/spec/latest/` obvious and keep the public menu calm while post-publication learning accumulates.

Status: Defined by `WO-0230`; residual follow-ons are listed in the v0.2 publication evidence pack produced by `WO-0231`.
