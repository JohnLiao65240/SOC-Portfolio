# SOC Home Lab – Environment Baseline (Week 1 Day 1)

## Overview
This project documents the initial deployment and validation of a Wazuh SIEM home lab.

Current active environment includes:
- Windows 11 (Wazuh Agent installed)
- Ubuntu Server (Wazuh Agent installed)
- Wazuh Server (Manager, Indexer, Dashboard)

No attack simulation has been conducted at this stage.

---

## Architecture Summary

Log Flow:
Wazuh Agent → Wazuh Manager (TCP 1514)

Active agents:
- Windows 11
- Ubuntu Server

---

## Validation Results

### Service Status
All core services are running:
- wazuh-manager
- wazuh-indexer
- wazuh-dashboard
- filebeat

### Log Ingestion
Logs from Windows and Ubuntu are successfully forwarded to Wazuh.

### Alert Verification
Example alert observed:

- Rule ID: 60106
- Description: Windows logon success
- Level: 3
- MITRE Technique: T1078

This confirms that:
- Log ingestion is functioning
- Rule engine is active
- MITRE mapping is operational

---

## Conclusion

The SIEM pipeline is fully operational.
The environment is ready for further detection engineering exercises.