# MTTL-W01 standalone firmware assessment — 2026-10-18

## Finding
Candidate: https://github.com/af950833/mttl_w01_standalone
Upstream release: 2.0.17 (2026-10-18), firmware file comMTTL-W01_2.0.17.fwr.
Source: https://github.com/af950833/mttl_w01_standalone/blob/main/README_EN.md

This firmware is purpose-built for LG U+ MTTL-W01, runs an on-device LAN HTTP dashboard with four channel controls, metering, schedules, watchdog, protection configuration, SSE live updates, and optional MQTT. It removes the original requirement for a permanently running TCP server/bridge. Initial replacement of stock firmware requires Windows x64 or Apple silicon Mac and the original OTA tool, plus careful hardware-variant verification. DO NOT flash remotely or automatically.

## Current constraints
- The application https://smartpower1212.vercel.app is HTTPS. The firmware uses unauthenticated, unencrypted LAN HTTP and the browser may block HTTPS-to-HTTP fetch, private-network requests and cross-origin access. CORS/PNA must be checked in device source and with an actual device. Never presume Vercel can directly control the device.
- Direct local device dashboard at http://DEVICE_IP may work independently of our hosted app while on the same trusted Wi-Fi.
- Never expose HTTP or MQTT ports to the public internet or create a Vercel proxy to a private device.
- Physical safety: software protections aren't hardware safety substitutes. Firmware author verified one high-power shutdown test; temperature/current protections and measurement accuracy have not been fully validated on device variants.
- On-device relay states reflect logical state, not independently measured contact state.
- Recovery may require ST-Link and safe electrical isolation by a qualified technician. The stock firmware restoration path is documented but not guaranteed for all variants.
- Keep relay controls in MTC web app disabled until direct communication and confirmation are validated on the target hardware.

## Engineering milestones
1. Inspect upstream embedded HTTP API paths, JSON state shape, CORS and SSE endpoints and implement a typed client interface behind a feature flag (offline tests only).
2. Add device URL configuration with safe private LAN address validation; no passwords collected by hosted app until architecture reviewed.
3. Determine whether hosted HTTPS PWA can call firmware. If not, consider serving MTC UI from the firmware itself, rather than introducing a permanent server.
4. Verify firmware binary integrity from upstream and board revision on hardware; back up original firmware and confirm recoverability before any installation.
5. Test on isolated power with no external load; then use properly supervised staged tests, not unattended appliances.
6. Only after verified responses: enable individual controls, live power/energy feedback, and device-connected state.

## Upstream safety and recovery
https://github.com/af950833/mttl_w01_standalone/blob/main/recovery/README_EN.md

## Decision
Research approved; no hardware change, flashing, internet port opening, or relay actuation authorized by this document.
