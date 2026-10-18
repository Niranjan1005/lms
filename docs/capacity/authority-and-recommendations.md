# Capacity Authority & Recommendation Rules

Capacity answers whether the selected combined workload can meet required performance on the actual device. It never decides what the customer commercially owns.

## Authority split
### Central Capacity Engine
Performs advisory pre-assessment using latest reported stable inventory, workload definitions and approved benchmark profiles. It is useful for planning, Marketplace previews and deployment targeting.

### Local Capacity Engine
Is authoritative for actual activation because it sees current drivers/runtime, installed model/app versions, active streams, dynamic resource pressure and thermal state.

## Activation gate
A protected feature may activate only when:
1. signed grant is valid
2. technical compatibility passes
3. required application/model is installed
4. health/warm-up passes
5. local combined-workload capacity result permits the selected configuration

## Results
`PASS` — meets target/headroom policy.  
`WARNING` — feasible only with reduced confidence/headroom or an allowed acknowledgement/configuration.  
`FAIL` — selected configuration does not meet the minimum target.  
`STALE` — evidence is no longer valid for current hardware/runtime/workload/benchmark state.

## Recommendation mode
The engine recommends; it never silently changes commercial entitlement or active workload settings.

Example: licensed People Counting 8 + PPE 4 but full combined workload fails.
Possible recommendations:
- PC 8 + PPE 2
- PC 4 + PPE 4
- lower FPS
- lower resolution
- alternate decode path
- optimized model/runtime
- move PPE to second device
- hardware upgrade

The customer/admin selects an allowed recommendation. Selected active configuration is persisted separately from purchased rights.

## Recommendation requirements
Each recommendation should state recommended configuration, limiting resource/reason codes, expected performance/headroom where supported, benchmark confidence, entitlement impact and local revalidation requirement.

## Overrides
Normal FAIL blocks activation. Exceptional capacity override, if policy permits it, is scoped, time/revision-limited, maker-checker approved and audited. It may not bypass hard incompatibility, invalid signatures or missing required runtime.

## Evidence
Assessment records benchmark profile/version, inventory version/hash, workload hash, release/model/runtime versions, dynamic snapshot, result, limiting resources, headroom, confidence, recommendations and selected option.

## Staleness
Hardware, driver/runtime, app/model, camera/workload or materially changed benchmark inputs make prior assessment stale and trigger re-evaluation.

## Related SDR/ADR
`SDR-CAP-001` through `SDR-CAP-011`; ADR-012