# Team RACI

| Area | Primary Owner | Key contributors / accountability |
|---|---|---|
| Customer/site/device registry | Backend | Product, QA |
| Entitlements, allocations & grants | Backend | Product/Commercial, Security, QA |
| Trial/subscription/perpetual/add-on policy | Product/Commercial | Backend, QA, Support |
| Renewal/grace/offline-freshness policy | Product/Commercial | Backend, Support, QA |
| License Agent/runtime enforcement | Edge/Application | Backend, Security |
| Device identity/key storage | Edge/Application | Security, Backend |
| Capacity benchmark matrix | AI/ML Performance | Edge, Backend, QA |
| Capacity engine/recommendations | AI/ML Performance + Backend/Edge | Product, QA |
| Marketplace | Backend/Web | Product, Edge, QA |
| Release/OTA orchestration | Backend + Edge | QA, DevOps, Security |
| Model OTA | AI/ML + Edge | Backend, Security, QA |
| Signing/key custody | DevOps/Security | Backend |
| Artifact repository | DevOps/Backend | Release Manager, Security |
| Release promotion | Release Manager / QA | Engineering, Security, Product as needed |
| ERP integration | Backend | Finance/Commercial, Product |
| Notifications/support workflows | Backend/Support | Product |
| Backup/DR/monitoring | DevOps/Operations | Backend, Security |
| VAPT | Security | All engineering teams |
| Handbook/ADRs | Architecture/Tech Leads | All contributors |

## Approval rule

Normal allocations within an approved entitlement may be single-admin or automated. Sensitive actions such as entitlement increase, large custom/perpetual grants, trial extension, forced LTS, major rehost, security/capacity override and signing-key changes use maker-checker approval.