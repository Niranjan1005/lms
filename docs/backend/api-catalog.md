# API Endpoint Catalogue

This is the initial endpoint inventory for design and ownership. Exact request/response schemas are finalized in OpenAPI before implementation freeze.

## Identity & access

~~~text
POST   /v1/auth/login
POST   /v1/auth/refresh
POST   /v1/auth/logout
GET    /v1/me
GET    /v1/roles
~~~

## Customers and sites

~~~text
GET    /v1/customers
POST   /v1/customers
GET    /v1/customers/{customer_id}
PATCH  /v1/customers/{customer_id}
GET    /v1/customers/{customer_id}/sites
POST   /v1/customers/{customer_id}/sites
PATCH  /v1/sites/{site_id}
~~~

## Devices and enrollment

~~~text
POST   /v1/enrollment-authorizations
POST   /v1/devices/register
GET    /v1/devices/{device_id}
POST   /v1/devices/{device_id}/hardware-inventory
POST   /v1/devices/{device_id}/resource-snapshots
POST   /v1/devices/{device_id}/site-assignments
POST   /v1/devices/{device_id}/transfer-requests
POST   /v1/devices/{device_id}/rehost-requests
POST   /v1/devices/{device_id}/decommission
~~~

## Entitlements, allocations and grants

~~~text
GET    /v1/entitlements
POST   /v1/entitlements
GET    /v1/entitlements/{id}
POST   /v1/entitlements/{id}/allocations
PATCH  /v1/allocations/{id}
POST   /v1/grants/issue
POST   /v1/grants/{id}/revoke
GET    /v1/devices/{device_id}/grants
~~~

## Capacity

~~~text
POST   /v1/devices/{device_id}/capacity-assessments
GET    /v1/devices/{device_id}/capacity-assessments
GET    /v1/benchmark-profiles
POST   /v1/benchmark-profiles
~~~

## Marketplace, trials and purchase

~~~text
GET    /v1/marketplace/features
GET    /v1/marketplace/features/{feature_id}
POST   /v1/trials
POST   /v1/purchase-requests
GET    /v1/purchase-requests/{id}
POST   /v1/purchase-requests/{id}/approve
~~~

## Releases, models and artifacts

~~~text
GET    /v1/releases
POST   /v1/releases
POST   /v1/releases/{id}/artifacts
POST   /v1/releases/{id}/promote
GET    /v1/models
POST   /v1/models
POST   /v1/models/{id}/releases
POST   /v1/model-releases/{id}/promote
~~~

## Deployment and OTA

~~~text
POST   /v1/deployments
GET    /v1/deployments/{id}
POST   /v1/deployments/{id}/cancel
POST   /v1/installations/receipts
GET    /v1/devices/{device_id}/release-inventory
~~~

## Lifecycle

~~~text
POST   /v1/renewals
POST   /v1/renewals/{id}/approve
POST   /v1/devices/{device_id}/check-ins
POST   /v1/revocations
GET    /v1/notifications
~~~

## Offline exchange

~~~text
POST   /v1/offline/requests/import
GET    /v1/offline/responses/{request_id}
POST   /v1/offline/receipts/import
~~~

## Audit and integration

~~~text
GET    /v1/audit-events
POST   /v1/integrations/erp/events
GET    /v1/integrations/erp/reconciliation
~~~

## API ownership rule

Every endpoint has exactly one owning module. Cross-module orchestration belongs in an application service/use-case layer, not in controllers directly.