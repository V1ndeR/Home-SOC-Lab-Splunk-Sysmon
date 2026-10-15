# Investigation #001 — Windows Authentication Analysis

## Investigation Overview

**Environment:** Personal SOC Lab  
**SIEM:** Splunk Enterprise  
**Endpoint:** Windows 11  
**Host:** DESKTOP-F2EIULL  
**Date:** October 15, 2026  
**Classification:** Benign Activity — Authorized User Testing

## Objective

Investigate multiple failed Windows authentication attempts
followed by successful logon events.

Determine whether the activity represents suspicious
authentication behavior or legitimate user activity.

## Evidence

Analysis of Windows Security Event Logs identified:

- Four failed authentication events (Event ID 4625).
- Two successful logon events (Event ID 4624).
- Target account: Anr.
- Logon Type: 2 (Interactive).
- Source IP: 127.0.0.1.
- Failure Sub Status: 0xC000006A (Incorrect password).

### Event Timeline

| Time | Event ID | Description |
|------|----------|-------------|
| 18:19:05 | 4625 | Failed authentication |
| 18:19:07 | 4625 | Failed authentication |
| 18:19:12 | 4625 | Failed authentication |
| 18:19:19 | 4625 | Failed authentication |
| 18:19:25 | 4624 | Successful logon |
| 18:19:25 | 4624 | Successful logon |

Times are displayed in the Splunk search interface.

## Successful Logon Analysis

The two successful events were investigated
using their Windows Security Record Numbers.

Record 70740:
- New Logon ID: 0x2F467D
- Linked Logon ID: 0x2F4702
- Elevated Token: Yes

Record 70741:
- New Logon ID: 0x2F4702
- Linked Logon ID: 0x2F467D
- Elevated Token: No

The events reference each other through
their Linked Logon IDs.

This is consistent with linked Windows logon
sessions with different elevation states.

The two events do not necessarily represent
two separate user login actions.

## Analysis

The authentication sequence initially warranted
investigation because several failed attempts
were followed by successful authentication.

The failed events indicated incorrect passwords.

All investigated events used Logon Type 2,
consistent with interactive authentication.

The lab owner confirmed intentionally entering
incorrect credentials before successfully logging in.

## Assessment

The activity was confirmed as authorized
authentication testing conducted in a personal lab.

No evidence of a brute-force attack was identified
in the reviewed events.

**Final Classification: Benign Activity**

## Conclusion

This investigation demonstrates the importance
of correlating Windows authentication events,
reviewing raw log data, and validating activity
before classifying it as malicious.

The investigation was performed in a controlled
personal SOC laboratory.
