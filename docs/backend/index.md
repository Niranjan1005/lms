# Backend Engineering Architecture

The backend is a Python/FastAPI modular monolith that owns central business truth and orchestrates signing, storage, notifications, integrations and edge workflows.

## Baseline stack

- Python 3.12
- FastAPI
- Pydantic
- SQLAlchemy 2.x
- PostgreSQL
- Alembic
- background workers/scheduler
- React + Vite + TypeScript portal
- external artifact repository
- protected signing provider

## Modules

~~~text
identity_access
customers_sites
devices_enrollment
catalog_products_features
licensing_entitlements_allocations_grants
policy
capacity
marketplace
releases_models_artifacts
deployments
renewals_lifecycle
offline_exchange
notifications
integrations_erp
audit
telemetry_adapter
signing_gateway
~~~

## Architectural rules

1. Each endpoint has one owning module.
2. Controllers validate/authorize and delegate; cross-domain orchestration lives in application/use-case services.
3. Commercially atomic changes use one DB transaction where possible.
4. External side effects use outbox/jobs instead of weakening DB consistency.
5. Tenant scope is explicit in service/repository interfaces.
6. Public API contracts remain backward-compatible within `/v1`.
7. Long-running deployment/bundle work is represented by durable jobs/resources.
8. Signing private keys are never loaded into backend process memory from normal configuration.

## Data ownership

PostgreSQL owns transactional LMS state. Artifact repository owns immutable large binaries. Telemetry may use separate analytics storage. ERP remains external financial truth. Signing provider owns private cryptographic operations.

## Reliability model

External dependency failures are retried/idempotent. Dead-letter work is visible. Request IDs correlate API, audit, outbox/job and edge receipt flows.

## Security model

Human/device/service principals are distinct. Authorization is permission + tenant/object scope. Background jobs carry scope. All privileged mutations are audited.

## Related SDR

`SDR-BE-*`, `SDR-SEC-*`, `SDR-OPS-*`