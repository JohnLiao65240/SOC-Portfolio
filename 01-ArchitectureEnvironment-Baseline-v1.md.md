# SOC Lab Environment Baseline v1

## Date
2026-02-21

## Objective
To validate Wazuh infrastructure stability and confirm log ingestion and alert generation.

---

## Infrastructure Components

### SIEM Core
- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

### Active Agents
1. Windows 11
2. Ubuntu Server

Both agents are successfully registered and online.

---

## Network Communication

Agent to Manager communication:
- Protocol: TCP
- Port: 1514
- Function: Log forwarding

---

## Validation Steps

### 1. Service Verification

systemctl status wazuh-manager
systemctl status wazuh-indexer
systemctl status wazuh-dashboard
systemctl status filebeat


All services reported as active (running).

---

### 2. Agent Status Check

Dashboard confirms:
- 2 active agents
- 100% coverage
- No disconnected agents

---

### 3. Alert Validation

Observed alert:

- Rule ID: 60106
- Description: Windows logon success
- Level: 3
- MITRE Technique: T1078

This confirms:
- Log parsing successful
- Rule matching functional
- Detection engine operational

---

## Current Scope Limitations

- No attack simulation performed
- No Kali deployment
- No Metasploitable deployment

Environment currently focused on host-based event monitoring.

---

## Status

Baseline validation completed successfully.
Environment stable for next phase analysis.