
# Home SOC Lab — Network Architecture

## Overview

This virtualized SOC environment uses pfSense for network segmentation, Windows Active Directory for identity management, and Wazuh SIEM for centralized security monitoring.

## Network Configuration

| Component | IP Address | Purpose |
|---|---|---|
| pfSense LAN | 10.10.10.1 | Firewall and LAN gateway |
| pfSense DMZ | 10.10.20.1 | DMZ gateway |
| Windows Server DC01 | 10.10.10.10 | Active Directory and DNS |
| Windows Workstation WS01 | 10.10.10.102 | Endpoint monitoring |
| Wazuh Server | 10.10.10.103 | Centralized SIEM |
| Kali Linux | 10.10.10.100 | Controlled security testing |

## Security Monitoring Architecture

- Windows Security and Sysmon logs are collected by the Wazuh agent on WS01.
- pfSense forwards firewall events to Wazuh over UDP port 514.
- Wazuh processes pfSense logs using a custom decoder and detection rule.
- CrowdSec is deployed on Kali Linux for SSH security monitoring.

## Verified Detection

A controlled ICMP test from Kali Linux to the pfSense DMZ interface generated four blocked firewall events.

Wazuh successfully detected all four events using custom rule 100100 at severity Level 5.

## Future Enhancements

- CrowdSec-to-Wazuh integration
- Additional detection scenarios
- Expanded SOC investigations
