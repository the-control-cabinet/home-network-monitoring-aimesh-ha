# 05 · Cards and Alerts

[← Back to README](../README.md)

| Item | File | Behaviour |
|---|---|---|
| Wi-Fi signal card | [config/cards/wifi-signal-card.yaml](../config/cards/wifi-signal-card.yaml) | Every device with an RSSI, weakest first, banded 🟢 ≥ −60 · 🟡 −61 to −67 · 🟠 −68 to −75 · 🔴 < −75 dBm |
| Access point card | [config/cards/access-point-card.yaml](../config/cards/access-point-card.yaml) | Finds the nodes by model; name, area, online/offline and how long |
| Weak-signal alert | [config/automations/wifi-weak-signal-alert.yaml](../config/automations/wifi-weak-signal-alert.yaml) | Any device below −75 dBm for 30 min; once per episode |
| AP-offline alert | [config/automations/access-point-offline-alert.yaml](../config/automations/access-point-offline-alert.yaml) | Any node offline for 5 min |

**Markdown cards use `content: |`.** A folded scalar (`>-`) joins the table's lines and breaks the rows.

**First use:** the gateway card in the Evohome repo combines its RF traffic with this repo's presence and RSSI for the same device. During every stall the gateway stayed on Wi-Fi at −62 to −64 dBm, which ruled out the network.
