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

Security Analysis:
Explain why this could be malicious.


Not all alerts are incidents