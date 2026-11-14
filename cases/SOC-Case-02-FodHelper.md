# SOC Case 02 — FodHelper UAC Bypass Detection

## 1. Incident Overview

**Incident Type:** Potential UAC bypass / privilege escalation  
**Endpoint:** WS01 — Windows 10 SOC Workstation  
**Detection Platform:** Wazuh SIEM  
**Detection Rule:** `92055`  
**Severity:** Level 12  
**MITRE ATT&CK:** T1548.002 — Bypass User Account Control

## 2. Objective

Investigate a Wazuh alert involving the Windows `fodhelper.exe` binary and determine whether the activity represented a successful privilege escalation attempt or a benign system event.

## 3. Detection

Wazuh detected the execution of:

```text
fodhelper.exe
```

The process was associated with the Windows `svchost.exe` process running the `DcomLaunch` service under the SYSTEM account.

The detection triggered Wazuh Rule `92055` with Level 12 severity.

## 4. Investigation

The alert was investigated using Wazuh Threat Hunting and Windows Sysmon telemetry.

The investigation focused on:

- Process execution
- Parent-child process relationships
- User context
- Privilege level
- Registry activity
- Possible follow-on processes
- Indicators associated with the FodHelper UAC bypass technique

### Observed Activity

```text
svchost.exe
    |
    └── fodhelper.exe
            |
            └── No suspicious follow-on process observed
```

The `fodhelper.exe` process was Microsoft-signed and was launched by the Windows `DcomLaunch` service.

## 5. Investigation Findings

The following observations were made:

- `fodhelper.exe` execution was detected.
- The executable was Microsoft-signed.
- The parent process was `svchost.exe`.
- The associated service was `DcomLaunch`.
- The process executed with SYSTEM-level context.
- No confirmed `ms-settings` registry modification was identified.
- No suspicious child process or confirmed malicious follow-on activity was observed.

## 6. MITRE ATT&CK Mapping

**Technique:** T1548.002 — Bypass User Account Control

FodHelper is a legitimate Windows component that can be abused to bypass User Account Control when combined with specific registry modifications.

Therefore, detection of `fodhelper.exe` alone is not sufficient to confirm malicious activity.

## 7. Analyst Assessment

**Verdict:** Likely Benign / False Positive

The alert was treated as a potential UAC bypass because of the behavior associated with `fodhelper.exe`.

However, the available telemetry did not provide sufficient evidence to confirm exploitation.

No confirmed malicious registry modification, suspicious child process, or additional indicators of compromise were identified during the investigation.

## 8. Limitations

The investigation was limited by the telemetry available in the lab environment.

Additional evidence such as:

- Complete registry telemetry
- Additional endpoint activity
- Correlated authentication events
- Network telemetry
- Process command-line context

could provide greater confidence in the final determination.

## 9. SOC Analyst Workflow

```text
Wazuh Alert
     |
     v
Identify Process
     |
     v
Analyze Parent/Child Relationship
     |
     v
Check User & Privilege Context
     |
     v
Check Registry Activity
     |
     v
Map to MITRE ATT&CK
     |
     v
Look for Additional Indicators
     |
     v
Determine Verdict
```

## 10. Skills Demonstrated

- Wazuh SIEM investigation
- Windows endpoint monitoring
- Sysmon telemetry analysis
- Process tree analysis
- MITRE ATT&CK mapping
- UAC bypass detection
- False-positive analysis
- SOC alert triage
- Incident investigation
- Security event correlation
