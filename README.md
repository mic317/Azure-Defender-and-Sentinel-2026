# Azure-Defender-and-Sentinel-2026
SC-200 Home Lab
What I Did (Realistic Summary of the Lab)
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


