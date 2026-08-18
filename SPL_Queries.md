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

Events Investigated

| Event ID | Description                          |
| -------- | ------------------------------------ |
| 1102     | Security Event Log cleared           |
| 104      | System/Application Event Log cleared |

### Investigation Finding

The query identified the log-clearing activity performed during the defense evasion phase.

Event ID 1102 showed that the Trent account was associated with the Security log clearing activity. Event ID 104 indicated that the System and Application logs had also been cleared.

The events had already been forwarded to Splunk before the local logs were cleared, allowing the SOC investigation to continue.


## 🔐 Password Spraying Investigation
Objective

Investigate repeated failed authentication attempts and identify a successful authentication following the failures.

## Events Investigated
4625 — Failed Logon
4624 — Successful Logon

## Investigation Pattern
Multiple 4625 events
        ↓
Same account / source
        ↓
Successful 4624 event
        ↓
Valid credentials obtained

The investigation identified repeated failed authentication attempts against the Trent account originating from 192.168.1.186, followed by a successful authentication.

This sequence was used as evidence of the simulated password spraying attack.

## 👑 Privilege Escalation Investigation

## Objective

Identify changes that resulted in the compromised account obtaining elevated privileges.

## Events Investigated
4624 — Successful Logon
4672 — Special Privileges Assigned
4728 — Account Added to Security Group
4732 — Account Added to Local Security Group
4756 — Account Added to Universal Security Group


## Investigation Pattern
Successful Authentication
        ↓
Special Privileges Assigned
        ↓
Privileged Group Modification
        ↓
Domain Administrator Access


The investigation correlated these events to determine that the compromised Trent account had been elevated to Domain Administrator privileges.

---

## 🧑‍💻 Persistence Investigation
## Objective

Identify the creation of a new privileged account and changes to privileged group membership.

## Events Investigated

4720 — User Account Created
4728 — Added to Security Group
4732 — Added to Local Security Group
4756 — Added to Universal Security Group

## Key Account
Account: SAMADT
Created By: Trent

The investigation showed that SAMADT was created and subsequently added to the Domain Admins group.

This activity established a secondary privileged account that could be used to maintain access to the environment.

---
## 📁 SMB / Data Access Investigation
## Objective

Investigate suspicious access to the Domain Controller's administrative SMB share.

## Event Investigated
5140 — Network Share Access

## Key Evidence
Account: Trent
Source IP: 192.168.1.186
Share: \\*\C$

The investigation correlated the SMB access with earlier authentication and privilege escalation events.

The sequence:
4624
  ↓
4672
  ↓
5140

helped establish that the compromised administrative account accessed the Domain Controller's administrative share.

The investigation determined that SecurityDatabase.txt was retrieved during the simulated data exfiltration phase.

## 🔎 Credential Validation
## Event Investigated
4776 — Credential Validation

Event ID 4776 was reviewed as part of the authentication and discovery investigation to provide additional context around credential validation activity.

## 📊 Attack Timeline Correlation
The investigation correlated events across multiple attack stages rather than relying on a single event.

| Attack Stage         | Evidence                                        |
| -------------------- | ----------------------------------------------- |
| Reconnaissance       | Nmap / network service discovery                |
| Identity Discovery   | SMB enumeration / Kerberos username enumeration |
| Initial Access       | 4625 → 4624                                     |
| Discovery            | 4624 / 4776                                     |
| Privilege Escalation | 4728 / 4672                                     |
| Persistence          | 4720 / 4728                                     |
| Data Exfiltration    | 5140                                            |
| Defense Evasion      | 1102 / 104                                      |


This correlation allowed the Blue Team to reconstruct the attack from initial reconnaissance through defense evasion.

## 🛡️ Defensive Value
The investigation demonstrated the importance of centralized logging and event correlation.

Even after the attacker cleared the local Windows Event Logs, the relevant events had already been collected by the Splunk Universal Forwarder and indexed by Splunk Enterprise.

This allowed the investigation to:

> Identify the compromised account
> Identify the attacker's source IP
> Detect privilege escalation
> Identify the unauthorized privileged account
> Detect administrative SMB access
> Detect log-clearing activity
> Reconstruct the attack timeline
> Support containment and remediation decisions

















