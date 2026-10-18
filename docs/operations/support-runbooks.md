# End-to-End Support Runbooks

## Device cannot activate feature

1. Identify customer/site/device and request ID.
2. Check registration state and device ownership.
3. Check entitlement and allocation.
4. Check latest grant issuance/delivery/acceptance state.
5. Check commercial expiry, offline freshness and grace separately.
6. Check device-reported rejection code.
7. Check capacity/compatibility and installed release/model dependencies.
8. If offline, validate request/response pairing and nonce.
9. Apply only approved remediation; do not hand-edit grants.
10. Record resolution/audit reference.

## Offline package rejected

1. Confirm package was created for the same device/request ID.
2. Verify operator did not reuse an older response.
3. Compare device accepted revision vs response revision.
4. Check signature/key trust status.
5. Check release/model compatibility.
6. Export a fresh request if nonce/request expired or state changed.

## Deployment failed and rolled back

1. Confirm rollback health status.
2. Capture installation receipt and request ID.
3. Identify failed stage: download, verify, stage, migration, start, health check.
4. Check disk/dependency/runtime prerequisites.
5. Block release for broader rollout if systemic.
6. Escalate to Release Manager when failure rate crosses rollout threshold.

## Rehost required

1. Confirm major hardware/key identity change.
2. Verify customer/device ownership.
3. Collect previous/new fingerprint evidence.
4. Submit rehost request and required approval.
5. Rebind identity and issue superseding grant.
6. Retire old binding and return/reconcile allocation.

## Renewal approved but device still expired

1. Confirm ERP/commercial approval reached LMS.
2. Confirm new entitlement term and grant revision exist.
3. Check whether device has delivered/imported the new revision.
4. For offline site, produce/import renewed response package.
5. Confirm device accepted revision and generated receipt.

## Signing service unavailable

1. Stop repeated manual issuance attempts.
2. Confirm signing gateway/provider health.
3. Existing valid grants continue according to policy; do not bypass signature requirement.
4. Queue issuance via outbox/retry.
5. Escalate according to incident severity if customer activations/renewals are blocked.