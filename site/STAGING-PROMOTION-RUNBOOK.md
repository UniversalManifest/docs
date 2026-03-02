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

Current operational staging hosts (while custom-domain DNS is pending):

- docs fallback: `https://universalmanifest-net-staging.pages.dev`
- resolver fallback: `https://myum-resolver-staging.grig-624.workers.dev`

## Isolation Requirements

- Staging and production resolver MUST use different KV namespace IDs.
- Staging must never deploy against production KV bindings.
- Staging and production smoke checks MUST run against explicit base URLs.

Resolver staging config entrypoint:

- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/wrangler.toml` (`[env.staging]`)

## Promotion Gate Policy

Promotion is allowed only if all staging gates pass:

1. staging docs deploy succeeds
2. staging resolver deploy succeeds
3. staging smoke passes:
   - `npm run smoke:endpoints:staging`
4. staging post-deploy verify passes:
   - `npm run verify:postdeploy:staging`

Production deploy is blocked if any staging gate fails.

## Automated Release Path

Workflow:

- `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml`

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
- `STAGING_DOCS_BASE` (optional override for staging verification job)
- `STAGING_RESOLVER_BASE` (optional override for staging verification job)
- `STAGING_RESOLVER_WWW_BASE` (optional override for staging verification job)

## Command References

Staging smoke:

```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
npm run smoke:endpoints:staging
```

Staging smoke (fallback hosts, explicit override):

```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
node scripts/smoke-endpoints.mjs --mode prod --docs-base https://universalmanifest-net-staging.pages.dev --resolver-base https://myum-resolver-staging.grig-624.workers.dev
```

Staging post-deploy verify:

```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
npm run verify:postdeploy:staging
```

Staging post-deploy verify (fallback hosts, explicit override):

```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
node scripts/post-deploy-verify.mjs --mode prod --docs-base https://universalmanifest-net-staging.pages.dev --resolver-base https://myum-resolver-staging.grig-624.workers.dev --resolver-www-base https://myum-resolver-staging.grig-624.workers.dev
```

Production smoke:

```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
npm run smoke:endpoints:prod
```

Production post-deploy verify:

```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
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
   - `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/deploy-checks/`
