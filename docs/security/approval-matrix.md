# Security & Privileged Action Matrix

| Action | Minimum role | Second approval | Audit |
|---|---|---|---|
| View customer/device state | Support / Customer Admin scoped | No | Access log |
| Allocate within entitlement pool | Customer/Vendor Admin scoped | Normally no | Yes |
| Increase entitlement | Commercial/Product Admin | Yes unless ERP-approved automation | Yes |
| Issue exceptional perpetual/custom grant | Product Admin | Yes | Yes |
| Rehost after motherboard/device-key change | Support/Admin | Yes | Yes |
| Publish Development/QA release | Developer/Release Manager | No | Yes |
| Promote Stable/LTS | Release Manager | Yes, QA/Security gate | Yes |
| Override capacity/security block | Privileged Admin | Yes | Yes |
| Rotate signing key | Security/DevOps | Yes | Yes |
| Revoke grant/device | Admin/Support policy | High-impact cases yes | Yes |

Development roles may create/test plugins and artifacts only in non-production channels unless separately authorized.