# Tenant Isolation Standard

SaaS mode is multi-tenant. Cross-tenant disclosure or mutation is treated as a security-critical defect.

## Enforcement model

Every business object is associated with a customer/tenant directly or through a verified ownership path. Authorization resolves caller scope before repository/service operations.

## Rules

- Never accept `customer_id` as proof of access.
- Repository methods for tenant data require explicit scope/context.
- Background jobs carry tenant identity with the job payload.
- Audit queries are tenant-scoped unless caller has explicit global audit permission.
- Artifact/deployment targets are validated against customer ownership before delivery.
- Customer-hosted mode may be single-customer, but code paths remain compatible with tenant checks.

## Required tests

1. user from Customer A cannot read Customer B object by ID
2. user from A cannot enumerate B through filters/search
3. user from A cannot mutate B using guessed IDs
4. background jobs cannot cross tenant due to missing scope
5. offline request for one customer cannot obtain another customer's grant/artifact
6. support/global roles are tested for both allowed and denied scope combinations

Tenant isolation regression tests are release blockers.