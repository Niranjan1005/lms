# Approval & Maker-Checker Workflows

Approval workflows separate intent from execution for actions where one mistaken or compromised account could materially affect commercial rights, security posture or fleet operation.

## Workflow model

~~~text
DRAFT -> SUBMITTED -> APPROVED -> EXECUTING -> EXECUTED
          |            |             |
          +-> REJECTED +-> EXPIRED   +-> FAILED
          +-> CANCELLED
~~~

## Approval record

Every approval captures:
- approval/request ID
- action type
- target object IDs
- exact requested payload or immutable payload hash
- target object revision
- requester
- required approver role/separation
- reason/business justification
- submitted/approved/executed timestamps
- expiry
- decision comment
- execution result/error/audit reference

## Binding rule

Approval applies only to the reviewed payload/object revision. If entitlement quantity, target device, grant term, release, capacity override scope or other material parameters change, the approval becomes invalid and must be resubmitted.

## Single-actor operations

Examples where policy can allow one authorized actor:
- allocate quantity within already approved entitlement pool
- normal device registration
- standard renewal after approved commercial status
- publish Development/QA release
- routine customer/site metadata edit

## Maker-checker operations

At minimum evaluate/require separation for:
- create/increase entitlement outside approved ERP/order automation
- perpetual/exceptional custom grant
- trial extension/repeat outside policy
- cross-customer transfer
- major rehost
- capacity/security override
- Stable promotion and LTS designation
- forced broad production rollout
- mass revocation
- signing-key activation/rotation
- trust-bundle/key revocation
- model KEK/wrapping administration
- break-glass or high-risk audit export

## Execution

Approval does not itself mutate business state. An authorized execution service revalidates: approval status/expiry, object revision, caller/system permission and current business invariants before applying the action transactionally.

## Automation

ERP-approved or policy-approved automation may satisfy selected approval steps only when the automation identity, source event, rules and audit evidence are explicitly approved. 'Automated' does not mean 'uncontrolled'.

## Failure/retry

Execution failure leaves an explicit failed/pending state. Retrying uses idempotent execution and does not create duplicate entitlements/grants/releases.

## Related SDR

`SDR-SEC-008`, `SDR-GOV-002`