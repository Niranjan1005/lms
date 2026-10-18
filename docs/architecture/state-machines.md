# State Machines

## Device

~~~text
PENDING -> REGISTERED -> ACTIVE -> SUSPENDED -> RETIRED
                         |
                         +-> REHOST_REQUIRED
~~~

## Grant

~~~text
DRAFT -> ISSUED -> DELIVERED -> ACCEPTED -> ACTIVE -> GRACE -> EXPIRED
                                               |
                                               +-> REVOKED
~~~

## Installation

~~~text
AVAILABLE -> VERIFIED -> STAGED -> INSTALLING -> HEALTH_CHECK -> ACTIVE
                                                    |
                                                    +-> ROLLED_BACK
~~~

State changes are explicit, auditable and transactional where business integrity requires it.