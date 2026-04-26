# Staging and Promotion Runbook (Two-Surface Deployments)

This runbook defines the staging-to-production path for both public surfaces:

- standards/docs surface (`universalmanifest.net`)
- resolver surface (`myum.net`)

It is the operational baseline for safe release iteration.

## Environment Matrix

Production:

- docs: `https://universalmanifest.net`
- resolver: `https://myum.net`
- resolver host variant: `https://www.myum.net`

Staging:

- docs: `https://staging.universalmanifest.net`
- resolver: `https://staging.myum.net`
- resolver host variant: `https://www.staging.myum.net`

Custom-domain staging status:

- active as of 2026-03-03 and validated in CI:
  - `https://github.com/grigb/universal-manifest/actions/runs/22602253533`
  - `https://github.com/grigb/universal-manifest/actions/runs/22602225159`

Fallback staging hosts (used automatically when custom domains are unreachable):

- docs fallback: `https://universalmanifest-net-staging.pages.dev`
- resolver fallback: `https://myum-resolver-staging.grig-624.workers.dev`

## Isolation Requirements

- Staging and production resolver MUST use different KV namespace IDs.
- Staging must never deploy against production KV bindings.
- Staging and production smoke checks MUST run against explicit base URLs.

Resolver staging config entrypoint:

- `services/myum-resolver/wrangler.toml` (`[env.staging]`)

## Promotion Gate Policy

Promotion is allowed only if all staging gates pass:

1. staging docs deploy succeeds
2. staging resolver deploy succeeds
3. staging reachability probes pass (see "Reachability Gate (WO-0237)" below)
4. staging smoke passes:
   - `npm run smoke:endpoints:staging`
5. staging post-deploy verify passes:
   - `npm run verify:postdeploy:staging`

Production deploy is blocked if any staging gate fails.

### Gate-Failure Semantics (WO-0234)

The two staging deploy steps in `.github/workflows/deploy-gated.yml`
(`Deploy Pages (staging)` and `Deploy resolver (staging)`) carry
`continue-on-error: true`. This is **intentional**: the workflow records
each step outcome (`success` / `failure`) into a job output (`deploy_outcome`)
so that a downstream gate can present a single consolidated promotion
decision rather than aborting mid-flight.

The compensating gate is the first step of the `verify_staging` job,
`Assert staging deploys succeeded`. It reads
`needs.deploy_staging_docs.outputs.deploy_outcome` and
`needs.deploy_staging_resolver.outputs.deploy_outcome` and **fails the
job** if either is not `success`. Because both
`deploy_production_docs` and `deploy_production_resolver` declare
`needs: verify_staging` (and `needs: [verify_staging, ...]`), a failed
`verify_staging` blocks both production deploys.

**What fails the workflow (hard fail, blocks promotion):**

- Either staging deploy step exits non-zero → `verify_staging` fails on its
  first step with `FAIL: staging docs deploy outcome was "<outcome>"`
  (or the resolver equivalent).
- Staging smoke (`smoke-endpoints.mjs`) fails for any reason.
- Staging post-deploy verify (`post-deploy-verify.mjs`) fails for any
  reason.
- Production KV namespace binding assertion fails (see
  `Assert production KV namespace binding`).

**What is allowed to advisory-fail (no current cases):**

There are presently no advisory-fail steps in the staging path. Every
`continue-on-error: true` flag is paired with a downstream hard gate.
If a future change introduces an advisory step, it must (a) document the
rationale here and (b) add or extend a downstream gate so the failure is
either escalated or explicitly waived.

**Operator response when the gate fires:**

1. Inspect the `Assert staging deploys succeeded` step in the failed
   `verify_staging` job — the printed line names which deploy outcome was
   non-success.
2. Open the corresponding deploy job (`Deploy staging docs` or
   `Deploy staging resolver`) and read the `Deploy …` step logs to
   identify the underlying failure (auth preflight, KV binding,
   wrangler retry exhaustion, etc.).
3. Fix the underlying issue (rotate / set the missing secret or variable,
   restore the staging KV namespace, fix the wrangler config, etc.).
4. Re-run `deploy-gated.yml` against the same `ref`. Do not bypass the
   gate by toggling `continue-on-error` off-the-cuff — the gate exists
   precisely to prevent a stale staging surface from being promoted.
5. If the failure is environmental (provider outage) and the staging
   surface is otherwise verified healthy via manual smoke, document the
   incident under `.dev/ai/reports/deploy-checks/` and wait for the
   provider issue to clear before retrying.

### Reachability Gate (WO-0237)

After `select-staging-bases.mjs` resolves the staging `DOCS_BASE` and
`RESOLVER_BASE`, the `verify_staging` job runs explicit `curl` probes (step
name: "Probe staging targets are reachable") against the resolved targets
**before** the smoke and post-deploy verify steps execute. Without this
gate, a successful target-resolution step does not actually prove the
selected hosts respond to HTTP — the smoke step would be the first to
discover the surface is unreachable, with less explicit diagnostics.

Probes:

- docs root probe: `curl -sS --max-time 30 "${DOCS_BASE%/}/"` must return 2xx.
- resolver health probe: `curl -sS --max-time 30 "${RESOLVER_BASE%/}/health"` must return 2xx.

Each probe captures `http_status` and `time_total` in the workflow log for
diagnostics. On failure, the step prints `staging target unreachable:
<label> (<url>) -- http_status=<code> time_total=<seconds>s` and
`verify_staging` fails, which blocks both `deploy_production_docs` and
`deploy_production_resolver` (they declare `needs: verify_staging`).

Resolver `/health` contract:

- The resolver runtime exposes `GET /health` and returns
  `{ "status": "ok", "contract": "<contract-version>" }` with HTTP 200.
- Source: `services/myum-resolver/src/index.ts` (`pathname === '/health'`).
- The endpoint is also referenced from the resolver descriptor at
  `/.well-known/myum-resolver.json` and from
  `select-staging-bases.mjs`'s custom-domain probe set above.

**Operator response when the reachability gate fires:**

1. Inspect the "Probe staging targets are reachable" step log; the printed
   `staging target unreachable: <label> (<url>) -- http_status=…
   time_total=…` line names which surface failed and the observed status.
2. Cross-check the upstream deploy job logs (`Deploy staging docs` /
   `Deploy staging resolver`) and DNS / Cloudflare custom-domain status.
3. If the custom-domain hosts are unhealthy but the fallback hosts are
   healthy, re-run `deploy-gated.yml` — `select-staging-bases.mjs` will
   automatically fall back to `pages.dev` + `workers.dev`.
4. If both custom-domain and fallback hosts are unreachable, treat as a
   provider incident and follow the same procedure as the deploy-outcome
   gate above.

## Automated Release Path

Workflow:

- `.github/workflows/deploy-gated.yml`
- `.github/workflows/provision-staging-domains.yml` (re-applies staging custom-domain deployment for docs proxy + resolver)

Manual trigger inputs:

- `ref` (branch/tag/SHA)
- `promote_to_production` (`false` or `true`)

### Required CI secrets and variables

Secrets:

- `CF_ACCOUNT_ID`
- `CF_API_TOKEN`

Repository variables:

- `CF_PAGES_PROJECT_STAGING`
- `CF_PAGES_PROJECT_PROD`
- `STAGING_DOCS_BASE` (optional explicit override for staging verification target)
- `STAGING_RESOLVER_BASE` (optional explicit override for staging verification target)
- `STAGING_RESOLVER_WWW_BASE` (optional explicit override for staging verification target)

### Automatic staging target selection

Both staging verification and staging synthetic monitoring use:

- `packages/universal-manifest/scripts/select-staging-bases.mjs`

Selection precedence:

1. Explicit override mode if `STAGING_DOCS_BASE` and `STAGING_RESOLVER_BASE` are set
2. Custom-domain auto mode if all custom-domain probes pass:
   - `https://staging.universalmanifest.net/`
   - `https://staging.universalmanifest.net/resolver/`
   - `https://staging.myum.net/health`
   - `https://staging.myum.net/.well-known/myum-resolver.json`
   - `https://www.staging.myum.net/health`
3. Fallback auto mode (`pages.dev` + `workers.dev`) when custom-domain probes fail

Local dry-run examples:

```bash
cd <repo-root>
node packages/universal-manifest/scripts/select-staging-bases.mjs --format json
```

```bash
cd <repo-root>
STAGING_DOCS_BASE=https://example.com STAGING_RESOLVER_BASE=https://example.org node packages/universal-manifest/scripts/select-staging-bases.mjs --format shell
```

## Command References

Staging smoke:

```bash
cd packages/universal-manifest
npm run smoke:endpoints:staging
```

Staging smoke (fallback hosts, explicit override):

```bash
cd packages/universal-manifest
node scripts/smoke-endpoints.mjs --mode prod --docs-base https://universalmanifest-net-staging.pages.dev --resolver-base https://myum-resolver-staging.grig-624.workers.dev
```

Staging post-deploy verify:

```bash
cd packages/universal-manifest
npm run verify:postdeploy:staging
```

Staging post-deploy verify (fallback hosts, explicit override):

```bash
cd packages/universal-manifest
node scripts/post-deploy-verify.mjs --mode prod --docs-base https://universalmanifest-net-staging.pages.dev --resolver-base https://myum-resolver-staging.grig-624.workers.dev --resolver-www-base https://myum-resolver-staging.grig-624.workers.dev
```

Production smoke:

```bash
cd packages/universal-manifest
npm run smoke:endpoints:prod
```

Production post-deploy verify:

```bash
cd packages/universal-manifest
npm run verify:postdeploy:prod
```

## Rollback Protocol

Docs:

- Redeploy the last known-good Pages artifact to the same Pages project.

Resolver:

- Redeploy the last known-good Worker version to target environment (`staging` or `production`).

After rollback:

1. rerun smoke for the affected environment
2. rerun post-deploy verify for the affected environment
3. record report artifact path under:
   - `.dev/ai/reports/deploy-checks/`
