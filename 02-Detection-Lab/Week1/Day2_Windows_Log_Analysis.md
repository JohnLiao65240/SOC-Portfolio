🛡 Wazuh Log Ingestion Verification – Windows
1️⃣ Objective

Verify that Windows security events are ingested and analyzed by Wazuh.

2️⃣ Test Case 1 – Account Creation

Command Executed:

net user socuser123 P@ssw0rd! /add

Observed Alert Details:

Rule ID:

Rule Level:

Description:

MITRE Technique:

MITRE Tactic:

Security Analysis:
Explain why this could be malicious.

3️⃣ Test Case 2 – Failed Login Attempt

Method Used:
Manual incorrect password attempts

Observed Alert Details:

Rule ID:

Rule Level:

Description:

MITRE Technique:

MITRE Tactic:

Security Analysis:
Explain brute-force risk.

4️⃣ Key Learning

SIEM uses rule-based detection

Alerts have severity levels

MITRE mapping improves incident context

Not all alerts are incidents