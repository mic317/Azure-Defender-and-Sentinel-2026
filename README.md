# Azure-Defender-and-Sentinel-2026
# SC-200 Home Lab – Defender & Sentinel

## 1. Lab Overview

This lab simulates a realistic SOC analyst workflow using:
- Microsoft Defender for Cloud
- Microsoft Sentinel
- Multiple Azure virtual machines (Ubuntu + Windows)

The goal was to onboard machines, generate alerts, and understand how Defender XDR processes telemetry. The lab is intentionally imperfect and includes a real onboarding failure that required troubleshooting.

## 2. What I Did

- Created three Azure VMs (Ubuntu + two Windows).
- Enabled Defender for Servers Plan 2 in Defender for Cloud.
- Connected a Log Analytics workspace and enabled Microsoft Sentinel.
- Installed the Azure Monitor Agent (AMA) using a Data Collection Rule.
- Verified Heartbeat logs flowing into Sentinel.
- Generated and investigated an EICAR malware alert.
- Troubleshot a Windows VM that failed to fully onboard into Defender for Endpoint.
- Captured screenshots of both successful and failed states.

## 3. What Worked

- Defender for Cloud onboarding
- AMA installation and Heartbeat logs
- EICAR malware detection
- Ubuntu VM onboarding
- First Windows VM onboarding
- Sentinel workspace integration

## 4. What Didn’t Work (On Purpose)

- Second Windows VM never fully onboarded into Defender for Endpoint (MDE).
- VM did not appear in Defender XDR → Devices.
- No alerts for failed logins, firewall disable, recon, or PowerShell activity.
- `SenseCncProxy.exe` was missing.
- Onboarding package was `GatewayWindowsDefenderATPOnboardingPackage`.
- Multiple MSI installs did not create the cloud connector.

## 5. What I Learned

- A VM can have the `sense` service running but still be in AV-only mode.
- Defender AV ≠ Defender for Endpoint (full XDR).
- Missing cloud connector means no XDR device registration or advanced telemetry.
- VM image choice affects Defender onboarding behavior.
- Real SOC work includes diagnosing missing telemetry, not just generating alerts.

## 6. Detailed Documentation

- [Troubleshooting Guide](troubleshooting.md)
- [Automated Response Playbook](playbook.md)
- [Lab Architecture & Data Flow](architecture.md)

## 7. Screenshots

Screenshots are organized under the `screenshots/` folder:
- Resource group and VMs
- Defender for Cloud settings
- Sentinel workspace and Heartbeat
- EICAR alert
- Broken Windows VM (onboarding failure)
- AMA / DCR configuration


