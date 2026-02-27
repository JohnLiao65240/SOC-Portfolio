# Week 1 – Day 4
## Windows Privilege Escalation Detection

### Objective
Detect suspicious account creation and privilege escalation.

---

## Observed Event

Event ID: 4720  
Event ID: 4732  

TargetUserName: attacker (Administrators)  
SubjectUserName: Administrator (John) 

---

## MITRE ATT&CK Mapping

Tactic: Persistence  
Technique: T1098 – Account Manipulation
Rule level : 5

Tactic: Defense Evasion, Privilege Escalation  
Technique: T1484 – Domain Policy Modification
Rule level : 12

---

## Security Analysis

The creation of a new account followed by adding it to the Administrators group is a common attacker technique to maintain persistence and escalate privileges.

This behavior should be validated with IT change management records.

---

## Conclusion

Wazuh successfully detected the privilege escalation activity.