# MTC Smart Power

Arabic-first experimental PWA for LG U+ / Jinheung MTTL-W01 smart power strip.

## Version 1.0.2
- Browser diagnostic action now confirms every click with an incrementing count and visible timestamp.
- Results explicitly distinguish browser connectivity from actual hardware connectivity.

## Version 1.0.1
- Added a safe, read-only browser connectivity diagnostics panel.
- Added guided SoftAP setup steps and explicit detection limitations.
- No direct hardware connection is claimed or attempted.

## Previous prototype 0.1.0
- Responsive dashboard, four outlets, customizable local names.
- Installable web app and offline shell cache.
- Energy telemetry placeholders; no simulated metrics.
- Controls are intentionally disabled until **direct browser-to-device control without an always-on bridge** is verified.

## Important protocol finding
The factory device initiates a TCP connection to a listening server on port 10086. Ordinary Safari/Chrome pages cannot listen for arbitrary incoming TCP connections. A PWA alone cannot be represented as functioning hardware control using this protocol. Firmware or a new verified device endpoint is required to meet the no-bridge requirement.

References:
- https://github.com/ardabil/ha-mttl-w01
- https://github.com/ttaengz/mttl-w01-matterbridge

## Deploy
Static project: deploy repository root on Vercel with Framework Preset 'Other', no build command, and output directory `.` (project root).

## Safety
Do not claim relay state or issue commands unless a real verified connection exists. No firmware modification is performed by this project.
