# Home Network Monitoring: ASUS AiMesh + Home Assistant (Commissioned, Trial Running)

**The Wi-Fi network that the building controls depend on, monitored like plant: four access points converted to AiMesh nodes on Ethernet backhaul so the router reports every client's signal; per-device RSSI, node health and alerts in Home Assistant; and a measured trial of the one trade-off (shared channels).**

[![YouTube](https://img.shields.io/badge/YouTube-The%20Control%20Cabinet-red?logo=youtube)](https://www.youtube.com/channel/UC5Cupmz7vlfcodpCX7k8iuQ)
[![Portfolio](https://img.shields.io/badge/Portfolio-the--control--cabinet-24292f?logo=github)](https://github.com/the-control-cabinet/the-control-cabinet)
![Domain](https://img.shields.io/badge/BMS-IT%2FOT%20network-blue)
![Status](https://img.shields.io/badge/Status-Trial%20running-yellow)

> **The short version:**
> - **Why:** a heating gateway kept dropping out, and nobody could see its Wi-Fi signal. Standalone access points hide their clients; the router saw them all as "wired".
> - **What:** AiMesh with Ethernet backhaul, the AsusRouter integration, a signal card for every Wi-Fi device, a node status card, and alerts for weak signal and an offline access point.
> - **Trade-off:** on these models every node uses the router's channels. A baseline and one-week scan measure whether that costs anything.
> - **First result:** it proved the gateway's dropouts were **not** Wi-Fi (−62 to −64 dBm during every stall).

**Portfolio position:** Supervisory level · head-end and network health. Related: [head-end health](https://github.com/the-control-cabinet/head-end-health-monitoring) · [Evohome gateway reliability](https://github.com/the-control-cabinet/evohome-heating-controls-ramses-integration/blob/main/docs/B6-gateway-reliability.md) · [ESPHome fleet](https://github.com/the-control-cabinet/esphome-fleet-standards) · [O&M pack](https://github.com/the-control-cabinet/om-manual-handover-pack)

---

## Documents

| Doc | Contents |
|---|---|
| [01 Architecture and decision](docs/01-architecture-and-decision.md) | Before and after, why AiMesh, the channel trade-off, options rejected |
| [02 Conversion runbook](docs/02-conversion-runbook.md) | One access point at a time: checks, conversion, pitfalls met, rollback |
| [03 Channel-sharing trial](docs/03-channel-sharing-trial.md) | Baseline and one-week scan method, thresholds, results |
| [04 Home Assistant integration](docs/04-home-assistant-integration.md) | AsusRouter vs ASUSWRT, tracker policy, private MACs, clean-up |
| [05 Cards and alerts](docs/05-cards-and-alerts.md) | Signal card, node card, weak-signal and AP-offline alerts |

## Points

| Point | Source | Use |
|---|---|---|
| Per-device Wi-Fi signal (RSSI), band | AsusRouter device trackers | Signal card, weak-signal alert |
| Per-device presence (home/away) | AsusRouter device trackers | Separates Wi-Fi drops from device hangs |
| Node connected (×4) | AsusRouter AiMesh entities | Node card, AP-offline alert |
| Router CPU, memory, temperature, WAN/LAN/Wi-Fi traffic | AsusRouter sensors | Head-end health |

## Repository layout
```
├── config/cards/          ← Wi-Fi signal card, access point status card
├── config/automations/    ← weak-signal and AP-offline alerts
├── config/templates/      ← diagnostic templates (find by MAC, group by hub, RSSI list)
├── data/                  ← channel trial records
└── docs/                  ← 01-05
```

No SSIDs, MAC addresses, IP addresses or passwords are published.
