
# Home SOC Lab | Wazuh SIEM & Threat Detection

## Overview
A hands-on Security Operations Center (SOC) lab designed to simulate enterprise security monitoring, network defense, endpoint visibility, and incident investigation.

Built using Oracle VirtualBox, Wazuh SIEM, pfSense, Windows Active Directory, Sysmon, Kali Linux, and CrowdSec.

## Technologies Used
- Wazuh SIEM — Security monitoring and alert investigation
- pfSense — Firewall and network segmentation
- Windows Server 2022 — Active Directory and DNS
- Windows 10 — Domain-joined SOC workstation
- Sysmon — Endpoint process and activity monitoring
- Kali Linux — Controlled security testing
- CrowdSec — SSH security monitoring
- VirtualBox — Virtualized lab infrastructure

## Key Achievements
- Deployed Wazuh Manager, Indexer, Dashboard, and Windows Agent.
- Configured Windows Security and Sysmon log collection.
- Integrated pfSense firewall logs with Wazuh over UDP 514.
- Created a custom pfSense decoder and detection rule (ID 100100).
- Successfully generated 4 real Level 5 firewall-block alerts.
- Investigated suspicious FodHelper activity using Wazuh telemetry.
- Deployed and tested CrowdSec SSH monitoring.

## SOC Investigation Cases

### Case 01 — pfSense Firewall Block Detection
- Source: 10.10.10.100 (Kali Linux)
- Destination: 10.10.20.1 (pfSense DMZ)
- Protocol: ICMP
- Result: 4 blocked packets and 4 Wazuh Level 5 alerts
- Rule ID: 100100
- Verdict: Expected firewall control validation

### Case 02 — Windows FodHelper Investigation
- Detection: FodHelper-related process activity
- Wazuh Rule: 92055
- Severity: Level 12
- MITRE ATT&CK: T1548.002
- Verdict: Likely benign based on available evidence

## Project Evidence
Architecture diagrams, screenshots, detection rules, and detailed investigation reports will be added to this repository.

## Future Enhancements
- CrowdSec-to-Wazuh integration
- Additional SOC detection scenarios
- Expanded incident investigation reports

## Disclaimer
All security testing was conducted in an isolated, authorized virtual lab for educational purposes.
