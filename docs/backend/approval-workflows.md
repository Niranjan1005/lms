# Approval & Maker-Checker Workflows

Everyday operations should remain efficient; high-risk overrides require independent approval.

## Single-actor operations

Examples: allocating quantity within an already approved entitlement, normal renewal after approved commercial status, publishing a QA release, standard device registration.

## Maker-checker operations

Require separate requester and approver for:
- creating/increasing commercial entitlement outside imported/approved order state
- perpetual or exceptional custom grant
- trial extension beyond campaign/customer policy
- forced rehost after major identity change
- override of security/capacity block
- Stable/LTS production promotion
- emergency revocation override
- signing-key rotation/activation administrative workflow

## State model

~~~text
DRAFT -> SUBMITTED -> APPROVED -> EXECUTED
              |           |
              +-> REJECTED+-> CANCELLED
~~~

Approval records capture requester, approver, reason, policy evaluated, object revision, timestamps and execution result.