# API Standards

## Protocol and versioning

- HTTPS outside local development
- REST/JSON baseline with `/v1` major version prefix
- explicit content type and UTF-8
- UTC ISO-8601 timestamps
- opaque IDs; clients do not parse identifier structure
- breaking semantic changes require new major API version or migration contract

## Authentication principals

Human API calls use the configured human identity/session mechanism. Device APIs use registered device cryptographic identity or an explicitly documented enrollment bootstrap flow. Internal workers use dedicated least-privilege service identities.

## Authorization

Every protected endpoint evaluates permission plus customer/product/site/device/object scope. Client-supplied tenant identifiers never grant access.

## Common headers

~~~text
Authorization: Bearer <token>       # human/service where applicable
X-Request-ID: <uuid>
Idempotency-Key: <opaque-uuid>      # retry-safe write workflows
~~~

Device-signed endpoints may additionally carry key ID/signature/nonce fields in their canonical request envelope.

## Request rules

- schema validation at boundary
- maximum payload/upload sizes
- unknown critical fields rejected where signed canonicalization requires strictness
- pagination/filter limits on collections
- optimistic revision supplied for concurrent mutable resources where needed

## Response rules

Successful responses use a consistent `data` + `meta` envelope. Errors use the stable error model. Security-sensitive failures may intentionally generalize external messages.

## Idempotency

Required for grant issuance, activation, offline import, payment/commercial callbacks, deployment creation and other retried write workflows. Same key + different request hash is rejected.

## Pagination

Cursor pagination is preferred for large/ordered collections. APIs define stable sort order, maximum page size and tenant-scoped filters.

## Long-running operations

Release builds, large deployments, offline bundle generation and other long operations return a job/resource identifier rather than holding an HTTP request open. Job state is durable and observable.

## Compatibility

Additive optional fields are allowed within `/v1`. Removal, type changes, changed meaning, newly required fields or changed security semantics require explicit compatibility handling.

## Endpoint catalogue

The authoritative inventory is maintained in `API Endpoint Catalogue`; generated OpenAPI becomes the executable contract once implementation begins.