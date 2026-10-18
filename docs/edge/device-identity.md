# Device Identity & Hardware Change Policy

Device identity binds grants, offline requests and lifecycle records to a cryptographic principal while tolerating legitimate hardware maintenance.

## Identity material

- device-generated asymmetric key pair
- stable device ID assigned by LMS
- registered public key + key ID/history
- versioned weighted hardware fingerprint
- hardware inventory snapshot
- MAC/network identifiers as supporting evidence only

## Enrollment

1. Device generates key pair locally.
2. Admin/LMS creates short-lived single-use enrollment authorization.
3. Device submits token, public key, fingerprint, inventory and product context.
4. Central validates token/customer/product/duplicate identity.
5. Central binds device ID to customer and key.
6. Registration audit event is recorded.

Private key does not leave the device during normal enrollment.

## Fingerprint design

Fingerprint implementation is versioned. Inputs are weighted by stability/identity value rather than exact concatenated hash equality. The raw data needed for support/change evaluation is handled according to security/privacy policy.

### Typical lower-weight/minor changes
- RAM upgrade/replacement
- storage replacement
- NIC replacement
- added accelerator while core identity remains consistent

### Typical major changes
- motherboard/system identity replacement
- device private-key loss/recreation
- multiple core identity attributes change beyond threshold
- evidence strongly suggests cloning/identity duplication

## Decision outcome

~~~text
MATCH -> continue
MINOR_CHANGE -> audit + compatibility/capacity revalidation
MAJOR_CHANGE -> REHOST_REQUIRED
SUSPECT_DUPLICATE -> quarantine/review
~~~

## Key rotation

Normal key rotation, if supported, must authenticate with the existing device identity or an approved recovery/rehost workflow and retain key history. A new key must not silently create a second device or inherit rights without validation.

## Rehost flow

~~~mermaid
flowchart TD
    A[Identity mismatch detected] --> B{Minor / Major / Suspicious}
    B -->|Minor| C[Revalidate compatibility/capacity]
    C --> D[Continue + audit]
    B -->|Major| E[REHOST_REQUIRED]
    B -->|Suspicious| Q[Quarantine / support-security review]
    E --> F[Request + maker-checker approval]
    F --> G[Register replacement identity]
    G --> H[Reconcile allocation + supersede old grant]
    H --> I[Retire old key/binding]
~~~

## Cloning protection

Central detects duplicate/contradictory key/fingerprint/customer assignments. Edge grants are bound to registered device identity and revision. MAC spoofing alone cannot satisfy identity.

## Related SDR

`SDR-DEV-005` through `SDR-DEV-011`