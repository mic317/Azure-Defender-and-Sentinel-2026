# Azure-Defender-and-Sentinel-2026
SC-200 Home Lab
What I Did 
This lab was built to simulate a real SOC analyst workflow using Microsoft Defender for Cloud, Microsoft Sentinel, and multiple Azure virtual machines. The goal was to onboard machines, generate alerts, and understand how Defender XDR processes telemetry. The process was not perfect — and that’s exactly what made it realistic.

What I Successfully Completed
Created three Azure VMs (Ubuntu + two Windows).
Enabled Defender for Servers Plan 2 in Defender for Cloud.
Connected a Log Analytics workspace and enabled Microsoft Sentinel.
Installed the Azure Monitor Agent (AMA) using a Data Collection Rule.
Verified Heartbeat logs flowing into Sentinel.
Successfully generated and investigated an EICAR malware alert.
Performed deep troubleshooting on Windows onboarding issues.
Learned the difference between:
Defender Antivirus
Defender for Endpoint
Full XDR onboarding
AV‑only mode
Captured screenshots of every step, including failures.
What Worked Exactly as Expected
Defender for Cloud onboarding
AMA installation
Heartbeat logs
EICAR malware detection
Ubuntu VM onboarding
First Windows VM onboarding
Sentinel workspace integration
These components behaved normally and provided the expected telemetry.
 What Did NOT Work (And Why It Matters)
The second Windows VM never fully onboarded into Defender for Endpoint (MDE).
Symptoms included:
VM never appeared in Defender XDR → Devices
No alerts for:
Failed logins
Firewall disable
Reconnaissance
PowerShell activity
Only EICAR alerts worked (AV telemetry only)
SenseCncProxy.exe was missing from the system
Onboarding package downloaded as GatewayWindowsDefenderATPOnboardingPackage
Multiple MSI installs did not create the cloud connector
What I Learned From the Failure
This was the most valuable part of the lab.
I learned that:
A VM can have the Sense service running but still be in AV‑only mode.
Defender AV ≠ Defender for Endpoint (full XDR).
If the cloud connector is missing, the device will:
Never register in Defender XDR
Never send advanced telemetry
Never generate behavioral alerts
Some Azure VM images do not support full MDE onboarding.
Troubleshooting onboarding is a real SOC skill:
Checking services
Checking registry keys
Checking onboarding state
Checking cloud connectivity
Understanding why telemetry fails

TroubleShooting 
Troubleshooting the Windows VM Onboarding Failure
This section documents the real‑world troubleshooting I performed when my second Windows VM failed to fully onboard into Microsoft Defender for Endpoint (MDE). This was the most valuable part of the lab because it required actual investigation, not just following a tutorial.
5.1 Symptoms Observed
The second Windows VM showed several clear signs of partial onboarding / AV‑only mode:
VM did not appear under Defender XDR → Assets → Devices
Only EICAR malware alerts worked
No alerts for:
Failed logins
Firewall disable
Reconnaissance
PowerShell activity
SenseCncProxy.exe was missing
Onboarding package downloaded as GatewayWindowsDefenderATPOnboardingPackage
Multiple MSI installs did not create the cloud connector
These symptoms pointed to a deeper issue than a simple onboarding script failure.
5.2 Verification Steps Performed
A. Checked the Sense service
powershell
sc.exe query sense
Result: RUNNING  
This confirmed the basic Defender service was installed.
B. Checked passive mode
powershell
Get-MpPreference | Select ForceDefenderPassiveMode
Result: False  
This confirmed Defender AV was active and not overridden by another AV.
C. Attempted to register the device
powershell
& "$env:ProgramFiles\Windows Defender\SenseCncProxy.exe" -register
Result: CommandNotFoundException  
This proved the cloud connector component was missing.
D. Confirmed the VM never appeared in Devices
The VM never registered in Defender XDR, even after multiple onboarding attempts.
5.3 Root Cause Analysis
Based on all evidence, the VM was stuck in AV‑only mode, meaning:
Defender Antivirus was working
But the full MDE platform (cloud connector + telemetry pipeline) was not installed
Therefore, the VM could not:
Register with Defender XDR
Send advanced telemetry
Generate behavioral alerts
This is a known issue with certain Azure VM images that do not support full MDE onboarding, even when the Sense service is running.
5.4 Why This Matters
This troubleshooting experience taught me:
Defender AV and Defender for Endpoint are not the same
A device can look “healthy” but still be missing critical XDR components
The onboarding package type matters
VM image selection affects Defender onboarding
Real SOC work involves diagnosing why telemetry is missing, not just generating alerts
This failure became one of the most valuable parts of the lab because it reflects real‑world SOC engineering challenges.
5.5 Final Outcome
Even though the VM never fully onboarded, the troubleshooting process provided:
A realistic investigation scenario
Clear evidence of partial onboarding
A documented root cause
Screenshots of errors and diagnostic commands
A strong learning experience for my SOC portfolio
This section demonstrates my ability to troubleshoot complex Defender onboarding issues — a skill that SOC analysts use every day.


