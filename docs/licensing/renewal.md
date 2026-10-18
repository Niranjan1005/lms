# Renewal & Offline Validity

Three clocks remain independent:

1. **Commercial term/expiry**.
2. **Offline authorization freshness** — default 7 days unless overridden by policy.
3. **Grace/restriction period** — default 7 days unless separately overridden.

A successful check-in never extends the paid commercial term.

A payment or central entitlement renewal does not activate an offline device until the new signed grant revision is delivered/imported and accepted locally.

## Reminder baseline

Default proposed reminders are 30 days, 7 days and 1 day before expiry, configurable by product/customer policy.

~~~mermaid
flowchart LR
    A[Due Soon / Reminder] --> B[Renewal Requested]
    B --> C[Commercial Approval]
    C --> D[Entitlement Term Updated]
    D --> E[New Signed Grant Revision]
    E --> F{Delivery}
    F -->|Online| G[Delivered]
    F -->|Offline| H[Export / Import]
    G --> I[Local Verify]
    H --> I
    I --> J[Atomic Accept / Active]
    J --> K[Receipt / Reconciliation]
~~~

## Status milestones

- Due Soon
- Requested
- Approved / Grant Issued
- Delivered / Imported
- Accepted / Active
- Failed / Rejected
- Expired / Restricted

`Issued != Delivered != Accepted`.

If delivery or verification fails, the old grant continues according to its own expiry/grace rules. Where product safety permits, restricted/grace mode should preserve diagnostics, license recovery/import and access to existing customer data while unauthorized analytics execution is disabled.