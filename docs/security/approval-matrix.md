# Security & Privileged Action Matrix

| Action | Minimum role | Second approval | Audit |
|---|---|---|---|
| View customer/device state | Support / Customer Admin scoped | No | access/security log |
| Allocate within approved entitlement pool | Customer/Vendor Admin scoped | Normally no | Yes |
| Increase/create exceptional entitlement | Product/Commercial Admin | Yes unless approved ERP automation | Yes |
| Issue exceptional perpetual/custom grant | Product Admin | Yes | Yes |
| Extend/repeat trial beyond policy | Product Admin | Yes when outside approved campaign | Yes |
| Rehost after motherboard/device-key change | Support/Admin | Yes | Yes |
| Cross-customer device transfer | Privileged Admin | Yes | Yes |
| Publish Development/QA release | Developer/Release Manager | No | Yes |
| Promote Stable | Release Manager | QA/Security gate according to policy | Yes |
| Designate/promote LTS | Release Manager | Yes | Yes |
| Force broad rollout outside normal policy | Release Manager/Privileged Admin | Yes | Yes |
| Override capacity warning/fail where allowed | Privileged Admin | Yes | Yes |
| Override security block | Security/Privileged Admin | Yes | Yes |
| Rotate/activate signing key | Security/DevOps | Yes | Yes |
| Change edge trust bundle/revoke verification key | Security/Release | Yes | Yes |
| Change model KEK/key-wrapping configuration | Security/DevOps | Yes | Yes |
| Revoke individual grant/device | Admin/Support policy | High-impact cases yes | Yes |
| Mass revoke/suspend customer/fleet | Vendor/Security Admin | Yes | Yes |
| Export global audit/security data | Auditor/Security/Admin | Policy-dependent | Yes |
| Use break-glass access | Designated emergency role | Post-use review; second control where feasible | Mandatory |

## Principles

- requester and approver must be distinct when maker-checker is required
- approval binds to object revision/payload so approved data cannot be silently changed before execution
- expired/rejected/cancelled approvals cannot execute
- high-risk automation must preserve equivalent evidence and policy checks
- development roles remain restricted to non-production release channels by default