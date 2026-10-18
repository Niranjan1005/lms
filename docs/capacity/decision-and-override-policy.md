# Capacity Decision & Override Policy

## Default decision mode

The Capacity Engine recommends a feasible configuration. The customer/admin explicitly selects the configuration. The platform must never silently lower camera count, FPS, resolution or purchased entitlement.

## PASS

Activation may proceed if all licensing, compatibility, installation and health gates also pass.

## WARNING

Activation may proceed only if product policy permits warning acceptance. The selected configuration and warning acknowledgement are audited.

## FAIL

Normal activation is blocked. The system presents recommendations such as reduced active workload, lower FPS/resolution, alternative model/runtime, moving workloads, second device or hardware upgrade.

## Exceptional override

If the company chooses to support a capacity override for exceptional cases, it is a privileged maker-checker action and must:
- never change the commercial entitlement
- capture requester, approver, reason and expiry
- bind to a specific device/workload/release/model context
- be time-limited or revision-limited
- generate an audit event
- be visible in support/operations views
- automatically become invalid when material hardware/runtime/workload state changes

A capacity override must not bypass hard technical incompatibility such as unsupported architecture, missing required runtime or invalid package/model signature.

## Recommendation selection

The selected recommendation becomes part of the activation/deployment record so later support can distinguish licensed rights from the operator-selected active configuration.