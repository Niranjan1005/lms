# Test Strategy

Testing follows risk and trust boundaries, not only code modules. Critical licensing/security/update behavior requires automated negative tests and end-to-end evidence.

## Test layers

### Unit
Policy resolution, constraints, grant canonicalization, state transitions, compatibility rules, recommendation logic and error mapping.

### Repository/database
FK/unique/check constraints, tenant-scoped query behavior, transaction rollback, optimistic concurrency, idempotency, migrations and indexes.

### API integration
Authentication, authorization, validation, error envelopes, idempotency and cross-module workflows against real PostgreSQL.

### Central-edge contract
Grant/manifest schemas, signature/canonicalization compatibility, offline request/response, check-in/receipt and release-set contracts.

### System/end-to-end
Registration -> entitlement -> allocation -> grant -> local verification -> install/activation -> receipt; trial, renewal, reallocation, OTA/model OTA, rehost, transfer, revocation and offline flows.

### Security
Tenant isolation, IDOR/BOLA, auth abuse/rate limit, signature tamper, replay/rollback, malformed archive, path traversal, unknown critical schema, key rotation/trust-store and privilege escalation.

### Capacity/performance
Benchmark profile regression, combined workload, stale assessment triggers, representative hardware, local authoritative checks, soak/load/fault tests.

## Environments

- local/unit with synthetic fixtures
- integration with PostgreSQL and development signing provider
- QA with central + edge simulator/representative agents
- hardware lab for capacity/update/device identity
- staging production-like environment without uncontrolled production data

## Test data

Use synthetic customers/devices/entitlements and generated test keys. Production private keys/customer exports are prohibited in normal test environments.

## Automation gates

PR CI runs unit, API/integration, migration, tenant isolation, signature/contract and static security tests appropriate to the change. Longer hardware/upgrade/rollback/soak tests run in dedicated pipelines before Stable promotion.

## Failure injection

Required scenarios include signing outage, artifact timeout, DB reconnect, worker restart, duplicate request, process crash during install, power/interruption simulation, corrupted offline bundle and rollback failure.

## Evidence

Release evidence links test versions/environment, pass/fail summary, known exceptions and relevant artifacts/logs. A green unit suite alone is not production readiness.