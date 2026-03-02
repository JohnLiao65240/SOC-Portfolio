📄 Week 1 – Day 5
Custom Brute Force Detection & Authentication Analysis

1. Executive Summary

This lab focused on analyzing Windows authentication failures and implementing a custom threshold-based detection rule in Wazuh.

Repeated failed login attempts within a defined timeframe successfully triggered a high-severity alert, demonstrating practical brute-force detection capability.

The detection logic was validated through controlled testing scenarios.

2. Lab Objective

Analyze Windows Event ID 4625 (Failed Logon)

Understand authentication-related log fields

Create a custom detection rule

Validate threshold-based alert triggering

Map detection behavior to MITRE ATT&CK

3. Environment
Component	        Configuration
SIEM	            Wazuh
Manager OS	        Ubuntu Server
Endpoint	        Windows 10
Agent Name	        DESKTOP-3C3INCJ
Test Account	    John
Base Event	        Windows Event ID 4625
Custom Rule ID	    100100

4. Detection / Event Overview

When an incorrect password is entered, Windows generates:

Event ID: 4625
Description: Logon failure – Unknown user or bad password

Wazuh parses this into:

Rule ID: 60122
Level: 5

This represents a single failed authentication attempt.

5. Technical Analysis
Key Event Fields

Target User

targetUserName: John

Logon Type

logonType: 2

Logon Type 2 = Interactive (local login)

Failure Status Codes

status: 0xC000006D
subStatus: 0xC000006A

0xC000006D → Logon failure

0xC000006A → Incorrect password

This confirms password-based authentication failure.

6. Detection Logic

A custom rule was created to detect repeated failed login attempts.

Detection behavior:

Match base rule 60122

Same user

Trigger when frequency threshold is met within timeframe

Example configuration:

## (Ubuntu wazuh server path : /var/ossec/etc/rules/local_rules.xml)

<rule id="100100" level="10" frequency="2" timeframe="60">
  <if_matched_sid>60122</if_matched_sid>
  <same_user />
  <description>Multiple failed login attempts detected (Possible Brute Force)</description>
  <mitre>
    <id>T1110</id>
  </mitre>
</rule>

This enables differentiation between normal user mistakes and potential brute-force activity.

7. Validation Testing

Controlled testing was performed to verify detection behavior.

Scenario	                            Result
1 failed attempt within 60 seconds	    No 100100 alert triggered
2 failed attempts within 60 seconds	    100100 alert triggered
Attempts spaced beyond 60 seconds	    No 100100 alert triggered

This confirms correct threshold-based correlation behavior.

The system accurately distinguishes between isolated failures and repeated authentication attempts.

8. MITRE ATT&CK Mapping
Tactic	Technique
Credential Access	T1110 – Brute Force

Repeated authentication failures are commonly associated with password guessing or automated brute-force attacks.

9. Security Impact Assessment

Single failed logins may indicate:

User error

Forgotten password

Normal operational activity

However, repeated failures within a short timeframe may indicate:

Password guessing

Automated brute-force attempts

Credential harvesting behavior

In production environments, recommended mitigations include:

Account lockout policy

Multi-factor authentication (MFA)

Login monitoring and alerting

Restricting external authentication exposure

10. Key Takeaways

Successfully analyzed Windows authentication logs

Implemented custom threshold-based detection logic

Validated correlation behavior through controlled testing

Mapped detection to MITRE ATT&CK framework

Demonstrated practical SOC detection engineering capability