# API Standards

- HTTPS outside local development.
- Versioned base path /v1.
- JSON request/response.
- Structured error envelope.
- Correlation ID.
- Idempotency key on issuance/activation/import/payment-result workflows.
- Explicit tenant/customer authorization.
- Pagination on collections.
- UTC ISO-8601 timestamps.

Proposed endpoints:

~~~text
POST /v1/devices/register
POST /v1/devices/{id}/hardware-inventory
POST /v1/devices/{id}/capacity-assessments
POST /v1/activations
POST /v1/devices/{id}/check-ins
POST /v1/activation-requests/import
POST /v1/installations/receipts
~~~