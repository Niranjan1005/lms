# ERP Integration Contract

ERP and LMS remain separate systems. Integration is intentionally narrow so the LMS does not become an accounting platform.

## Authority split

| Data | System of record |
|---|---|
| Invoice/payment state | ERP |
| Contract/order reference | ERP |
| Commercial SKU/order line | ERP |
| Customer operational device/site topology | LMS |
| Entitlement operational state | LMS after approved import |
| Allocation/grant state | LMS |
| Deployment/check-in state | LMS |

## Inbound ERP event example

~~~json
{
  "event_id": "erp_evt_001",
  "event_type": "order_line_approved",
  "occurred_at": "2026-10-18T10:00:00Z",
  "customer_external_ref": "CUST-1007",
  "contract_ref": "CTR-2031",
  "order_ref": "SO-9001",
  "line": {
    "product_code": "ANALYTICS_BASE",
    "feature_code": "PPE",
    "quantity": 40,
    "term": {"type": "subscription", "start": "2026-11-01", "end": "2027-10-31"}
  }
}
~~~

## Integration rules

- ERP events are idempotent by `event_id`.
- Unknown product/SKU mapping is quarantined for review.
- Payment/renewal status alone does not directly modify a device grant; LMS first updates entitlement state and then issues a new grant revision.
- ERP retries are safe.
- LMS never overwrites financial truth back into ERP unless a separate outbound contract explicitly permits it.

## Reconciliation

A scheduled reconciliation compares approved ERP commercial lines against LMS entitlements. Differences are categorized as missing, extra, quantity mismatch, term mismatch or mapping failure and surfaced to operations without destructive auto-correction.