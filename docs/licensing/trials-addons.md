# Trials & Add-ons

## Trials

- Default trial period is 7 days.
- Duration is policy/campaign configurable by feature, product or approved customer exception.
- Trial starts at first successful feature activation, not request, issuance, package download or import.
- Trial is a signed time-limited device-bound grant, not a UI flag.
- Baseline eligibility is **one trial per customer entitlement + feature**.
- Admin/campaign override may permit extension or an additional trial, but the override is auditable and may require maker-checker approval.
- Globally reusable trial licenses are prohibited.

## Add-ons

Subscription add-ons normally co-terminate with the active base subscription.

~~~text
Base: Jan 1 ---------------- Dec 31
PPE:                 Sep 1 -- Dec 31
Renewal: Jan 1 ---- Base + PPE together
~~~

Commercial pricing may be prorated for the remaining base term. An explicitly independent add-on may carry its own term when product/commercial policy permits it.

Perpetual base licenses may have subscription add-ons.

Dependent add-ons become dormant when their required base is inactive unless the add-on policy explicitly marks them independent.

## Purchase/activation distinction

A trial request, purchase request, payment approval or marketplace selection does not itself authorize runtime execution. The device still requires a valid signed grant and all compatibility/capacity/install/health gates.