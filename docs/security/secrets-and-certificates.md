# Secrets, Certificates & Service Credentials

## Secret categories

- database credentials
- SMTP/webhook/integration credentials
- OIDC client secrets where applicable
- artifact-storage credentials
- KMS/HSM/signing service authentication
- telemetry/export credentials
- internal service tokens

Signing private keys and model KEKs are not ordinary application secrets; they remain inside the protected cryptographic provider.

## Storage

Production secrets are injected from approved secret-management/deployment mechanisms, not committed in source, baked into images/packages or stored in documentation.

## Rotation

Every production secret type has an owner and rotation/revocation procedure. Applications should support overlap where needed so rotation does not require service outage.

## Certificate lifecycle

- certificates have tracked owner and expiry
- automated renewal preferred where deployment allows
- certificate validation never disabled in production
- hostname/SAN validation required
- expired/revoked certificate failures alert operations
- private certificate keys receive restricted filesystem/secret-store permissions

## Service credentials

Use separate credentials by environment and service. Avoid one shared superuser credential across LMS, workers and integrations.

## Compromise response

Suspected secret leakage triggers revocation/rotation, impact review, log/audit search, dependent credential rotation where necessary and incident documentation.