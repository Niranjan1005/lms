# Device Identity & Hardware Change Policy

## Identity material

- device-generated asymmetric key pair
- centrally registered public key
- versioned hardware fingerprint
- MAC/network identifiers as supporting evidence only

## Fingerprint policy

Fingerprint comparison is weighted/tolerant rather than exact equality.

Minor changes normally trigger compatibility revalidation but do not require rehost:
- RAM upgrade/replacement
- storage replacement
- NIC replacement
- added accelerator where identity remains stable

Major changes enter `REHOST_REQUIRED`:
- motherboard replacement
- device private key loss/recreation
- multiple core identity attributes change beyond tolerance

## Rehost flow

~~~mermaid
flowchart TD
    A[Identity mismatch detected] --> B{Minor or Major?}
    B -->|Minor| C[Revalidate compatibility/capacity]
    C --> D[Continue with audit]
    B -->|Major| E[REHOST_REQUIRED]
    E --> F[Admin / maker-checker approval]
    F --> G[Register replacement identity]
    G --> H[Issue superseding device grant]
    H --> I[Return old allocation / retire old binding]
~~~