# Audit Event Catalogue

Audit events are append-only and designed for investigation, compliance evidence and operational traceability.

## Event envelope

~~~json
{
  "event_id": "evt_...",
  "event_type": "grant.issued",
  "actor": {"type": "user", "id": "usr_..."},
  "scope": {"customer_id": "cust_...", "device_id": "dev_..."},
  "object": {"type": "grant", "id": "grant_...", "revision": 4},
  "result": "success",
  "reason": "approved allocation change",
  "request_id": "req_...",
  "occurred_at": "2026-10-18T12:00:00Z"
}
~~~

## Required event families

| Family | Example events |
|---|---|
| Identity | auth.login_success, auth.login_failed, role.changed |
| Customer/site | customer.created, site.updated |
| Device | device.registered, device.transfer_requested, device.rehost_approved, device.decommissioned |
| Entitlement | entitlement.created, entitlement.term_changed, entitlement.quantity_changed |
| Allocation | allocation.created, allocation.rebalanced |
| Grant | grant.issued, grant.superseded, grant.revoked, grant.rejected_by_device |
| Trial | trial.started, trial.extended, trial.expired, trial.converted |
| Capacity | capacity.assessed, capacity.override_requested, capacity.override_approved |
| Release | release.created, release.promoted_stable, release.promoted_lts, release.retired |
| Model | model_release.published, model_release.promoted, model_key_authorization.failed |
| Deployment | deployment.created, deployment.started, deployment.failed, deployment.rolled_back, deployment.completed |
| Offline | offline.request_imported, offline.response_issued, offline.receipt_reconciled |
| Security | signing_key.rotated, privileged_override.approved, suspicious_clock_detected |
| Integration | erp.event_received, erp.reconciliation_failed |

## Retention

Baseline retention is configurable 1–3 years. Customer/regulatory requirements may extend it. Deletion/retention jobs must themselves be audited.