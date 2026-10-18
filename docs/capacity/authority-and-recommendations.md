# Capacity Authority & Recommendation Rules

## Authority split

**Central Capacity Engine** performs advisory pre-assessment using reported inventory and benchmark profiles.

**Local Capacity Engine** is authoritative for actual activation because it sees current runtime, active streams, drivers, local resources and installed components.

## Activation gate

A feature may activate only when:
1. grant is valid
2. compatibility constraints pass
3. required package/model is installed and healthy
4. local combined-workload capacity validation passes for the selected configuration

## Recommendation mode

The engine recommends; it does not silently reconfigure commercial use.

Example for licensed People Counting 8 + PPE 4 when full combined workload fails:
- PC 8 + PPE 2
- PC 4 + PPE 4
- reduce FPS/resolution
- select optimized model/runtime
- move one workload to another device
- upgrade hardware

The customer/admin explicitly chooses an allowed recommendation. Purchased entitlement remains People Counting 8 + PPE 4 unless a commercial change is separately made.

## Confidence and evidence

Assessment records should include benchmark profile/version, inventory version, workload inputs, result, limiting resource, recommendations and confidence/evidence quality.