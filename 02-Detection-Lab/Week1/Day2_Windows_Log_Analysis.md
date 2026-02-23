🛡 Wazuh Log Ingestion Verification – Windows
1️⃣ Objective

Verify that Windows security events are ingested and analyzed by Wazuh.

2️⃣ Test Case 1 – Account Creation

Command Executed:

net user socuser123 P@ssw0rd! /add

Observed Alert Details: 

Rule ID: 60109

Rule Level: 8

Description: User account enable or created

MITRE Technique: T1098 - Account Manipulation

MITRE Tactic: Persistence

Security Analysis:
Explain why this could be malicious.

3️⃣ Test Case 2 – Failed Login Attempt

Method Used:
Manual incorrect password/account attempts

Observed Alert Details:

Rule ID: 60122

Rule Level: 5

Description: Logon failure - Unknown user or bad password

MITRE Technique: T1078, T1531 - Valid Accounts, Account Access Removal

MITRE Tactic: 
                "Defense Evasion", 
                "Persistence", 
                "Privilege Escalation", 
                "Initial Access",
                "Impact"

Security Analysis:
Explain brute-force risk.

4️⃣ Key Learning

SIEM uses rule-based detection

Alerts have severity levels

MITRE mapping improves incident context

Not all alerts are incidents