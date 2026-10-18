# Operational Runbook Baseline

Runbooks are executable operational procedures for restoring service safely without requiring responders to infer architecture from source code.

## Required production runbooks

1. LMS API unavailable
2. PostgreSQL degraded/unavailable
3. signing provider unavailable
4. artifact repository unavailable
5. background job/outbox dead-letter backlog
6. failed Stable rollout
7. mass rollout pause/rollback
8. rollback failure
9. offline bundle rejected
10. device stuck in REHOST_REQUIRED
11. entitlement over-allocation/conflict
12. renewal approved but device remains expired
13. stale check-in spike
14. suspected signing-key compromise
15. tenant-isolation suspicion
16. backup restore
17. customer-hosted LMS recovery
18. ERP synchronization mismatch

## Required runbook structure

Each runbook contains:
- purpose/scope
- triggering alerts/symptoms
- customer impact
- safety/security warnings
- prerequisites/permissions
- diagnostic commands/portal/API checks
- expected decision tree
- approved remediation
- retry/idempotency considerations
- rollback/recovery
- evidence to preserve
- escalation threshold/owner
- customer communication input
- post-incident follow-up

## Runbook safety principles

- do not disable signature verification
- do not hand-edit grants/entitlements in DB as normal remediation
- do not move devices between tenants to fix lookup errors
- do not delete failed deployment/audit evidence before investigation
- do not retry non-idempotent workflows blindly
- do not expose keys/tokens/decrypted models in tickets/chat

## Severity baseline

| Severity | Description | Example |
|---|---|---|
| Sev-1 | broad critical outage/security/data exposure | signing compromise, tenant breach, platform-wide license failure |
| Sev-2 | major customer/service impairment | widespread deployment/renewal failure, rollback issue |
| Sev-3 | limited degradation | single-customer update/rehost issue with workaround |
| Sev-4 | minor/non-urgent | cosmetic/reporting issue |

Severity is based on impact, security/data risk and breadth, not which module produced the error.

## Validation

Critical runbooks are exercised in staging/tabletop/DR tests before production and after material architecture changes. Runbooks that fail during an incident are corrected as part of post-incident action.