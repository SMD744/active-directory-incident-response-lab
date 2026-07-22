# 🛡️ Active Directory Incident Response Lab

> **Final Project – ElevateUTTech Cybersecurity Bootcamp**

## Overview

This repository contains my final project completed during the ElevateUTTech Cybersecurity Bootcamp.

The objective of this project was to build a realistic Active Directory lab, simulate a complete cyber attack, and investigate the attack from a Security Operations Center (SOC) analyst's perspective.

Using Splunk Enterprise, Sysmon, and Windows Security Logs, I tracked the attack from the initial reconnaissance phase through privilege escalation, persistence, data exfiltration, and defense evasion. The goal was not only to perform the attack but to understand how defenders can detect, investigate, and respond to malicious activity using log analysis and event correlation.

---

# 🖥️ Lab Environment

| Component | Technology |
|-----------|------------|
| Attacker Machine | Kali Linux |
| Target Machine | Windows Server (Active Directory Domain Controller) |
| SIEM | Splunk Enterprise |
| Endpoint Monitoring | Sysmon |
| Log Collection | Splunk Universal Forwarder |

---

# 🎯 Project Objectives

The objectives of this project were to:

- Build a small Active Directory lab
- Simulate a realistic attack against a Windows Domain
- Detect attacker activity using Splunk Enterprise
- Investigate Windows Security Events and Sysmon logs
- Reconstruct the complete attack timeline
- Identify Indicators of Compromise (IOCs)
- Recommend containment, eradication, and recovery actions

---

# ⚔️ Attack Lifecycle

The simulation covered the following stages:

- Reconnaissance
- Username Enumeration
- Password Spraying
- Initial Access
- Discovery
- Privilege Escalation
- Persistence
- Data Exfiltration
- Defense Evasion

Each phase includes both the Red Team activity and the Blue Team investigation.

---

# 📸 Project Screenshots

## Lab Environment

![Lab Environment](screenshots/01-lab-environment.png)

---

## Reconnaissance

Using Nmap, the attacker identified exposed services running on the Domain Controller.

![Nmap Scan](screenshots/02-nmap-scan.png)

---

## Username Enumeration

Valid Active Directory usernames were identified before attempting authentication attacks.

![Username Enumeration](screenshots/03-kerbrute-enumeration.png)

---

## Password Spraying Detection

Splunk detected multiple failed logon attempts followed by a successful authentication using Windows Event IDs **4625** and **4624**.

![Password Spraying](screenshots/04-password-spraying.png)

---

## Privilege Escalation

After gaining access, the compromised account was added to the Domain Admins group. Splunk captured the related security events used to investigate the privilege escalation.

![Privilege Escalation](screenshots/05-privilege-escalation.png)

---

## Persistence

To maintain long-term access, a new privileged account was created. Windows Security Events were used to identify the account creation and group membership changes.

![Persistence](screenshots/06-persistence.png)

---

## Data Exfiltration

The attacker accessed the administrative SMB share and copied sensitive files from the Domain Controller. Splunk logs helped identify the unauthorized network share access.

![Data Exfiltration](screenshots/07-data-exfiltration.png)

---

## Defense Evasion

The attacker attempted to clear the Windows Event Logs to hide their activity. Despite this, Splunk preserved the logs before they were deleted, allowing the investigation to continue.

![Defense Evasion](screenshots/08-defense-evasion.png)

---

## Incident Timeline

The investigation reconstructed the complete attack timeline from reconnaissance to defense evasion.

![Incident Timeline](screenshots/09-incident-timeline.png)

---

# 🔍 Windows Security Events Investigated

| Event ID | Description |
|-----------|-------------|
| 4624 | Successful Logon |
| 4625 | Failed Logon |
| 4672 | Special Privileges Assigned |
| 4720 | User Account Created |
| 4728 | Added to Security Group |
| 4732 | Added to Local Security Group |
| 4776 | Credential Validation |
| 5140 | Network Share Access |
| 1102 | Security Log Cleared |
| 104 | System/Application Log Cleared |

---

# 🛠️ Tools Used

- Splunk Enterprise
- Sysmon
- Windows Event Viewer
- Windows Security Logs
- Kali Linux
- Nmap
- Kerbrute
- NetExec
- SMBClient
- Evil-WinRM
- Impacket
- xfreerdp

---

# 🧠 Skills Demonstrated

- Incident Response
- Security Monitoring
- Threat Detection
- Threat Hunting
- Log Analysis
- Active Directory Security
- Windows Event Analysis
- Splunk SPL
- Digital Forensics
- MITRE ATT&CK Mapping

---

# 📌 Key Takeaways

Working on this project gave me a better understanding of how attackers move through an Active Directory environment and how defenders can detect those activities using log analysis.

One of the biggest lessons I learned was the importance of centralized logging. Even after the attacker cleared the local Windows Event Logs, Splunk had already collected the relevant events through the Universal Forwarder. This made it possible to reconstruct the attack timeline and understand exactly what happened during the incident.

The project also reinforced the importance of strong password policies, least privilege, continuous monitoring, and timely incident response.

---

# 📂 Repository Structure

```
active-directory-incident-response-lab/

├── README.md
├── LICENSE
├── docs/
│   └── Incident_Response_Simulation_Full_Attack_Lifecycle.pdf
│
├── screenshots/
│   ├── 01-lab-environment.png
│   ├── 02-nmap-scan.png
│   ├── 03-kerbrute-enumeration.png
│   ├── 04-password-spraying.png
│   ├── 05-privilege-escalation.png
│   ├── 06-persistence.png
│   ├── 07-data-exfiltration.png
│   ├── 08-defense-evasion.png
│   └── 09-incident-timeline.png
│
├── IOC.md
└── MITRE.md
```

---

# 🙏 Acknowledgement

This project was completed as my final project during the **ElevateUTTech Cybersecurity Bootcamp**. It reflects the practical skills I developed in building a SOC lab, investigating security events, and responding to simulated attacks in an Active Directory environment.

I'm excited to continue growing my skills in Security Operations, Incident Response, and Threat Detection while taking on more real-world cybersecurity challenges.
