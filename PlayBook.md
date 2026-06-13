
---

### 3️⃣ playbook.md — automated response playbook

Create `playbook.md` and paste:

```markdown
# Automated Response Playbook – EICAR Malware Alert

This document describes an automated response playbook for handling a malware alert (EICAR) using Microsoft Sentinel and Defender. Even though one VM was partially onboarded, the EICAR alert still generated, making it a good candidate for automation.

---

## 1. Playbook Goal

The playbook is designed to:

- Collect alert and incident details.
- Notify the SOC team.
- Attempt device isolation (if supported).
- Create a ticket or case.
- Log actions for audit and review.

---

## 2. Trigger

- Trigger source: **Microsoft Sentinel incident**.
- Incident type: **Malware detected (EICAR)**.
- Data source: **Microsoft Defender for Cloud / Defender AV**.

---

## 3. Playbook Steps

### 3.1 Extract Incident Information

The playbook pulls:

- Alert name.
- Alert severity.
- Impacted resource (VM).
- Timestamp.
- Incident ID.

This information is used in notifications and ticketing.

---

### 3.2 Notify the SOC Team

Send an automated notification (email, Teams, Slack) to the SOC channel including:

- Summary of the alert.
- Impacted VM.
- Severity.
- Recommended next steps (review alert, confirm scope, check related activity).

---

### 3.3 Attempt VM Isolation (If Supported)

If the VM is fully onboarded into MDE:

- Call the Defender API to isolate the device.
- Log whether isolation succeeded or failed.
- Include isolation status in the incident notes.

> In this lab, the second Windows VM could not be isolated due to partial onboarding. This limitation is documented as part of the learning experience.

---

### 3.4 Create a Ticket or Case

Automatically create a ticket in a ticketing system (e.g., ServiceNow, Jira):

- Include alert details and incident ID.
- Assign to the SOC queue.
- Store the ticket number in the incident for tracking.

---

### 3.5 Document the Response

Log:

- Actions taken by the playbook.
- Isolation attempts and results.
- Notifications sent.
- Ticket information.

This creates an audit trail for compliance and future review.

---

## 4. Why This Playbook Matters

This playbook demonstrates:

- How Sentinel and Defender can work together.
- How automation can reduce response time.
- How SOC workflows can be standardized.
- How limitations (like partial onboarding) are handled and documented.

Even in an imperfect lab, the logic of the playbook reflects real SOC practices.

---

## 5. Future Enhancements

Potential improvements:

- Automatic user lookup for the affected device.
- Quarantine of suspicious files.
- Collection of forensic artifacts (logs, processes).
- Triggering hunting queries for related activity.
- Auto-closing known false positives with documented criteria.
