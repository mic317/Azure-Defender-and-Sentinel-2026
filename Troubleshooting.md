# Troubleshooting the Windows VM Onboarding Failure

This document describes the real-world troubleshooting I performed when my second Windows VM failed to fully onboard into Microsoft Defender for Endpoint (MDE). This was the most valuable part of the lab because it required investigation, not just following a tutorial.

---

## 1. Symptoms Observed

The second Windows VM showed clear signs of partial onboarding / AV-only mode:

- VM did not appear under **Defender XDR → Assets → Devices**.
- Only **EICAR malware** alerts worked.
- No alerts for:
  - Failed logins
  - Firewall disable
  - Reconnaissance
  - PowerShell activity
- `SenseCncProxy.exe` was missing.
- Onboarding package downloaded as `GatewayWindowsDefenderATPOnboardingPackage`.
- Multiple MSI installs did not create the cloud connector.

These symptoms indicated a deeper issue than a simple onboarding script failure.

---

## 2. Verification Steps Performed

### 2.1 Checked the Sense service

```powershell
sc.exe query sense
