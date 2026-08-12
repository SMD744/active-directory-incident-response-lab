# 🔎 Splunk SPL Queries

This document contains the Splunk searches used and documented during the Active Directory Incident Response investigation.

The queries were used to investigate Windows Security Events, identify suspicious activity, and reconstruct the attack timeline.

---

## 🧹 Windows Event Log Clearing

### Objective

Identify attempts to clear the Windows Security, System, and Application logs.

### SPL Query

```spl
index=main (EventCode=1102 OR EventCode=104)
| table _time host EventCode Message
| sort -_time

```
