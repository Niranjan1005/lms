# Database Schema — Detailed Baseline

The logical model is normalized around commercial truth, device identity, evidence, release management and lifecycle. JSON columns are used only for bounded/extensible attributes, not as a substitute for core relational integrity.

## Tenant and topology

| Table | Key fields | Notes |
|---|---|---|
| customers | customer_id, name, status | Commercial owner. |
| sites | site_id, customer_id, name, timezone, status | Logical/physical deployment site. |
| devices | device_id, customer_id, product_id, public_key_id, fingerprint_hash, status | Device ownership is customer-level. |
| device_site_assignments | assignment_id, device_id, site_id, type, valid_from, valid_until, status | Supports multi-site servers. |
| device_keys | key_id, device_id, public_key, algorithm, status, created_at | Key history and rotation metadata. |

## Commercial licensing

| Table | Key fields | Notes |
|---|---|---|
| entitlements | entitlement_id, customer_id, product_id, term_type, starts_at, expires_at, status | Commercial right. |
| entitlement_items | item_id, entitlement_id, feature_id, quantity_type, quantity, policy_id | Pool definition. |
| allocations | allocation_id, item_id, device_id/site_id, quantity, status, revision | Distribution of pooled rights. |
| grants | grant_id, entitlement_id, device_id, grant_type, revision, valid_from, valid_until, status | Device-bound executable right. |
| grant_constraints | constraint_id, grant_id, key, operator, value_json | Dynamic limits without product-specific columns. |
| grant_dependencies | grant_id, requires_grant_id, dependency_policy | Base/add-on relation. |
| grant_supersessions | old_grant_id, new_grant_id, effective_at | Explicit replacement chain. |
| license_artifacts | artifact_id, grant_id, format_version, key_id, hash, issued_at | Signed serialized artifact. |

## Hardware and capacity

| Table | Key fields | Notes |
|---|---|---|
| device_hardware_inventory | inventory_id, device_id, collected_at, schema_version, cpu_json, gpu_json, memory_json, storage_json, os_runtime_json, inventory_hash | Stable/versioned profile snapshot. |
| device_resource_snapshots | snapshot_id, device_id, captured_at, ram_available, gpu_utilization, gpu_memory_used, temperature, active_streams, workload_hash | Dynamic runtime evidence. |
| workload_profiles | workload_id, device_id/site_id, feature_id, model_id/version, camera_count, resolution, fps, codec, decode_path, backend, precision, target_json, workload_hash | Reproducible workload definition. |
| benchmark_profiles | benchmark_id, hardware_class, feature_id, model_id/version, runtime_dimensions_json, workload_dimensions_json, metrics_json, thresholds_json, confidence_class, version, status | Governed measured evidence. |
| benchmark_profile_approvals | approval_id, benchmark_id, requester_id, approver_id, status, approved_at | Maker-checker/evidence lifecycle where required. |
| capacity_assessments | assessment_id, device_id, inventory_id, resource_snapshot_id, workload_hash, benchmark_version, result, limiting_resources_json, compatibility_json, headroom_json, confidence, recommendations_json, assessed_at, stale_at | Central/local assessment evidence. |
| capacity_recommendation_selections | selection_id, assessment_id, selected_option_json, actor_id, selected_at | Records operator-selected active configuration. |
| capacity_overrides | override_id, assessment_id, device_id, workload_hash, reason, requester_id, approver_id, valid_until, status | Exceptional, scoped, auditable override. |

## Marketplace, release and OTA

| Table | Key fields | Notes |
|---|---|---|
| features | feature_id, product_id, code, status | Catalog feature. |
| feature_releases | release_id, feature_id, version, channel, status | Feature version. |
| artifact_packages | artifact_id, release_id, type, version, uri, hash, signature_ref | App/UI/runtime artifact metadata. |
| models | model_id, code, status | Model identity. |
| model_releases | model_release_id, model_id, version, channel, encryption_profile, hash | Independent model lifecycle. |
| release_dependencies | release_id, dependency_type/id, version_range | Compatibility graph. |
| deployment_jobs | job_id, target_scope, release_set_id, policy_snapshot, status | Orchestration. |
| deployment_targets | target_id, job_id, device_id, status, attempts | Per-device rollout state. |
| installation_receipts | receipt_id, device_id, release_set_id, result, health_status, installed_at | Final device evidence. |

## Lifecycle and governance

| Table | Key fields | Notes |
|---|---|---|
| trial_eligibility | eligibility_id, customer_id, feature_id, policy_version, status | Dynamic trial control. |
| purchase_requests | request_id, customer_id, feature_id, requested_term, status | Not an authorization by itself. |
| renewals | renewal_id, entitlement_id, requested_at, approved_at, status | Commercial lifecycle. |
| device_checkins | checkin_id, device_id, checked_in_at, accepted_revision, result | Offline freshness evidence. |
| revocations | revocation_id, object_type, object_id, reason, effective_at | Central revoke state. |
| audit_events | event_id, actor_id, action, object_type, object_id, before_ref, after_ref, result, created_at | Immutable operational audit. |

## Mandatory database controls

- All business tables carry customer/tenant ownership directly or through an enforceable FK path.
- Allocation updates and grant supersession occur in a single business transaction where possible.
- Idempotency keys have unique constraints at the workflow boundary.
- Mutable business objects carry revision/version columns for optimistic concurrency.
- Audit events are append-only.
- UTC is used for persisted timestamps; site timezone is display/scheduling context only.