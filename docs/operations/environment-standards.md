# Environment Standards

Environment separation prevents test code/data/keys from becoming production authority and ensures release evidence is reproducible.

## Environment classes
| Environment | Purpose | Data rule | Release channels | Signing |
|---|---|---|---|---|
| Local Dev | developer iteration | synthetic only | Development | developer-only keys |
| Integration | API/edge/integration tests | synthetic/test | Development/QA | test keys/provider |
| QA | formal functional/regression | synthetic/anonymized | QA/Internal | non-production signing |
| Staging | production-like readiness | anonymized/approved | Internal/Stable candidate | isolated staging keys |
| Production | customer service | real customer data | Stable/LTS | production protected provider |

## Separation requirements
- separate credentials/secrets per environment
- production signing keys never available in lower environments
- production DB credentials never valid in lower environments
- test tenants/devices visibly marked and cannot target production signing/deployment by accident
- environment-specific artifact repositories or strong namespace/policy separation
- production backups not restored to lower environments without approved sanitization
- release promotion records exact source artifact/build rather than rebuilding ad hoc in production

## Configuration
Configuration is provided through environment/deployment/secret manager. Environment-specific values include DB, artifact provider, signing provider, auth/IdP, email, telemetry, external integrations, public URL, CORS/headers and monitoring endpoints.

## Production guardrails
Production mode SHALL fail startup/readiness for dangerous conditions such as known development signing configuration, default/insecure secret, disabled TLS validation on external connections, or unsupported schema version where detectable.

## Networking
Lower environments do not require access to production databases, KMS/HSM or customer networks. Production admin/service interfaces follow deployment security/network policy.

## Time
All environments use reliable time synchronization for realistic expiry/signature testing. Persist UTC; site timezone is used for scheduling/display only.

## Data refresh
Synthetic seed data is preferred. Sanitized production-derived datasets require explicit approval and repeatable sanitization so Confidential/Highly Restricted fields do not leak.

## Environment parity
Staging should exercise the same package, migration and provider interfaces as production even when scaled down. Differences are documented and considered during release approval.

## Access review
Production human/service access is narrower than lower environments and periodically reviewed; emergency access follows break-glass policy.