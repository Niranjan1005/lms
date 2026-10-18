# Local Component Interfaces

Local components must interact through explicit contracts so product teams do not bypass licensing or update controls.

## License Agent API

Suggested local-only interface:

~~~text
GET  /local/v1/license/status
POST /local/v1/license/import
POST /local/v1/license/check
GET  /local/v1/features/effective
~~~

`license/check` inputs feature, requested quantity/scope, product context and optional workload reference; output is allow/deny/restricted with reason code and effective grant revision.

## Capacity Engine API

~~~text
POST /local/v1/capacity/assess
GET  /local/v1/capacity/latest
~~~

Inputs include current resource snapshot, existing workloads, proposed workloads and benchmark profile version. It returns pass/warning/fail plus recommendations; it never changes purchased rights.

## Update Manager API

~~~text
POST /local/v1/releases/import
POST /local/v1/releases/install
POST /local/v1/releases/rollback
GET  /local/v1/releases/status
GET  /local/v1/models/inventory
~~~

Only the Update Manager may activate a release set. Product services must not unpack arbitrary marketplace files directly.

## Runtime adapter contract

Analytics services must ask the License Agent for authorization at actual execution boundaries. UI state may mirror authorization but cannot be the enforcement layer.

## Local persistence

Protected local state should include accepted grant revision/sequence, last-known trusted time, current release set, rollback release set, installed model inventory and latest signed receipt queue.