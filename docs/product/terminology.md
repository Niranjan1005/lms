# Terminology

Terms in this handbook are normative. UI labels may be friendlier, but implementation and APIs should preserve these distinctions.

| Term | Meaning | Must not be confused with |
|---|---|---|
| Customer / Tenant | Commercial owner/security scope | Site or device |
| Site | Logical/physical deployment location owned by customer | Device owner |
| Device | Registered cryptographic edge/server identity | Site |
| Enrollment Authorization | Short-lived/single-use permission to register a device | License/grant |
| Registration | Establishes device identity/ownership | Licensing or capacity approval |
| Entitlement | Central commercial right purchased/granted to customer | Device executable permission |
| Entitlement Pool | Quantity/right available for allocation | Active workload capacity |
| Allocation | Distribution of pooled entitlement to device/site scope | Grant artifact |
| Grant | Signed device-bound executable authorization derived from entitlement/allocation/policy | Entitlement/contract |
| Grant Revision | Monotonic version in a grant lineage | Software release version |
| Supersession | Explicit replacement of an older grant | Additive grant stacking |
| Trial Grant | Time-limited signed grant | UI trial flag |
| Commercial Expiry | End of paid/perpetual-defined commercial term | Offline freshness |
| Offline Freshness | How long device may operate without authorized sync | Commercial term |
| Grace | Restricted recovery period after expiry/staleness according to policy | Paid extension |
| Check-in | Device synchronization/evidence exchange | Commercial renewal |
| Rehost | Approved rebinding after major identity/hardware/key change | Silent transfer |
| Transfer | Approved ownership/site context change | Rehost |
| Feature / Capability | Licensable functional unit | Package/release |
| Release | Versioned application/feature/UI/runtime package metadata | Model release |
| Model Release | Independently versioned encrypted AI model artifact | Feature entitlement |
| Release Set | Coherent application/feature/UI/runtime/model/config snapshot | Single binary |
| Deployment Job | Central orchestration intent across targets | One device installation result |
| Installation Receipt | Device evidence of install/health/rollback result | Central deployment request |
| Capacity Assessment | Combined workload feasibility result | Licensed quantity |
| Benchmark Profile | Versioned measured performance evidence | Live utilization snapshot |
| Resource Snapshot | Time-specific local RAM/GPU/thermal/workload evidence | Benchmark |
| Compatible | Technical dependency/platform requirements satisfied | Capacity-valid or licensed |
| Capacity Validated | Workload feasible under required performance/headroom policy | Commercially licensed |
| Marketplace | Discovery/trial/purchase-request capability | OTA/install authority |
| OTA | Delivery/install/rollback orchestration | Commercial purchase |
| Offline Request | Device-signed request bound to nonce/request ID | Reusable activation file |
| Offline Response | Centrally signed device/request-bound grant/package response | Generic package |
| Relay | Transport convenience for offline transfer | Signing/licensing authority |
| Audit Event | Durable record of significant action/state change | Debug log |
| Telemetry | High-volume operational/usage analytics stream | Transactional licensing truth |

## State phrase rules

Use `Issued`, `Delivered/Imported`, and `Accepted/Active` separately. Use `Licensed`, `Compatible`, `Capacity Validated`, and `Installed/Healthy` separately. Avoid generic `Active` when the specific domain state matters.