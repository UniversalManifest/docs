# 2026-04-22 Compatibility Surface Retirement Readiness

## Purpose

This report closes `WO-0188` by defining when compatibility-only routes, deploy layers, and asset aliases are ready to retire.

The objective is not immediate removal. The objective is to make retirement deliberate: every compatibility surface should have a clear current posture, explicit evidence requirements before removal, and a safe sequence for retirement.

## Readiness Rules

A compatibility surface is only retirement-ready when all of the following are true:

1. The canonical replacement surface is already stable and verified.
2. Current authored docs and navigation no longer point at the compatibility surface.
3. Remaining references are understood: either archival, external, or intentionally retained for continuity.
4. The retirement action is explicit:
   - remove entirely
   - replace with redirect-only behavior
   - keep as compatibility infrastructure for now
5. Post-change verification is defined in advance:
   - route checks
   - build verification
   - redirect verification where applicable

## Retirement-Readiness Matrix

| Compatibility surface | Canonical target or replacement | Current posture | Required evidence before retirement | Sequencing note |
| --- | --- | --- | --- | --- |
| `/ns/universal-manifest/latest/*` redirects in `deploy/universalmanifest.net/_redirects` | versioned namespace artifacts under `/ns/universal-manifest/v0.1/*` and later versioned releases | `redirect-only` | explicit versioning-policy change, audit of docs/tool consumers that still rely on `latest`, redirect smoke verification after any replacement | keep until versioned publication policy changes; not an early retirement candidate |
| sandbox shortcut redirects in `deploy/universalmanifest.net/_redirects` | canonical scenario routes under `/sandbox/.../` | `redirect-only` | scenario slugs remain stable, no meaningful published dependency on shortcuts, redirect checks preserved until removal | low-risk retirement candidate after route inventory review |
| `/workbench/index/` and `/workbench/index.html` | `/workbench/` with raw payload retained under `/workbench/app/` | `retire-candidate` | no remaining intentional authored links, canonical `/workbench/` remains stable, browser verification confirms `/workbench/` fully covers the old entry use | earliest route-level retirement candidate |
| `deploy/localartist.network/` compatibility deployment | canonical namespace/property hosting on `universalmanifest.net` | `keep` | early v0.1 references and fixture/report dependencies are inventoried and intentionally retired or redirected, legacy namespace continuity is proven elsewhere, explicit deprecation plan exists | highest-risk and latest retirement candidate |
| `/resolver/ops/` and `/resolver/result/` plus associated legacy static payloads | `/resolver/` and resolver reference/docs surfaces | `keep` | canonical resolver entry absorbs current workflows, resolver docs stop depending on auxiliary pages, browser verification confirms no operational regression after simplification | do not retire until resolver UX is intentionally simplified |
| `/diagrams/universal-manifest-overview-template.svg` | `/diagrams/universal-manifest-system-overview.svg` | `retire-candidate` | current authored docs already use the canonical path, external/shared references to the template alias are reviewed, compatibility need falls low enough to remove safely | asset-alias cleanup after route/deploy retirement work, not before |
| `/animations/scenario-01-um-object-model.svg` | `/animations/scenario-01-object-model.svg` | `retire-candidate` | no remaining intentional docs references, external dependency check for previously shared links, verifier remains green after any alias change | pair with later asset-alias cleanup, after higher-value route decisions are settled |

## Surfaces Explicitly Not Targeted For Retirement By This WO

These are preserved because they are subordinate payloads or active canonical surfaces, not compatibility-only retirement targets:

- `site/public/workbench/app/index.html`
- `site/public/resolver/app/index.html`
- `site/public/tools/concept-explorer/app/index.html`
- canonical tool/proof entry routes created under the shared shell strategy

## Evidence Used For This Readiness Pass

Reviewed inputs:

- `docs/CANONICAL-ROUTE-AND-COMPATIBILITY-ALIAS-POLICY.md`
- `docs/reports/2026-04-13-post-wo-0179-surface-disposition-and-unification-strategy.md`
- `deploy/localartist.network/README.md`
- `deploy/localartist.network/_redirects`
- `deploy/universalmanifest.net/README.md`
- `deploy/universalmanifest.net/_redirects`

Observed compatibility signals that justify caution:

- `deploy/localartist.network/README.md` still explicitly exists to preserve early v0.1 namespace continuity.
- `deploy/universalmanifest.net/_redirects` still intentionally publishes `latest` namespace redirects and sandbox shortcut redirects.
- `site/src/pages/resolver/index.astro` still actively links to `/resolver/ops/`.
- repository search still finds `localartist.network` references in journey artifacts, fixtures, and historical materials, which makes premature retirement of `deploy/localartist.network/` inappropriate.

## Safe Retirement Sequence

1. Retain canonical routes and current compatibility layers exactly as they are until evidence is collected.
2. Start with the lowest-risk alias-only entry surfaces:
   - `/workbench/index/`
   - `/workbench/index.html`
3. Review sandbox shortcut redirects next, because they are redirect-only and easy to verify.
4. Review asset-alias retirement later, after the public route/deploy cleanup sequence is stable.
5. Leave `deploy/localartist.network/` for last, because its compatibility risk is materially higher than the route and asset alias cases.
6. Treat resolver auxiliary pages as a separate UX simplification decision, not as an opportunistic deletion.

## Outcome

`WO-0188` is now complete.

The project now has:

- explicit exit criteria for compatibility-only surfaces
- a readiness matrix instead of indefinite compatibility retention
- a clear retirement order that starts with the lowest-risk alias routes and ends with the highest-risk legacy deploy infrastructure

That is enough to move the active queue forward from the site-architecture convergence lane into the next standards/proof batch.
