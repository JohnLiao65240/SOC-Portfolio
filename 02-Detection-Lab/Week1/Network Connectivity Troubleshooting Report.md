## SOC Lab Network Debugging & Virtualization Analysis

1. Objective

To diagnose and resolve network connectivity issues between:

Desktop (Windows – Wired)

Laptop (Windows – Wired)

Ubuntu VM (Hosted on Laptop)

The goal was to ensure full Layer 3 connectivity within the SOC lab environment to support Wazuh agent communication and future attack simulations.

2. Initial Network Architecture
Device	IP Address	Connection Type
Desktop (Windows)	192.168.1.10	Wired
Laptop (Windows)	192.168.1.13	Wired
Ubuntu VM	(Initial: Non-192.168.1.x)	Virtual Adapter

All devices were connected to the same router:

Gateway: 192.168.1.1
Subnet: 192.168.1.0/24
3. Observed Issue
Phase 1

Desktop ↔ Laptop could not ping each other.

Both could ping the router (192.168.1.1).

Phase 2

Windows ↔ Windows connectivity restored.

Desktop Windows ↔ Ubuntu VM still unreachable.

Error observed:

Destination host unreachable
4. Troubleshooting Methodology

A structured Layer 2 / Layer 3 diagnostic approach was used.

Step 1 – Subnet Verification

Commands used:

ipconfig
ip a

Confirmed both physical machines were in:

192.168.1.0/24

Conclusion:
✔ Not a subnet mismatch issue.

Step 2 – Gateway Reachability Test

Both systems successfully executed:

ping 192.168.1.1

Conclusion:
✔ Router functioning properly
✔ No upstream network issue

Step 3 – Directional Connectivity Testing

Tested:

Desktop → Laptop

Laptop → Desktop

Observed asymmetric connectivity initially.

Conclusion:
Likely host-based firewall filtering inbound ICMP traffic.

Step 4 – Windows Firewall Analysis

Key discovery:

Windows Defender Firewall default behavior:

Allows outbound traffic

Blocks unsolicited inbound ICMP

Resolution steps:

Open firewall management:

wf.msc

Enable rule:

File and Printer Sharing (Echo Request - ICMPv4-In)

Verify active network profile:

Get-NetConnectionProfile

Set to Private if required:

Set-NetConnectionProfile -NetworkCategory Private

Result:
✔ Windows ↔ Windows connectivity restored.

Step 5 – Virtual Machine Network Mode Analysis

Ubuntu VM remained unreachable.

Investigation revealed VM was using non-bridged networking.

Virtualization network modes comparison:

Mode	External Access	Use Case
NAT	No	Internet access only
Host-Only	No	Host-local lab
Bridged	Yes	Full LAN visibility

Resolution:

VM network adapter changed to:

Bridged Adapter
→ Bound to physical wired NIC

After reboot:

ip a

VM obtained:

192.168.1.x

Result:
✔ Full bidirectional connectivity achieved.

5. Root Cause Analysis

The issue consisted of two independent root causes:

Windows Firewall blocking inbound ICMP under active network profile.

Ubuntu VM configured in non-bridged network mode, preventing LAN visibility.

6. Security & SOC Perspective

This troubleshooting exercise demonstrates key SOC-relevant competencies:

Network Segmentation Awareness

Being in the same subnet does not guarantee connectivity.

Stateful Firewall Behavior Understanding

Windows allows outbound traffic but blocks unsolicited inbound traffic.

Virtualization Network Architecture

Incorrect VM network mode can simulate segmentation or isolation.

Layered Debugging Approach

Systematic elimination of:

Subnet issues

Gateway issues

Host firewall filtering

Virtual network misconfiguration

7. Final Validated Architecture
Desktop Windows (192.168.1.10)
        ↕
Laptop Windows (192.168.1.13)
        ↕
Ubuntu VM (192.168.1.x - Bridged)

All devices reachable within:

192.168.1.0/24

Environment now ready for:

Wazuh Agent enrollment

Lateral movement simulation

Privilege escalation testing

Attack traffic analysis

8. Conclusion

The network issue was resolved through structured troubleshooting involving:

Layer 3 reachability validation

Host-based firewall configuration

Virtualization network mode correction

This process reflects real-world enterprise troubleshooting methodology and strengthens foundational SOC engineering skills.