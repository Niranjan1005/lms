# RBAC & Permission Catalogue

RBAC must be deny-by-default and customer-scoped. Roles are bundles of permissions; authorization checks should evaluate permission + scope, not role name alone.

## Initial roles

| Role | Typical scope | Purpose |
|---|---|---|
| Vendor Super Admin | global | Emergency/platform administration |
| Product Admin | global/product | Catalog, entitlement policy, commercial configuration |
| Release Manager | product/release | Release promotion and rollout |
| Security Approver | global/security | Maker-checker for sensitive security operations |
| Developer | non-production product/channel | Publish test plugins/models/releases |
| Support Engineer | assigned customers | Diagnostics, registration/rehost workflows |
| Customer Admin | customer | Sites, devices, allocations, update policy |
| Site Admin | site | Site-scoped devices and operations |
| Auditor / Read Only | assigned scope | Read-only reporting and audit |

## Permission families

~~~text
customer.read / customer.manage
site.read / site.manage
device.read / device.enroll / device.transfer / device.rehost / device.decommission
entitlement.read / entitlement.manage / entitlement.override
allocation.read / allocation.manage
grant.read / grant.issue / grant.revoke / grant.override
trial.read / trial.start / trial.extend
catalog.read / catalog.manage
release.read / release.publish_dev / release.promote_stable / release.promote_lts
model.read / model.publish / model.promote
deployment.read / deployment.create / deployment.override
capacity.read / capacity.assess / capacity.override
audit.read / audit.export
security.approve_sensitive_action
admin.user_manage / admin.role_manage
~~~

## Scope evaluation

Permission checks evaluate:
1. authenticated principal
2. effective permissions
3. customer/product/site/device scope
4. object status and policy
5. maker-checker requirement if sensitive

A Vendor role does not bypass customer scoping accidentally; global access is explicit.

## Developer restrictions

Developer role may create and test plugins/releases/models only in Development/QA/Internal channels by default. Production Stable/LTS promotion requires Release Manager plus approval gates.