# Home Assistant — Smart Home + Zigbee Mesh Diagnostics

> Part of [homelab-hub](https://github.com/YOUR_USERNAME/homelab-hub). Home Assistant instance (v2026.8.1) with door/motion sensors over Zigbee, plus a diagnostic audit of the mesh network itself.

## Overview

Home Assistant runs as part of the lab, currently covering door and motion sensors over a Zigbee mesh, with the setup being steadily expanded. Beyond just adding devices, this repo documents a **read-only diagnostic audit** of the entities, automations, helpers and dashboards, plus a deeper dive specifically into Zigbee mesh health.

## What's in this repo

| Path | Contents |
|---|---|
| `docs/zigbee-mesh-audit.md` | Full write-up: methodology, findings (topology anomalies, weak LQI links, overloaded repeaters, single points of failure), and remediation steps |
| `docs/entity-audit.md` | Read-only audit of entities, automations, helpers and dashboards — what was reviewed and why |
| `config/automations.example.yaml` | Sanitized example automation (door sensor → notification) |
| `scripts/check-zigbee-lqi.md` | How mesh link quality was checked and interpreted |

## Why a mesh audit matters

Zigbee is a mesh network — every powered device (not just the coordinator) can act as a repeater. A mesh that "mostly works" can still have hidden fragility: a single repeater carrying too much traffic, or a sensor with a weak link that only becomes visible when that one repeater goes offline. This audit treats the mesh itself as infrastructure worth diagnosing, not just a black box that either "has signal" or doesn't.

## Key findings (summary — full detail in the audit doc)

- Identified **topology anomalies**: some sensors routing through a longer/weaker path than a shorter one available to them.
- Found **weak LQI (Link Quality Indicator) links** on a subset of devices — flagged for closer monitoring or repeater placement changes.
- Identified **overloaded repeater nodes** — a small number of devices were carrying a disproportionate share of mesh traffic, creating single points of failure.

## Status / Known issues

- Setup is still being expanded (more sensors planned).
- Some of the topology anomalies identified are documented but not yet fully remediated — see the audit doc's "Remediation" section for what's done vs. pending.

## License

MIT — see [LICENSE](LICENSE).
