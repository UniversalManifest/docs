# Incident Report Template (Synthetic Monitoring)

Incident ID:  
Date opened (UTC):  
Date resolved (UTC):  
Severity:  
Reporter:  
Incident commander:

## 1) Detection

- Detection source (workflow/job URL):
- First failing check:
- Was webhook alert delivered? (yes/no):
- Related run artifact paths:

## 2) Impact

- Impacted surface:
- Start time (UTC):
- End time (UTC):
- User-facing impact summary:
- Estimated scope:

## 3) Timeline (UTC)

- `HH:MM` detected
- `HH:MM` triage started
- `HH:MM` mitigation applied
- `HH:MM` service recovered
- `HH:MM` incident closed

## 4) Root Cause

- Technical cause:
- Triggering condition:
- Why this was not prevented earlier:

## 5) Mitigation and Recovery

- Immediate mitigation:
- Validation commands:
- Monitoring recovery evidence:

## 6) Follow-Up Actions

- [ ] Preventive action 1
- [ ] Preventive action 2
- [ ] Documentation update
- [ ] Test/monitoring update

## 7) Links

- Synthetic policy: `/Users/grig/work/repo/universalmanifest/docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md`
- Production smoke runbook: `/Users/grig/work/repo/universalmanifest/docs/PRODUCTION-DEPLOY-SMOKE.md`
- Resolver deploy runbook: `/Users/grig/work/repo/universalmanifest/services/myum-resolver/CLOUDFLARE-DEPLOY.md`
- Docs deploy runbook: `/Users/grig/work/repo/universalmanifest/deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`
