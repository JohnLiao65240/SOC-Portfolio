🛡 Wazuh Log Ingestion Verification – Windows
### Objective

Verify that Windows security events are ingested and analyzed by Wazuh.

### MITRE ATT&CK Mapping

2️⃣ Test Case – Account Creation

Command Executed:

net user socuser123 P@ssw0rd! /add

Observed Alert Details: 

Rule ID: 60109

Rule Level: 8

Description: User account enable or created

MITRE Technique: T1098 - Account Manipulation, This alert is mapped to MITRE ATT&CK technique T1098 (Create Account), which falls under the Persistence tactic, indicating potential establishment of long-term access.

MITRE Tactic: Persistence

## Security Analysis

The observed event corresponds to a successful Windows logon (Rule ID 60106).

In this lab environment, the activity was generated intentionally for validation purposes. However, in a production environment, successful logon events involving privileged accounts should be monitored carefully.

Potential risks in real-world scenarios include:
- Unauthorized access using compromised credentials
- Privilege escalation attempts
- Lateral movement within a network

Although this event is benign in the current lab context, it demonstrates how Wazuh detects and classifies authentication activity.