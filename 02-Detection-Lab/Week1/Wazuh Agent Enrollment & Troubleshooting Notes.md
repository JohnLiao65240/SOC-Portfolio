## Wazuh Agent Enrollment & Troubleshooting Notes

SOC Lab Infrastructure Deployment Debug Log
1️⃣ Lab Architecture
Desktop Windows (Endpoint + Wazuh Agent)
        ↓
Ubuntu (Wazuh Server / Manager)
IP: 192.168.1.15
2️⃣ Objective

Install Wazuh Agent on Windows Endpoint

Register agent to Wazuh Manager

Ensure agent appears as Active in Dashboard

3️⃣ Initial Problem

After running:

"C:\Program Files (x86)\ossec-agent\agent-auth.exe" -m 192.168.1.12

Error received:

ERROR: (1208): Unable to connect to enrollment service at '[192.168.1.12]:1515'

Agent did not appear in:

sudo /var/ossec/bin/agent_control -l
4️⃣ Troubleshooting Process (Step-by-Step Analysis)
Step 1 – PowerShell Execution Error

Initial issue:

Unexpected token '-m'

Root cause:

PowerShell treats quoted path as string unless executed with call operator.

Correct syntax:

& "C:\Program Files (x86)\ossec-agent\agent-auth.exe" -m <ServerIP>
Step 2 – Enrollment Port Verification (Server Side)

On Ubuntu:

sudo ss -tulnp | grep 1515

Confirmed:

0.0.0.0:1515 LISTEN (wazuh-authd)

Meaning:
Enrollment service was active.

Step 3 – TCP Connectivity Test (Client Side)

On Windows:

Test-NetConnection 192.168.1.12 -Port 1515

Result:

TcpTestSucceeded : False

At this stage suspected:

Firewall

UFW

Port blocking

Step 4 – Firewall Verification

Ubuntu:

sudo ufw status

Result:

Status: inactive

Windows firewall already configured.

Conclusion:
Not a firewall issue.

Step 5 – Root Cause Identified

Critical mistake:

192.168.1.12 was the Desktop IP (Endpoint)
NOT the Ubuntu Server IP

Agent was trying to enroll to itself instead of the Wazuh Manager.

Correct architecture reminder:

Endpoint → Manager
NOT
Endpoint → Endpoint
5️⃣ Correct Enrollment Command

After identifying correct Ubuntu IP (192.168.1.15):

& "C:\Program Files (x86)\ossec-agent\agent-auth.exe" -m 192.168.1.15

Successful output:

INFO: Valid key received
6️⃣ Final Activation Step

Restart agent service:

Restart-Service Wazuh

Verify on Ubuntu:

sudo /var/ossec/bin/agent_control -l

Expected:

ID: 001, Name: DESKTOP-XXXX, IP: 192.168.1.12, Active
7️⃣ Key Lessons Learned
1️⃣ Always Confirm Server IP

Enrollment target must be the Wazuh Manager IP.

2️⃣ Understand Service Architecture
Agent → authd (1515) → Manager

Dashboard is only visualization layer.

3️⃣ Use Layered Troubleshooting

Check service running

Check listening port

Test TCP connectivity

Verify firewall

Validate architecture logic

4️⃣ Read Error Messages Carefully

The error was not:

Wazuh failure

Network failure

It was an architectural misdirection.

8️⃣ Technical Skills Strengthened

This exercise involved:

Windows PowerShell execution behavior

TCP port connectivity testing

Linux service verification

Firewall rule validation

Client-server enrollment architecture

Systematic troubleshooting methodology

9️⃣ Final Status
Agent successfully enrolled
Agent status: Active
SOC Lab infrastructure operational