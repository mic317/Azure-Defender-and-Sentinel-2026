# Lab Architecture & Data Flow

This document describes the architecture of the SC-200 home lab, including virtual machines, security components, and data flow between Defender for Cloud and Microsoft Sentinel.

---

## 1. Components

### 1.1 Azure Resources

- Resource group containing:
  - 1× Ubuntu VM
  - 2× Windows VMs
  - 1× Log Analytics workspace
  - Networking resources (VNet, NSG, etc.)

### 1.2 Security Services

- Microsoft Defender for Cloud
  - Defender for Servers Plan 2 enabled.
- Microsoft Sentinel
  - Enabled on the Log Analytics workspace.
- Azure Monitor Agent (AMA)
  - Installed on at least one Windows VM via Data Collection Rule.

---

## 2. Data Flow Overview

1. **VM Activity → AMA**  
   - The Azure Monitor Agent collects telemetry (Heartbeat, performance, logs) from the VM.

2. **AMA → Log Analytics Workspace**  
   - Telemetry is sent to the connected workspace.

3. **Workspace → Microsoft Sentinel**  
   - Sentinel uses the workspace as its data source for analytics, incidents, and hunting.

4. **Defender for Cloud → Defender XDR**  
   - Defender for Cloud and Defender AV generate security alerts (e.g., EICAR).
   - These alerts appear in Defender XDR and can also surface in Sentinel.

---

## 3. VM Roles

### 3.1 Ubuntu VM

- Used to demonstrate Linux onboarding and telemetry.
- Appears in Defender XDR Devices.
- Contributes Heartbeat and other logs to Sentinel.

### 3.2 First Windows VM (Successful Onboarding)

- Successfully onboarded into Defender for Endpoint.
- Appears in Defender XDR Devices.
- Sends telemetry for malware and other activity.
- Used to generate the EICAR alert.

### 3.3 Second Windows VM (Partial Onboarding)

- Sense service running, Defender AV active.
- Did not fully onboard into MDE.
- Did not appear in Defender XDR Devices.
- Only EICAR alerts worked (AV-only telemetry).
- Used as the focus of the troubleshooting guide.

---

## 4. AMA and Data Collection Rule (DCR)

- AMA installed via a Data Collection Rule targeting the Windows VM.
- Heartbeat logs verified in Sentinel using KQL:

```kql
Heartbeat
| project TimeGenerated, ResourceGroup, ComputerEnvironment
| take 10
