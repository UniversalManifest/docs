# Incident Report (Synthetic Drill)

Incident ID: INC-2026-03-04-synthetic-alert-drill
Date opened (UTC): 2026-03-04T04:55:29Z
Date resolved (UTC): 2026-03-04T04:56:48Z
Severity: SEV-3 (controlled drill)
Reporter: Codex automation
Incident commander: Platform/Ops owner

## 1) Detection

- Detection source (workflow/job URL): https://github.com/grigb/universal-manifest/actions/runs/22655716037
- First failing check: Production synthetic endpoint smoke with forced unknown UMID (urn:uuid:99999999-9999-4999-8999-999999999999)
- Was webhook alert delivered? (yes/no): yes
- Related run artifact paths:
  - /Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-wo-0121-synthetic-alert-drill-report.md
  - /Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-wo-0121-run2-job.log
  - /Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-wo-0121-webhook-requests.json

## 2) Impact

- Impacted surface: none (controlled drill)
- Start time (UTC): 2026-03-04T04:55:29Z
- End time (UTC): 2026-03-04T04:56:48Z
- User-facing impact summary: no production outage; drill intentionally forced synthetic failures
- Estimated scope: monitoring and alerting path validation only

## 3) Timeline (UTC)

- 04:55 detected (run 1 dispatched)
- 04:56 triage started (run 1 failure confirmed)
- 04:56 mitigation applied (run 2 dispatched to validate sustained alert path)
- 04:56 service recovered (drill complete; normal monitoring resumes)
- 04:57 incident closed

## 4) Root Cause

- Technical cause: synthetic checks were intentionally forced to fail via invalid UMID input in workflow_dispatch.
- Triggering condition: two consecutive failing runs with previous_conclusion=failure.
- Why this was not prevented earlier: this is intentional for drill validation; not a product defect.

## 5) Mitigation and Recovery

- Immediate mitigation: none required; drill ended after webhook dispatch proof.
- Validation commands:
  - gh run view 22655697651 --repo grigb/universal-manifest
  - gh run view 22655716037 --repo grigb/universal-manifest
  - curl -H 'Accept: application/json' https://webhook.site/token/<token>/requests?sorting=newest
- Monitoring recovery evidence:
  - controlled drill completed with expected alert behavior and no runtime deploy changes required.

## 6) Follow-Up Actions

- [x] Preventive action 1: Keep UM_SYNTHETIC_ALERT_WEBHOOK configured.
- [x] Preventive action 2: Document drill evidence and runbook references.
- [x] Documentation update
- [x] Test and monitoring update

## 7) Links

- Synthetic policy: /Users/grig/work/repo/universalmanifest/docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md
- Production smoke runbook: /Users/grig/work/repo/universalmanifest/docs/PRODUCTION-DEPLOY-SMOKE.md
- Resolver deploy runbook: /Users/grig/work/repo/universalmanifest/services/myum-resolver/CLOUDFLARE-DEPLOY.md
- Docs deploy runbook: /Users/grig/work/repo/universalmanifest/deploy/universalmanifest.net/CLOUDFLARE-PAGES.md
