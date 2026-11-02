# 02 · Conversion Runbook (Standalone AP to AiMesh Node)

[← Back to README](../README.md)

**One access point at a time; the house never loses Wi-Fi.** Done for all four RP-AX58s on 2 Nov 2026.

## Once, on the router
1. **Ethernet Backhaul Mode: On** (AiMesh → System Settings). There's no separate "enable AiMesh": a router in router mode is the AiMesh router.
2. Check the network names and passwords on each access point **match the router's**. If they differ, devices on that access point lose their network after conversion.

## Per access point
1. **Record its wireless settings** (both bands: channel, bandwidth, extension channel, Smart Connect, security), its IP and admin login. This is the rollback record.
2. **Operation Mode → AiMesh Node** (or factory reset). Its settings are wiped either way. Leave the cable in.
3. Router: **AiMesh → Topology → Add AiMesh Node** → select it → Connect. It can sit at 0% for a few minutes.
4. Check in Topology: **connection quality**, **Uplink: Ethernet**, clients appearing.
5. Firmware: compare with the other nodes; update via the router's Firmware Upgrade page (**Upload** per node).
6. Next access point.

## Pitfalls met

| Symptom | Cause | Fix |
|---|---|---|
| Node page: "Unable to connect to the Parent AP", 0 clients | Node firmware far older than the router's | Update the node firmware from the router (manual upload); it then synced |
| Node's own web page rejects its old password; IP changed | A node takes the router's admin login and gets its address by DHCP | Manage nodes from the router's AiMesh pages |
| DHCP reservations ignored | Reservation held the access point's standalone-mode MAC | Reserve the node's **Ethernet MAC** (Network tab, fronthaul section), then reboot the node |
| Nodes absent from the client list | AiMesh nodes aren't listed as clients | Find the node's IP in Topology → Network → Uplink |
| Other access points briefly unreachable during pairing | Router reconfiguring for the new node | Wait for pairing to finish |
| Router firmware "!" | A USB disk notice, not an update | Check updates on Administration → Firmware Upgrade |
| Location names | The router only offers fixed presets | Name the nodes in Home Assistant (device name + area) |

## Rollback (per node)
Topology → node → **Remove Node**, then set it up as a standalone access point with the recorded settings and its old IP reservation.
