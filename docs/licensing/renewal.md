# Renewal & Offline Validity

Three clocks remain independent:

1. Commercial expiry.
2. Offline authorization freshness, default 7 days.
3. Grace, default 7 days.

A check-in never extends paid commercial term.

~~~mermaid
flowchart LR
    A[Reminder] --> B[Renewal Request]
    B --> C[Commercial Approval]
    C --> D[New Entitlement Term]
    D --> E[Signed Grant Revision]
    E --> F{Delivery}
    F -->|Online| G[Sync]
    F -->|Offline| H[Import]
    G --> I[Device Verify & Accept]
    H --> I
    I --> J[Receipt / Reconciliation]
~~~