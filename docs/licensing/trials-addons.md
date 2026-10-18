# Trials & Add-ons

Trials and add-ons use the normal entitlement/policy/grant trust model. They are not special UI flags or reusable license files.

## Trials

### Default policy
- default duration: 7 days
- configurable by product/feature/campaign/approved customer exception
- baseline eligibility: one trial per customer entitlement + feature
- starts at first successful feature activation
- signed, device-bound, time-limited grant
- globally reusable trial license prohibited

### Trial lifecycle
~~~text
ELIGIBLE -> REQUESTED -> APPROVED / BUNDLE_READY -> ACTIVATED -> ACTIVE -> EXPIRED
              |                     |
              +-> REJECTED          +-> FAILED_ACTIVATION
~~~

Trial clock does not start at request, approval, grant issuance, package download or offline import. It starts only when local activation succeeds and the device records activation time/evidence.

### Offline trial nuance
For air-gapped activation, the device records first successful activation and emits a signed activation receipt for later central reconciliation. Implementation must also enforce an issuance/import/activate-by bound so a trial cannot be stockpiled indefinitely; exact anti-clock-abuse mechanics are part of the detailed grant/trusted-time design.

### Repeat/extension
Additional trial or extension requires explicit campaign/admin policy, reason and audit; maker-checker may be required for exceptions.

## Add-ons

### Default co-termination
Subscription add-ons normally co-terminate with the active base subscription:
~~~text
Base: Jan 1 ---------------- Dec 31
PPE :                 Sep 1 -- Dec 31
Renewal: Jan 1 ---- Base + PPE together
~~~

Commercial pricing may be prorated; pricing calculation itself may remain ERP/commercial responsibility.

### Independent add-on
Product/commercial policy may explicitly mark an add-on independent, allowing its own term. Independence is metadata/policy, not inferred from dates.

### Perpetual base
Perpetual base may carry subscription add-ons. Expiry of an add-on does not invalidate the perpetual base.

### Dependency behavior
Dependent add-ons become dormant when required base authorization is inactive. An independent add-on still requires whatever technical/runtime dependencies its feature declares.

## Purchase/activation distinction
Trial request, purchase request, ERP/payment approval or Marketplace selection does not itself authorize execution. Device still requires a valid signed grant plus compatibility, installed/healthy content and local capacity validation.

## Conversion trial -> paid
Paid entitlement/grant supersedes or replaces trial authorization according to grant lineage/policy; it does not extend the trial artifact by editing its expiry in place.

## Related SDR
`SDR-TRL-001` through `SDR-TRL-005`, `SDR-ADD-001` through `SDR-ADD-004`