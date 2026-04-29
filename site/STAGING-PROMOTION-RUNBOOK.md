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

1. staging docs deploy is attempted
2. staging resolver deploy is attempted
3. staging smoke passes against the resolved staging targets:
   - `npm run smoke:endpoints:staging`
4. staging post-deploy verify passes against the resolved staging targets:
   - `npm run verify:postdeploy:staging`

In the current reverted workflow state, production deploy is blocked when
`verify_staging` fails. A failed staging deploy outcome is still important,
but it is advisory unless it causes the downstream staging verification
steps to fail.

### Current workflow behavior after revert `e493b3e`

The live `deploy-gated.yml` no longer includes the WO-0234 deploy-outcome
hard gate or the WO-0237 explicit reachability probe step. After revert
commit `e493b3e`:

- both staging deploy steps still use `continue-on-error: true`;
- `verify_staging` still blocks production when staging smoke or
  post-deploy verification fails;
- a non-success staging deploy outcome does **not** by itself fail
  `verify_staging` if the subsequent verification steps still pass against
  the currently resolved staging targets.

Operationally, treat any non-success staging deploy outcome as an operator
warning even if the workflow later goes green. Review the staging deploy job
logs before trusting a promotion that verified against a previously healthy
staging surface.

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

Staging verification in `deploy-gated.yml` uses:

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
