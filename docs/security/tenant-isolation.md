# Tenant Isolation Standard

SaaS mode is multi-tenant. Cross-tenant disclosure or mutation is a security-critical defect and release blocker. Customer-hosted mode keeps the same tenant-aware code paths even when deployed for one customer.

## Isolation model
Every business object either carries `customer_id` directly or has an enforceable ownership path to one. Authorization resolves caller permissions and tenant/object scope before repository/service mutation or response serialization.

## Enforcement layers
### API/service
- never accept `customer_id` or object ID as proof of access
- resolve principal permissions + permitted customer/site/device scope
- avoid leaking unauthorized object existence where appropriate

### Repository/data access
- tenant-scoped repository methods require explicit scope context
- joins used for indirect ownership are validated
- unscoped/global query APIs are restricted to explicit privileged paths

### Async/jobs
- job/outbox payload includes tenant/customer scope
- worker re-resolves referenced objects before action
- missing scope is a failure, not 'all tenants'

### Artifact/deployment/offline
- deployment targets must belong to permitted customer/product context
- offline requests cannot obtain another tenant's grant/artifact
- temporary artifact URLs are short-lived/scoped where used

### Audit/support
- customer audit views are tenant-scoped
- global/support access requires explicit role and is audited
- support object IDs/deep links never bypass scope validation

## Required negative tests
1. guessed-ID read
2. enumeration through search/filter/export
3. guessed-ID mutation
4. cross-tenant nested object reference
5. cross-tenant deployment/allocation target
6. background job with wrong/missing scope
7. offline request for another tenant
8. audit/export leakage
9. support/global overreach
10. cache key/response mix-up

## Database/RLS
Application authorization is mandatory regardless of whether PostgreSQL Row-Level Security is later adopted. RLS may provide defense-in-depth but is not the sole isolation mechanism.

## Observability and incident handling
Authorization denials are measured. Suspected cross-tenant patterns alert Security. Any confirmed/suspected disclosure follows the tenant-isolation incident playbook and requires regression tests before closure.

## Related SDR/ADR
`SDR-BE-009`, `SDR-SEC-001`, `SDR-SEC-007`; ADR-016