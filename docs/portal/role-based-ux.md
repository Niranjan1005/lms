# Role-Based Portal UX

The portal must present role-appropriate actions while backend authorization remains authoritative.

## Vendor Super Admin

Views: global customers, products, incidents, signing/release health, privileged audit. Actions are tightly controlled and high-risk changes require approval.

## Product Admin

Views/actions: product/feature catalog, entitlement policy, trial campaigns, commercial configuration and approved exceptions.

## Release Manager

Views/actions: release candidates, QA/security evidence, channels, rollout plans, deployment status, rollback and LTS designation.

## Security Approver

Views/actions: pending maker-checker requests, signing-key changes, rehost/security overrides, VAPT/security disposition.

## Customer Admin

Views/actions: customer sites/devices, entitlement pool, allocations, trials, purchase requests, renewals, update policy, capacity recommendations.

## Site Admin

Views/actions: site-scoped devices, workload/capacity state, maintenance window, deployment progress and permitted site allocations.

## Support Engineer

Views/actions: diagnostic state, request IDs, grant delivery/acceptance, offline package state, rehost/renewal workflows and safe support actions. No hidden broad commercial override.

## Read Only / Auditor

Views: status, reports and audit history without mutation.

## Critical UX rules

- Always distinguish registration, license, capacity and install/health status.
- Always distinguish issued, delivered and accepted grants.
- Show why an action is blocked with safe error/reason codes.
- Offline export/import screens display request ID, target device, expiry, package version and reconciliation status.
- Capacity screens show purchased rights separately from selected active configuration and recommendation.
- Privileged actions show approval state and second-approver requirement before execution.