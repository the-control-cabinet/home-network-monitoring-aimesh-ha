# 03 · Channel-Sharing Trial

[← Back to README](../README.md)

**Status: baseline pending.** The trial asks one question: does putting every access point on the router's channels (1 and 36) crowd the air enough to matter?

## Method

1. **Baseline:** at a normal busy time (an evening), scan near **each node and the router** (five spots) with a Windows laptop:
   ```
   netsh wlan show networks mode=bssid > scan-<spot>-<date>.txt
   ```
   Wait about 10 seconds at each spot first so the laptop's list has refreshed.
2. **Record**, for each of the house's access points: channel, signal, connected stations and **Channel Utilization** (the % in brackets) in [data/channel-trial.csv](../data/channel-trial.csv). Note neighbours' networks on the same channels.
3. **During the week:** watch device dropouts, ESP32 reconnects and the weak-signal alert in Home Assistant.
4. **After one week:** repeat at the same spots and time, then compare.

## Thresholds

| Channel Utilization | Reading |
|---|---|
| < 40% | Comfortable |
| 40-60% | Busy: watch |
| > 60% | Congested: act |

## If it fails
In order: lower 2.4 GHz Tx power further; narrow 5 GHz to 40 MHz; return the worst-affected node to standalone on channel 6 or 11 (accepting the loss of visibility for its clients); check later firmware for per-node channel planning.

## Before the change (scan of 2 Nov 2026, one spot)
Channel 1 at 30-34% utilization across three access points; channel 6 at 9%; channel 11 at 29% (shared with neighbours on 11); 5 GHz channel 36 at 8%.

## Results
*To be added after the baseline and the one-week repeat.*
