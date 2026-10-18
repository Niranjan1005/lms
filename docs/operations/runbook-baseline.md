# Operational Runbook Baseline

Runbooks must be executable by support/operations without requiring source-code knowledge.

## Required runbooks before production

1. LMS API unavailable
2. PostgreSQL degraded/unavailable
3. Signing service unavailable
4. Artifact repository unavailable
5. Failed Stable rollout
6. Mass rollback
7. Offline bundle rejected at customer site
8. Device stuck in REHOST_REQUIRED
9. Customer over-allocation conflict
10. Suspected signing-key compromise
11. Backup restore
12. ERP synchronization mismatch

## Runbook format

Each runbook contains:
- symptoms and alerts
- customer impact
- safety checks
- diagnostic steps
- approved remediation
- rollback/recovery
- escalation owner
- audit/evidence to retain
- post-incident follow-up

## Incident severity proposal

| Severity | Description | Example |
|---|---|---|
| Sev-1 | broad critical outage/security compromise | signing-key compromise, platform-wide license failure |
| Sev-2 | major customer/service impairment | deployment/renewal failure affecting many devices |
| Sev-3 | limited degradation | single-customer update issue with workaround |
| Sev-4 | minor/non-urgent | cosmetic portal issue |