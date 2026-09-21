# Checking Zigbee LQI

Depending on your integration:

**ZHA (built-in):** Settings → Devices & Services → ZHA → Network Visualization Map. Each connection line shows LQI; the map itself highlights the routing topology described in `docs/zigbee-mesh-audit.md`.

**Zigbee2MQTT:** the web frontend's map view (`/`) shows the same information — each device's LQI to its parent, and the overall mesh graph. Values below ~50-60 are worth investigating; consistently low values or intermittent drops on a device point to either distance, interference, or an overloaded parent repeater.

Cross-reference low-LQI devices against the topology map to see if they're routing through a repeater that's already carrying a lot of the mesh's traffic — that combination is what actually causes visible reliability issues, more than either factor alone.
