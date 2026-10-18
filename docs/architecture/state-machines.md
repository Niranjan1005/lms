# State Machines

State transitions are explicit, auditable and transactional where business integrity requires it.

## Device

~~~text
PENDING -> REGISTERED -> ACTIVE -> SUSPENDED -> RETIRED
                         |
                         +-> REHOST_REQUIRED
~~~

## Grant / License

~~~text
DRAFT -> ISSUED -> DELIVERED -> ACCEPTED -> ACTIVE -> GRACE -> EXPIRED
                                               |
                                               +-> REVOKED
~~~

`ISSUED` does not mean the device has received it. `DELIVERED` does not mean the device accepted it.

## Trial

~~~text
ELIGIBLE -> REQUESTED -> ISSUED -> ACTIVE -> EXPIRED
                                      |
                                      +-> CONVERTED
~~~

Trial time begins when activation succeeds, not when the request or grant is issued.

## Purchase Request

~~~text
REQUESTED -> REVIEW -> APPROVED -> PAID/COMMERCIAL_CONFIRMED -> GRANT_ISSUED
                  |
                  +-> REJECTED
~~~

A purchase request or catalog entry never authorizes execution by itself.

## Offline Request / Response

~~~text
CREATED -> EXPORTED -> RECEIVED -> APPROVED -> RESPONSE_ISSUED -> IMPORTED -> RECONCILED
                           |            |
                           |            +-> REJECTED
                           +-> EXPIRED
~~~

## Installation

~~~text
AVAILABLE -> DOWNLOADED/IMPORTED -> VERIFIED -> STAGED -> INSTALLING -> HEALTH_CHECK -> ACTIVE
                                                              |             |
                                                              |             +-> ROLLED_BACK
                                                              +-> FAILED
~~~

## Renewal

~~~text
DUE_SOON -> REQUESTED -> APPROVED_GRANT_ISSUED -> DELIVERED_IMPORTED -> ACCEPTED_ACTIVE
                |                   |                     |
                +-> REJECTED       +-> FAILED            +-> FAILED
                                                            |
                                                            +-> EXPIRED_RESTRICTED
~~~

## Governance rule

Any implementation-specific state must map cleanly to these business states or be documented as an internal sub-state. UI/API must not collapse distinct business milestones that affect support or audit.