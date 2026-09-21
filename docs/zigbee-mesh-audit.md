# Zigbee Mesh Diagnostic Audit

## Scope

Read-only diagnostic pass over the Zigbee mesh backing the Home Assistant setup — no devices reconfigured during the audit itself, only observed and mapped. Goal: understand actual mesh health vs. assumed health ("it works" ≠ "it's resilient").

## Methodology

1. **Topology mapping** — pulled the mesh topology (via the Zigbee integration's network map / coordinator diagnostics) to see which device routes through which repeater to reach the coordinator.
2. **Link Quality Indicator (LQI) review** — checked LQI values on each hop, not just "is the device online." A device can report as online while riding a degraded link that will fail intermittently under interference.
3. **Repeater load analysis** — counted how many end devices route through each repeater-capable node, to spot any repeater carrying a disproportionate share of the mesh.
4. **Cross-reference with physical layout** — compared the logical topology against the actual physical placement of devices to sanity-check why certain routing choices were being made by the mesh.

## Findings

### 1. Topology anomalies
Some sensors were routing through a longer/weaker path when a shorter, stronger path was physically available through another repeater. This is a known Zigbee behavior (routes aren't always re-evaluated once established) but worth surfacing rather than assuming the mesh is self-optimizing.

### 2. Weak LQI links
A subset of devices showed LQI values low enough to be flagged for monitoring — not yet failing, but sitting close enough to the threshold where seasonal interference (e.g. Wi-Fi channel changes, new 2.4GHz devices) could push them into drop-outs.

### 3. Overloaded repeater nodes
A small number of repeater-capable devices were carrying a disproportionate share of the mesh's routing — a single point of failure risk: if one of these went offline (power cycle, removed, etc.), a cluster of end devices would need to re-route or could temporarily drop.

## Remediation

| Finding | Status | Action |
|---|---|---|
| Topology anomaly (long routes) | Documented | _Update once addressed — e.g. forced re-pairing closer to a stronger repeater_ |
| Weak LQI links | Monitoring | _Update once addressed — e.g. added repeater, relocated device_ |
| Overloaded repeaters | Documented | _Update once addressed — e.g. added a dedicated repeater to redistribute load_ |

## Why this is worth documenting

Most smart-home writeups stop at "I added a sensor and it works." This audit is meant to show the next level: treating a mesh network as something with measurable health, and being able to read and act on diagnostics like LQI and topology maps — the same underlying skill set as RF/link-quality work in a communications engineering context, just applied to a Zigbee PAN instead of a larger RF system.
