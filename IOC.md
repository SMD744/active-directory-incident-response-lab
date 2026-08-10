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




dfkjbjkefnifelknef
