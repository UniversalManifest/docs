# WO-0112 — myum Consumer Frontend + Runtime Reality Audit (Live vs Stub/Mock)

**Status:** COMPLETED
**Created:** 2026-03-02
**Updated:** 2026-03-02
**Priority:** P0 (Critical)
**Source:** Direct owner request (2026-03-02) after myum implementation audit
**Tags:** [resolver], [frontend], [site], [audit], [adoption]
**Blocks:** External adopter confidence, senior-team architecture decisions, friendly consumer-facing myum UX
**Dependencies:**
- WO-0098 (resolver API reference page; completed)
- Existing audit baseline: `.dev/ai/reports/2026-03-02-myum-domain-implementation-audit.md`
**Estimated effort:** 2-3 days (design + implementation + verification + report pack)

## Progress update (2026-03-02)

Completed this pass:

- Comprehensive WO-grade report created:
  - `.dev/ai/reports/2026-03-02-wo-0112-runtime-reality-report.md`
- Resolver consumer frontend and route-entry enhancements implemented:
  - `site/public/resolver/index.html`
  - `site/public/resolver/result.html`
  - `site/public/resolver/ops.html`
  - `site/src/pages/resolver/index.astro`
  - `site/src/pages/resolver/result.astro`
  - `site/src/pages/resolver/ops.astro`
- Docs/examples alignment updates implemented:
  - `site/src/content/docs/index.md`
  - `site/src/content/docs/reference/resolver-api.md`
  - `site/src/content/docs/publishing/production-smoke.md`
  - `examples/code/05-resolve-from-myum/README.md`
  - `examples/code/05-resolve-from-myum/fetch-by-umid.mjs`
- Verification evidence captured:
  - `.dev/ai/reports/2026-03-02-wo-0112-resolver-index-home.png`
  - `.dev/ai/reports/2026-03-02-wo-0112-resolver-result-404.png`
  - `.dev/ai/reports/2026-03-02-wo-0112-resolver-ops.png`
  - `.dev/ai/reports/2026-03-02-wo-0112-resolver-route-home.png`
  - `.dev/ai/reports/2026-03-02-wo-0112-resolver-route-result.png`
  - `.dev/ai/reports/2026-03-02-wo-0112-resolver-route-ops.png`

Deployment alignment completion:

- Docs artifact deployed to Cloudflare Pages project `universalmanifest-net` on 2026-03-02.
- Production route verification now passes:
  - `https://universalmanifest.net/sandbox/` -> `200`
  - `https://universalmanifest.net/resolver/` -> `200`
  - `https://universalmanifest.net/resolver/ops` -> `200`
  - `https://universalmanifest.net/reference/resolver-api/` -> `200`
- Production endpoint smoke now passes:
  - `cd packages/universal-manifest && node scripts/smoke-endpoints.mjs --mode prod --docs-base https://universalmanifest.net --resolver-base https://myum.net`
- Post-deploy verification report:
  - `.dev/ai/reports/deploy-checks/2026-03-02T21-54-52-324Z-post-deploy-verification.md`

## Objective

Deliver a complete, senior-team-grade execution package for `myum.net` composed of:

1. A **full comprehensive runtime reality report** that quantifies exactly what is:
   - real live production code and behavior,
   - skeleton/minimal implementation,
   - simulated/stub/mock tooling and UX surfaces,
   - drift between source, docs, and deployed runtime.

2. A **friendly consumer frontend** for resolver usage, with exact implementation specs and detailed page wireframes, so non-expert adopters can resolve a UMID and receive a clear trust/use verdict.

3. **Alignment and hardening updates** that ensure UI, docs, and examples reflect the real resolver contract and production behavior.

## Why this work matters

Current state has strong primitives but uneven external clarity:

- Resolver is live and functional (`myum.net`), but positioned/documented as a skeleton/minimal profile in multiple places.
- Some consumer-facing learning surfaces are simulated or stale relative to runtime behavior.
- Senior engineers need a single granular truth source for planning, and adopters need a direct, friendly UI to consume resolver output safely.

Without this work, teams will continue spending integration cycles on mismatch reconciliation instead of implementation.

## In-scope deliverables

### Deliverable A — Senior-Team Comprehensive Report (Granular)

Create and/or update a report in:

- `.dev/ai/reports/`

Required report sections:

1. **Endpoint behavior matrix (production-observed)**
   - `GET/HEAD/OPTIONS/POST` behavior by route:
     - `/health`
     - `/.well-known/myum-resolver.json`
     - `/{UMID_PATH}`
   - `200/304/307/400/404/405/410/500` mapping.

2. **Code-path provenance map**
   - Exact files/line references for each behavior (parse, KV, redirect, revoked, etag, CORS).

3. **Stub/mock/simulated inventory**
   - Hardcoded fixture behavior.
   - Simulated sandbox flows.
   - Simulation-first examples.
   - Any non-runtime demos.

4. **Live working inventory**
   - Real production endpoints and verifications.
   - Local E2E scripts proving branch coverage.

5. **Drift findings**
   - Source vs production drift.
   - Docs vs implementation drift.
   - Example semantics drift.

6. **Risk and impact analysis**
   - Security/contract/adopter risks.
   - Severity and remediation priority.

7. **Action plan with owner-ready phases**
   - Phase 0/1/2 tasks with acceptance criteria and verification commands.

### Deliverable B — Consumer Frontend (Friendly Resolver UI)

Implement a dedicated consumer-facing resolver frontend under:

- `site/public/resolver/` (or equivalent Astro route if preferred)

Must include:

1. **UMID lookup surface** (simple entry + advanced controls)
2. **Resolution result view** with clear trust verdict
3. **Explicit data provenance labels** (`Live resolver response` vs `Simulated/example`)
4. **TTL and freshness interpretation** (safe-to-use vs expired)
5. **Redirect handling view** (`307` path visibility)
6. **Developer details drawer** (headers, raw JSON, ETag, timings)
7. **Error state UX** for `400/404/405/410/500`

### Deliverable C — Alignment updates

1. Align examples/docs to current resolver path semantics.
2. Align UI copy so simulated flows cannot be mistaken for live runtime calls.
3. Ensure resolver contract examples and consumer page behavior match deployed contract expectations.

## Out of scope

- Building a full write/registration API for resolver ingestion.
- Private/authenticated resolver profile.
- New cryptographic profiles beyond current v0.2 contract.

## Page inventory and exact wireframes

Below are implementation wireframes intended to be translated directly into code. They define structure, key copy blocks, and component-level layout.

---

## Page 1 — Resolver Home (`/resolver/`)

### Purpose

Primary user entry point: resolve UMID and receive actionable trust result.

### Layout spec

- Header bar:
  - Left: `Universal Manifest Resolver`
  - Right: links `API`, `Conformance`, `Raw Harness`
- Hero panel:
  - Title: `Resolve a UMID`
  - Subtitle: `Fetch manifest -> validate structure -> verify freshness -> decide safe use`
- Resolve card:
  - Input `UMID`
  - Optional toggle: `Use b64u path`
  - Base URL selector (`https://myum.net` default)
  - Button `Resolve Now`
- Quick examples strip:
  - Known fixture UMID
  - Example b64u token
- Trust primer panel:
  - Explain `HTTP success != safe-to-use`
  - Explain `expiresAt` enforcement

### HTML wireframe

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Resolver | Universal Manifest</title>
  </head>
  <body class="rm-page rm-page--home">
    <header class="rm-topbar">
      <div class="rm-topbar__brand">Universal Manifest Resolver</div>
      <nav class="rm-topbar__nav">
        <a href="/reference/resolver-api/">API</a>
        <a href="/conformance/resolver/">Conformance</a>
        <a href="/harness/index.html">Raw Harness</a>
      </nav>
    </header>

    <main class="rm-main">
      <section class="rm-hero">
        <h1>Resolve a UMID</h1>
        <p>
          Fetch manifest, verify structure, enforce freshness, then decide if payload is safe to use.
        </p>
      </section>

      <section class="rm-card rm-card--resolve">
        <h2>Lookup</h2>
        <label for="umid">UMID</label>
        <input id="umid" type="text" value="urn:uuid:11111111-1111-4111-8111-111111111111" />

        <div class="rm-row">
          <label for="base">Resolver Base</label>
          <select id="base">
            <option>https://myum.net</option>
            <option>https://www.myum.net</option>
            <option>http://127.0.0.1:8787</option>
          </select>
        </div>

        <div class="rm-row">
          <label>
            <input id="use-b64u" type="checkbox" />
            Resolve using b64u escape hatch
          </label>
        </div>

        <button id="resolve">Resolve Now</button>
      </section>

      <section class="rm-card rm-card--examples">
        <h3>Quick examples</h3>
        <button data-example="fixture">Use fixture UMID</button>
        <button data-example="b64u">Use fixture UMID (b64u)</button>
      </section>

      <section class="rm-card rm-card--trust-primer">
        <h3>Trust primer</h3>
        <ul>
          <li>HTTP 200 only means transport success.</li>
          <li>Consumers MUST enforce <code>expiresAt</code> before use.</li>
          <li>If signature exists (v0.2), verify before trust.</li>
        </ul>
      </section>
    </main>
  </body>
</html>
```

---

## Page 2 — Resolution Result (`/resolver/result`)

### Purpose

Show complete outcome for a specific resolve action, with a top-level consumer verdict.

### Layout spec

- Sticky verdict banner (top):
  - `SAFE TO USE` | `DO NOT USE` | `MANUAL REVIEW`
- Split content:
  - Left: Manifest summary + trust checks
  - Right: Developer diagnostics
- Tabs:
  - `Summary`
  - `Manifest`
  - `Headers`
  - `Trace`
- Footer actions:
  - `Copy cURL`
  - `Open raw JSON`
  - `Resolve another`

### Trust checks panel

Required check rows:

- Structural validation
- TTL freshness (`expiresAt` vs now)
- Signature validation (if `manifestVersion=0.2` and signature present)
- Redirect status handling
- Contract header presence (`x-um-resolver-contract`)

### HTML wireframe

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Resolver Result | Universal Manifest</title>
  </head>
  <body class="rm-page rm-page--result">
    <header class="rm-topbar">
      <a href="/resolver/" class="rm-back">← Resolver</a>
      <div class="rm-verdict rm-verdict--fail">DO NOT USE: Manifest expired</div>
    </header>

    <main class="rm-main rm-main--result-grid">
      <section class="rm-column rm-column--primary">
        <article class="rm-card rm-card--summary">
          <h1>Resolution Summary</h1>
          <p>UMID: <code>urn:uuid:11111111-1111-4111-8111-111111111111</code></p>
          <p>Status: <strong>200 OK</strong></p>
          <p>Resolved from: <strong>Live resolver response</strong></p>
        </article>

        <article class="rm-card rm-card--checks">
          <h2>Trust Checks</h2>
          <ul class="rm-checklist">
            <li class="pass">Structure: PASS</li>
            <li class="fail">Freshness: FAIL (expired)</li>
            <li class="pass">Signature: PASS</li>
            <li class="pass">Contract header: PASS</li>
            <li class="pass">Caching semantics: PASS</li>
          </ul>
        </article>

        <article class="rm-card rm-card--manifest-preview">
          <h2>Manifest Preview</h2>
          <pre>{ "@id": "...", "subject": "..." }</pre>
        </article>
      </section>

      <aside class="rm-column rm-column--diagnostics">
        <article class="rm-card rm-card--diag">
          <h2>Diagnostics</h2>
          <p>Request URL: <code>https://myum.net/urn%3Auuid%3A...</code></p>
          <p>Latency: <code>84ms</code></p>
          <p>ETag: <code>W/"sha256-..."</code></p>
          <p>Cache-Control: <code>public, max-age=60</code></p>
          <p>X-UM-Resolver-Contract: <code>myum-resolver/v0.1</code></p>
        </article>

        <article class="rm-card rm-card--actions">
          <button>Copy cURL</button>
          <button>Open Raw JSON</button>
          <a href="/resolver/">Resolve another UMID</a>
        </article>
      </aside>
    </main>
  </body>
</html>
```

---

## Page 3 — Redirect Result (`/resolver/result` with `307`)

### Purpose

Make redirect outcomes explicit, safe, and understandable.

### Layout spec

- Banner: `REDIRECTED`
- Show `Location` target prominently.
- Two-path flow:
  - `Stop at redirect` (strict resolver behavior only)
  - `Follow redirect and evaluate target payload`

### HTML wireframe

```html
<section class="rm-card rm-card--redirect">
  <h2>Resolver returned 307 Temporary Redirect</h2>
  <p>Location target:</p>
  <p><code>https://example.com/manifests/urn%3Auuid%3A...</code></p>

  <div class="rm-row">
    <button id="stop">Keep redirect result only</button>
    <button id="follow">Follow redirect and evaluate payload</button>
  </div>

  <p class="rm-note">
    Note: redirect transport success does not imply payload trust.
    If followed, run full structure + TTL + signature checks.
  </p>
</section>
```

---

## Page 4 — Error States (`/resolver/result` failure variants)

### Purpose

Deliver precise, non-ambiguous failure messaging by status class.

### Required state cards

- `400 bad_request` (invalid UMID encoding)
- `404 not_found` (unknown UMID)
- `405 method_not_allowed`
- `410 revoked`
- `500 internal/corrupt record`

### HTML wireframe

```html
<section class="rm-card rm-card--error rm-card--error-404">
  <h2>404 Not Found</h2>
  <p>No record exists for this UMID in the resolver.</p>
  <pre>{ "error": "not_found", "umid": "..." }</pre>
  <div class="rm-row">
    <button>Try another UMID</button>
    <button>Copy request details</button>
  </div>
</section>
```

---

## Page 5 — Contract + Health Explorer (`/resolver/ops`)

### Purpose

Give senior engineers and integrators a quick operational pane.

### Layout spec

- Contract metadata section from `/.well-known/myum-resolver.json`
- Health snapshot (`/health`)
- Header compliance checks for latest resolve
- Optional method probes (read-only warning)

### HTML wireframe

```html
<!doctype html>
<html lang="en">
  <head><meta charset="utf-8" /><title>Resolver Ops | Universal Manifest</title></head>
  <body class="rm-page rm-page--ops">
    <main class="rm-main">
      <section class="rm-card">
        <h1>Resolver Ops Snapshot</h1>
        <p>Health: <strong>OK</strong></p>
        <p>Contract: <code>myum-resolver/v0.1</code></p>
      </section>

      <section class="rm-card">
        <h2>Well-known Contract</h2>
        <pre>{ "contract": "...", "kv": { "keyPattern": "um:{UMID}" } }</pre>
      </section>

      <section class="rm-card">
        <h2>Header Compliance</h2>
        <ul>
          <li>etag: present</li>
          <li>cache-control: present</li>
          <li>x-um-resolver-contract: present</li>
          <li>access-control-expose-headers: present</li>
        </ul>
      </section>
    </main>
  </body>
</html>
```

## Interaction and UX behavior requirements

1. Every resolver result card must display one provenance badge:
   - `Live resolver response`
   - `Simulated/demo response`

2. Verdict algorithm must be visible in UI:
   - `SAFE TO USE` only if structure pass + freshness pass + signature pass (when applicable).
   - `DO NOT USE` if freshness fail or structure fail or signature fail.
   - `MANUAL REVIEW` when redirect not followed or required material unavailable.

3. All timestamps shown in UTC + local display.
4. All failures must include raw machine-parseable payload.
5. No silent fallbacks; state transitions must be explicit.

## Engineering scope (implementation tasks)

### Phase 1 — Audit artifact finalization

- [x] Consolidate and refresh comprehensive report with production observations.
- [x] Add explicit appendix quantifying file-level live vs simulated surfaces.
- [x] Produce senior-team-ready executive and deep-dive sections.

### Phase 2 — Frontend implementation

- [x] Create resolver consumer pages and shared CSS tokens/components.
- [x] Implement real fetch flows for health, well-known, resolve (direct + b64u), etag revalidate.
- [x] Implement status-aware result rendering for `200/307/400/404/405/410/500`.
- [x] Implement trust verdict engine and diagnostics drawer.

### Phase 3 — Alignment cleanup

- [x] Update stale simulation messaging or route examples that conflict with real resolver domain.
- [x] Ensure docs and examples distinguish simulation from live behavior.
- [x] Ensure API/body examples reflect runtime behavior.

### Phase 4 — Verification

- [x] Run build/typecheck/test/smoke scripts.
- [x] Browser verification using DevTools (load pages, validate visuals, check console clean).
- [x] Capture verification evidence paths in report.

## Acceptance criteria

### Report quality acceptance

- [x] Report explicitly classifies each relevant surface as `Live`, `Skeleton`, `Simulated`, or `Mock`.
- [x] Report includes production-observed command evidence from audit date.
- [x] Report includes line-referenced provenance for all critical claims.
- [x] Report includes remediation sequence with severity and execution order.

### Frontend quality acceptance

- [x] A non-expert user can resolve a UMID in <30 seconds.
- [x] Verdict state (`SAFE TO USE` / `DO NOT USE` / `MANUAL REVIEW`) is always present.
- [x] Redirect (`307`) path is treated as a first-class valid resolver outcome.
- [x] Error-state messaging is explicit and non-ambiguous.
- [x] UI clearly labels data provenance (live vs simulated) at all times.

### Contract alignment acceptance

- [x] UI behavior is contract-consistent for headers/status semantics.
- [x] Example/documentation drift relevant to consumer usage is eliminated.
- [x] Smoke checks remain green after changes.

## Validation commands

- `cd services/myum-resolver && npm run typecheck`
- `cd packages/universal-manifest && node scripts/smoke-endpoints.mjs --mode prod --docs-base https://universalmanifest.net --resolver-base https://myum.net`
- `cd site && npm run build:clean`
- Browser verification via DevTools:
  - load `/resolver/` and `/resolver/ops`
  - execute success + failure + redirect cases
  - confirm no console errors

## Evidence locations

- Comprehensive report:
  - `.dev/ai/reports/`
- Work order implementation files:
  - `site/public/resolver/` (or final route paths)
- Contract and resolver source:
  - `services/myum-resolver/`

## Notes for execution

- Prefer improving/extending the existing harness logic where practical, but keep the new consumer frontend distinct from the technical harness UX.
- Preserve strict labeling so no stakeholder confuses simulated flows for live runtime resolution.
- If production behavior diverges from repository source during execution, capture drift with timestamps and treat deployment alignment as a blocker before final signoff.
