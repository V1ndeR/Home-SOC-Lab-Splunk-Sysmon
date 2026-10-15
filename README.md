# Home SOC Lab — Splunk SIEM & Sysmon

## Overview

This repository documents my personal Security Operations Center (SOC) laboratory, created to develop hands-on skills in security monitoring, log analysis, and incident investigation.

The lab is designed to simulate basic SOC Tier 1 investigation workflows using Windows security telemetry and Splunk SIEM.

## Lab Environment

| Component | Technology | Purpose |
|-----------|------------|---------|
| SIEM Server | Splunk Enterprise on Ubuntu Linux | Centralized log collection and analysis |
| Windows Endpoint | Windows with Sysmon | Security event generation |
| Log Forwarding | Splunk Universal Forwarder | Forward Windows security logs to Splunk |
| Security Logs | Windows Event Logs | Authentication and system event analysis |
| Endpoint Telemetry | Sysmon | Process and system activity monitoring |
| Network Analysis | Wireshark | Packet and network traffic investigation |

## Project Architecture

Windows Endpoint
    |
    | Windows Event Logs / Sysmon
    |
Splunk Universal Forwarder
    |
    | Forwarded Security Events
    |
Ubuntu Linux — Splunk Enterprise
    |
    | SPL Searches
    |
SOC Analyst Investigation

## Investigation Practice

The laboratory supports practical exercises involving:

- Windows authentication event analysis
- Suspicious process execution
- Parent-child process relationships
- Security event filtering using SPL
- Initial investigation of suspicious activity
- Evidence collection and documentation
- SOC Tier 1 alert triage workflows

## Splunk SPL Practice

Examples of searches developed during training:

### Failed Authentication Events

```spl
index=* EventCode=4625
| stats count by Account_Name
| sort - count
```

### Successful Authentication Events

```spl
index=* EventCode=4624
| table _time host Account_Name Source_Network_Address
| sort - _time
```

### Authentication Activity by User

```spl
index=* (EventCode=4624 OR EventCode=4625)
| stats count by Account_Name EventCode
```

Note: SPL field names and index names depend on the event source and parsing configuration. Queries should be validated against the actual lab data.

## Current Focus

- Improving Splunk SPL investigation skills
- Practicing Windows Event Log analysis
- Investigating suspicious endpoint processes
- Developing SOC incident reporting skills
- Preparing for a Junior SOC Analyst (Tier 1) role

## Disclaimer

This repository documents personal cybersecurity training conducted in an isolated lab environment. It does not represent professional SOC employment or production security operations.

## Documented Investigations

### Investigation #001 — Windows Authentication Analysis

Analyzed Windows Security Event Logs using Splunk Enterprise.

The investigation covered four failed authentication attempts
followed by two related successful logon events.

The activity was confirmed as authorized testing in a personal lab.

**Investigation Report:**  
[View Investigation #001](investigations/001-windows-authentication-analysis.md)

**SPL Queries:**  
[View Authentication Queries](spl-queries/windows-authentication.spl)

**Evidence:**  
[View Splunk Screenshots](screenshots/)
