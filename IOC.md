# 🔎 Indicators of Compromise (IOC)

This document summarizes the key indicators identified during the Active Directory incident response simulation.

The indicators were identified by correlating Windows Security Logs, Sysmon telemetry, authentication activity, account changes, network share access, and centralized Splunk logs.

---

## 🌐 Network Indicators

| Indicator | Type | Description |
|---|---|---|
| `192.168.1.186` | IP Address | Kali Linux attacker machine / source of malicious activity |
| `192.168.1.191` | IP Address | Windows Server / Active Directory Domain Controller |

The attacker activity consistently originated from `192.168.1.186`, including authentication attempts and subsequent remote access activity. :contentReference[oaicite:1]{index=1}

---

## 👤 Account Indicators

| Account | Status | Significance |
|---|---|---|
| `Trent` | Compromised | Legitimate domain account used to obtain initial access and later elevated privileges |
| `Administrator` | Compromised | Privileged account involved during the attack |
| `SAMADT` | Unauthorized / Created | Secondary privileged account created for persistence |

The investigation identified `Trent` as the compromised account and `SAMADT` as a newly created privileged account used to maintain access. :contentReference[oaicite:2]{index=2}

---

## 🔐 Authentication Indicators

### Password Spraying

Multiple failed authentication attempts were observed against the `Trent` account from:

```text
Source IP: 192.168.1.186
Account: Trent
Event ID: 4625

These failed attempts were followed by a successful authentication:

Event ID: 4624
Account: Trent
Logon Type: Network Logon
Source IP: 192.168.1.186
Authentication: NTLM

```

---

## 👑 Privilege Escalation Indicators
The following events were correlated during the privilege escalation investigation:

Event ID	Significance
4624	Successful logon
4672	Special privileges assigned
4728	Account added to security-enabled global group
4732	Account added to security-enabled local group
4756	Account added to security-enabled universal group

The investigation showed that Trent was elevated to Domain Administrator privileges.

---



## 🧑‍💻 Persistence Indicators

A new Active Directory account was created:

```
Account: SAMADT
Created By: Trent
Event ID: 4720

```

The newly created account was subsequently added to the Domain Admins group.
Relevant events included:
```
4720
4728
4732
4756

```

This activity established a secondary privileged account that could be used to maintain access if the original compromised account was disabled.

---

📁 Data Access Indicators

The attacker used the compromised administrative privileges to access the Domain Controller's administrative SMB share:
```
\\192.168.1.191\C$

```
The investigation identified the Cyberfolder directory as containing potentially sensitive organizational files, including:
SecurityDatabase.txt
Memo.txt
new cyber text.txt
Network share activity was investigated using Windows Security Event ID 5140.

---

🧹 Defense Evasion Indicators

The attacker attempted to remove forensic evidence by clearing Windows Event Logs.
The relevant indicators were:

| Event ID | Description                        |
| -------- | ---------------------------------- |
| `1102`   | Security audit log was cleared     |
| `104`    | System/Application log was cleared |

The centralized Splunk environment had already collected relevant events through the Universal Forwarder, allowing investigators to continue reconstructing the attack despite the local log-clearing activity.

---

📊 Key Detection Events

The following Event IDs were particularly important during the investigation:
4624  - Successful Logon
4625  - Failed Logon
4672  - Special Privileges Assigned
4720  - User Account Created
4728  - Added to Security Group
4732  - Added to Local Security Group
4756  - Added to Universal Security Group
4776  - Credential Validation
5140  - Network Share Access
1102  - Security Log Cleared
104   - System/Application Log Cleared

Correlation of these events allowed the Blue Team to reconstruct the attack from initial access through privilege escalation, persistence, data access, and defense evasion.

---

🛡️ IOC Response Actions

During the simulated incident response process, the following actions were recommended or performed:

Block the attacking IP address.
Disable compromised accounts.
Reset compromised credentials.
Remove the unauthorized SAMADT account.
Revoke Trent's unauthorized Domain Admin privileges.
Terminate active remote sessions.
Isolate the Domain Controller from the network.
Review Active Directory privileged group memberships.
Verify centralized logging and continued security monitoring.

These actions formed part of the containment, eradication, and recovery process documented in the full incident response report.

---

📌 Summary

The investigation identified a combination of network, account, authentication, privilege, persistence, file-access, and log-clearing indicators.

The most significant indicators were:

Attacker IP: 192.168.1.186
Compromised account: Trent
Unauthorized privileged account: SAMADT
Target Domain Controller: 192.168.1.191
Password spraying: 4625 → 4624
Privilege escalation: 4672, 4728, 4732, 4756
Account creation: 4720
SMB access: 5140
Log clearing: 1102, 104






