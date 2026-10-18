# Consolidated Business Rules

This page is the normative cross-domain business-rule checklist for LMS. More detailed pages remain authoritative for implementation specifics.

## Licensing and entitlement

- Registration, commercial licensing and capacity validation are separate states.
- Entitlement = what the customer owns; allocation = distribution of pooled rights; grant = device-bound signed executable authorization.
- Customer pooled quantity must never be over-allocated.
- Reallocation creates superseding grants and must not allow old/new quantities to remain simultaneously usable indefinitely.
- Subscription and perpetual base licenses are supported.
- Subscription add-ons co-terminate with the base by default; explicitly independent add-ons may have their own term.
- A perpetual base may carry subscription add-ons.
- Dependent add-ons become dormant when the required base is inactive.
- Commercial expiry, offline authorization freshness and grace are three independent clocks.
- Successful check-in never extends commercial expiry.
- Payment/renewal approval alone does not renew an offline device until it receives and accepts the new signed grant revision.

## Trials

- Default trial duration is 7 days and is policy-configurable.
- Trial starts on first successful feature activation, not on request, issuance or package import.
- Baseline eligibility is one trial per customer entitlement + feature, unless an auditable admin/campaign override permits another trial.
- A trial is a signed time-limited grant; globally reusable trial licenses are prohibited.

## Device lifecycle

- Device identity is cryptographic key + versioned weighted hardware fingerprint; MAC is evidence only.
- Minor hardware changes trigger re-evaluation and normally continue.
- Major identity changes enter `REHOST_REQUIRED`; they do not silently destroy or transfer licenses.
- Decommission/replacement returns eligible allocation to the entitlement pool after approval/reconciliation.
- Device transfer is request/approval/audit driven; ownership is never silently overwritten.
- Air-gapped revocation becomes effective only after signed state is imported or existing offline authorization expires.

## Capacity

- Central capacity assessment is advisory/pre-assessment; local capacity check is authoritative for actual activation.
- Commercial rights are never silently reduced because hardware is insufficient.
- Capacity engine recommends alternatives; an operator/customer chooses the allowed configuration.

## Marketplace and OTA

- Marketplace discovery/trial/purchase does not itself authorize execution.
- A feature activates only when compatible, licensed, installed, healthy and capacity-validated.
- Automatic production updates consume Stable by default.
- LTS deployment is explicitly company-controlled.
- Normal site releases must automate migration, health-check and rollback; no manual migration step.
- Models are independently versioned, encrypted, signed and inventory-aware.
- Offline bundles should contain only missing/required artifacts where possible.

## Governance

- High-risk actions use maker-checker approval.
- Audit retention baseline is configurable 1–3 years.
- Portal + email are initial notification channels; webhook delivery remains extensible.
- LMS is not an accounting system; ERP integration is separate.