# Security Architecture

Security is a cross-cutting architecture concern, not a release checklist. The LMS security model protects commercial rights, customer isolation, device trust, software/model integrity and recoverability across connected and air-gapped deployments.

## Security objectives

1. Only authorized humans and registered devices may interact with LMS.
2. A valid commercial entitlement alone is not enough to execute a feature; the device must hold a valid signed grant.
3. License/grant issuance must be impossible without the protected signing boundary.
4. Software/model artifacts must be authenticated before install or decryption.
5. Cross-customer data access is treated as a security-critical failure.
6. Offline packages must remain safe when moved through untrusted media/relay systems.
7. Device-local enforcement must resist replay/rollback and fail closed for unauthorized analytics.
8. Recovery must remain possible without placing production signing keys in normal backups.
9. Security controls must remain operable in SaaS and customer-hosted deployments.

## Security domains

| Domain | Primary controls |
|---|---|
| Human identity | OIDC/SSO target, MFA for privileged access, session controls, break-glass governance |
| Device identity | device-generated asymmetric key, enrollment authorization, versioned hardware fingerprint |
| Authorization | deny-by-default RBAC, tenant/customer/site/device scope, maker-checker |
| Grant trust | deterministic canonicalization, isolated license signing, revision/supersession, anti-rollback |
| Release trust | separate release signing key, immutable manifest, artifact hash/signature |
| Model protection | encrypted model artifact, envelope encryption, device/deployment-authorized key wrapping |
| Data protection | TLS, encryption at rest where supported, secret separation, backup encryption |
| Offline trust | signed request/response, nonce/request binding, anti-replay, bounded/quarantined package parsing |
| Edge enforcement | protected local key/state, runtime authorization, trusted time, quantity enforcement |
| Tenant isolation | scope propagation, ownership validation, negative isolation tests |
| Supply chain | PR review, SAST/SCA/secret scan, SBOM, build provenance, signed releases |
| Detection/response | security audit events, alerts, incident playbooks, evidence preservation |

## Trust model

~~~mermaid
flowchart LR
    U[Human User] -->|OIDC/password during bootstrap| API[LMS API]
    D[Device Identity Key] -->|signed enrollment/check-in| API
    API -->|authorized signing request| LS[License Signing Boundary]
    API -->|authorized release signing request| RS[Release Signing Boundary]
    API --> DB[(PostgreSQL)]
    API --> AR[(Artifact Repository)]
    AR --> EDGE[Edge Update Manager]
    LS --> EDGE
    RS --> EDGE
    EDGE --> LA[License Agent]
    LA --> RT[Protected Analytics Runtime]
~~~

The LMS application never possesses raw production signing private keys.

## Security decision precedence

1. Approved security ADRs.
2. Security control baseline.
3. Product/business policy where it does not weaken non-relaxable controls.
4. Deployment-specific configuration.

Customer/device overrides cannot weaken a control explicitly marked non-relaxable.

## Known boundary

A root/administrator-compromised edge host cannot be made fully tamper-proof in software alone. LMS therefore focuses on cryptographic authorization, protected local state where practical, integrity verification, auditability and bounded offline authorization rather than claiming impossible absolute protection.