## Local Authentication Failure Analysis

### Objective
Investigation of Suspected Brute Force Activity.

---

### Observed Event

- Event ID: 4625
- Target User: level8
- Source IP: 127.0.0.1
- Logon Type: 7

---

### Analysis

Five failed unlock attempts were detected (Event ID 4625).

The logon type was 7 (Unlock), and the logon process was User32.

The source IP was 127.0.0.1, indicating a local authentication attempt.

This activity represents user password mistyping during workstation unlock,
not a remote brute force attack.

A successful unlock event (4624, Type 7) followed shortly after.

---

### MITRE ATT&CK Mapping

Test Case – Failed Login Attempt

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


### Conclusion

Wazuh successfully detected multiple failed login attempts.
This scenario demonstrates credential attack detection capability.