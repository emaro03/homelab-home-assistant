# Entity / Automation / Helper / Dashboard Audit

A read-only pass over the full Home Assistant configuration to understand what actually exists vs. what was assumed to exist — useful after a setup has grown organically over time.

## What was reviewed

- **Entities** — every entity currently registered, flagging unavailable/stale ones (devices removed but never cleaned up in HA).
- **Automations** — checked for overlapping or conflicting automations (e.g. two automations triggering on the same door sensor with different logic).
- **Helpers** — input booleans/numbers/etc. actually referenced somewhere vs. orphaned leftovers from earlier experiments.
- **Dashboards** — whether dashboard cards still point at valid entities.

## Findings summary

_Fill in with your real findings — even a short honest list is valuable, e.g.:_
- N stale entities identified (device removed, entity never deleted)
- N helpers with no automation/dashboard reference
- Any automation logic conflicts found

## Why this matters

Configuration entropy is a real, boring, universal problem in any system that grows over time — not unique to home automation. Doing a periodic audit (and writing down what you found) is the same discipline as a config/infra review in a professional environment.
