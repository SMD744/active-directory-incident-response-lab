# 🎯 MITRE ATT&CK Mapping

This document maps the observed activities from the Active Directory incident response simulation to relevant MITRE ATT&CK techniques.

The mapping is based on the activities and evidence documented during the investigation.

---

## Attack Technique Mapping

| Attack Phase | Activity Observed | MITRE ATT&CK Technique |
|---|---|---|
| Reconnaissance | Network scanning to identify exposed services | T1046 – Network Service Scanning |
| Username Enumeration | Identification of valid Active Directory usernames | T1087.002 – Account Discovery: Domain Account |
| Password Spraying | Multiple authentication attempts against domain accounts | T1110.003 – Password Spraying |
| Initial Access | Successful authentication using compromised credentials | T1078 – Valid Accounts |
| Privilege Escalation | Compromised account elevated to Domain Admin privileges | T1098 – Account Manipulation |
| Persistence | Creation of a new privileged account | T1136.002 – Create Account: Domain Account |
| Persistence | Addition of account to privileged groups | T1098.007 – Additional Cloud Roles / Account Manipulation |
| Data Access | Access to administrative SMB share | T1021.002 – SMB/Windows Admin Shares |
| Defense Evasion | Clearing Windows Event Logs | T1070.001 – Clear Windows Event Logs |

---

## 🔎 Reconnaissance

### T1046 — Network Service Scanning

Nmap was used from the Kali Linux attacker machine to identify exposed services on the Active Directory Domain Controller.

The scan identified services including Kerberos, LDAP, SMB, RDP, WinRM, and Global Catalog services.

---

## 👤 Account Discovery

### T1087.002 — Account Discovery: Domain Account

Valid Active Directory usernames were enumerated before authentication attacks were attempted.

The discovered usernames were subsequently used during the password spraying phase.

---

## 🔐 Password Spraying

### T1110.003 — Password Spraying

Multiple failed authentication attempts were observed against the `Trent` account before a successful authentication occurred.

The investigation correlated Windows Event ID 4625 (failed logon) with Event ID 4624 (successful logon).

---

## 🔑 Valid Accounts

### T1078 — Valid Accounts

The attacker successfully authenticated using the compromised `Trent` domain account.

The account was subsequently used for additional activity within the Active Directory environment.

---

## 👑 Privilege Escalation

### Account Manipulation

The compromised account was elevated to Domain Administrator privileges through changes to privileged group membership.

The investigation identified relevant Windows Security Events associated with the privilege change.

---

## 🧑‍💻 Persistence

### T1136.002 — Create Account: Domain Account

A new account named `SAMADT` was created during the attack.

The account was subsequently given elevated privileges, providing an additional method of maintaining access to the environment.

---

## 📁 SMB / Windows Admin Shares

### T1021.002 — SMB/Windows Admin Shares

The attacker accessed the administrative SMB share:

`\\192.168.1.191\C$`

This access allowed files and directories on the Domain Controller to be accessed remotely.

---

## 🧹 Defense Evasion

### T1070.001 — Clear Windows Event Logs

The attacker attempted to clear Windows Event Logs to remove evidence of malicious activity.

The investigation identified Event IDs 1102 and 104 associated with log-clearing activity.

Because the events had already been collected centrally by Splunk, the investigation could continue using the centralized telemetry.

---

## 🛡️ Defensive Perspective

The MITRE ATT&CK mapping demonstrates how individual attacker actions can be connected to a broader attack lifecycle.

By mapping observed behavior to ATT&CK techniques, a SOC analyst can:

- Improve detection coverage
- Identify gaps in monitoring
- Correlate related security events
- Develop threat hunting hypotheses
- Improve incident response procedures
- Recommend appropriate security controls

---

## 📌 Conclusion

The simulation demonstrated multiple stages of an Active Directory attack and showed how Windows Security Events and centralized Splunk telemetry can be used to detect and investigate those activities.

Mapping the observed behavior to MITRE ATT&CK provided a structured way to understand the attacker's techniques and improve defensive monitoring.
