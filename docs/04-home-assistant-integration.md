# 04 · Home Assistant Integration

[← Back to README](../README.md)

## AsusRouter, not ASUSWRT

| | ASUSWRT (core) | **AsusRouter (HACS)** |
|---|---|---|
| Connection | SSH | The router's web API (HTTPS) |
| Client details | Presence, IP, MAC | Presence, IP, MAC, **connection type, band, RSSI**, last activity |
| AiMesh nodes | No | **Per-node connected status** |
| Router health | Basic | CPU per core, memory, temperatures, traffic per interface |

The router's web access was set to **HTTPS only** first; the integration connects with SSL on the router's HTTPS port.

**Set-up choices:** device trackers on, no filter; "store clients list in attributes" **off** (it puts the whole client list into one sensor's attributes on every update, bloating the database); 30 s updates; device considered away 45 s after it's last seen; monitored interfaces WAN, wired, 2.4 GHz and 5 GHz; device-connected events on, per-device disconnect/reconnect events off (noise).

## Migration from ASUSWRT
1. A template listed every ASUSWRT entity, which people used them, and a search pattern; a `grep` across automations, scripts, scenes, configuration and dashboard storage found **two** uses (a recorder exclusion and one dashboard card).
2. Both were moved to AsusRouter entity IDs, then ASUSWRT was deleted.
3. The access points' old client entries (from their standalone days) and an AP-mode integration entry were deleted.

## Tracker policy

| Enable | Skip / handle carefully |
|---|---|
| Fixed devices: heating hubs, gateways, safety devices, lights, TVs, consoles, printers, appliances | Phones, watches and tablets until their **private Wi-Fi address** is set to **Fixed** on the home networks (otherwise each appears twice and trackers are unreliable) |
| Wired devices (presence only: no RSSI) where uptime matters | Unknown devices with a locally administered (random) MAC: identify, then disable or delete |

Trackers enabled with a device created per tracker produce a repair ("entity has an area but no name of its own"): fix by setting **Use device area** on the entity.

## Diagnostic templates
[config/templates/](../config/templates/): every Wi-Fi client with its RSSI; trackers grouped by integration entry; a device found by MAC with all attributes.
