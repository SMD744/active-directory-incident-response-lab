# Active Directory Incident Response Lab

## Overview

This project was completed as my final project during the ElevateUTTech Cybersecurity Bootcamp.

The goal was to simulate a complete cyber attack against an Active Directory environment and investigate the attack from a SOC analyst's perspective using Splunk Enterprise, Sysmon, and Windows Security Logs.

Rather than focusing only on the attack, this project demonstrates how security teams can detect, investigate, and respond to malicious activity by analyzing log data and reconstructing the attack timeline.

---

## Lab Environment

| Component | Technology |
|-----------|------------|
| Attacker Machine | Kali Linux |
| Target | Windows Server (Active Directory Domain Controller) |
| SIEM | Splunk Enterprise |
| Endpoint Monitoring | Sysmon |
| Log Collection | Splunk Universal Forwarder |

---

## Project Objectives

During this project I wanted to:

- Simulate a realistic attack against an Active Directory environment.
- Detect attacker activity using Splunk.
- Investigate Windows Security and Sysmon logs.
- Reconstruct the complete attack timeline.
- Identify Indicators of Compromise (IOCs).
- Recommend containment, eradication, and recovery actions.

---

## Attack Lifecycle

The simulation follows the complete attack lifecycle:

- Reconnaissance
- Identity Discovery
- Password Spraying
- Initial Access
- Discovery
- Privilege Escalation
- Persistence
- Data Exfiltration
- Defense Evasion

Each phase includes both the attacker's actions and the Blue Team investigation.

---

## Detection

Throughout the investigation I analyzed several important Windows Security Events, including:

- Event ID 4624 – Successful Logon
- Event ID 4625 – Failed Logon
- Event ID 4672 – Special Privileges Assigned
- Event ID 4720 – User Account Created
- Event ID 4728 / 4732 – Privileged Group Membership Changes
- Event ID 4776 – Credential Validation
- Event ID 5140 – Network Share Access
- Event ID 1102 – Security Log Cleared
- Event ID 104 – System/Application Log Cleared

---

## Tools Used

- Splunk Enterprise
- Sysmon
- Windows Event Logs
- Kali Linux
- Nmap
- NetExec
- Kerbrute
- SMBClient
- Evil-WinRM
- Impacket
- xfreerdp

---

## Screenshots

The repository includes screenshots showing:

- Lab environment
- Password spraying detection
- Successful authentication
- Privilege escalation
- Persistence
- Data exfiltration
- Defense evasion
- Incident timeline

---

## Skills Demonstrated

This project helped me strengthen my skills in:

- Security Operations (SOC)
- Incident Response
- Threat Detection
- Log Analysis
- Active Directory Security
- Windows Event Analysis
- Splunk SPL
- Threat Hunting
- Digital Forensics

---

## Key Takeaways

One of the biggest lessons from this project was seeing how valuable centralized logging is during an investigation.

Although the attacker cleared the local Windows Event Logs, Splunk had already collected the relevant events through the Universal Forwarder. This made it possible to reconstruct the attack timeline, identify the compromised accounts, and understand exactly how the attacker moved through the environment.

This project also reinforced the importance of strong password policies, least privilege, continuous monitoring, and proactive detection.

---

## Repository Contents

```
docs/
    Incident_Response_Simulation_Full_Attack_Lifecycle.pdf

screenshots/
    Project screenshots

splunk/
    SPL search queries

IOC.md
MITRE.md
README.md
```

---

## About This Project

This project represents the practical skills I developed during the ElevateUTTech Cybersecurity Bootcamp.

It reflects my ability to build a lab environment, simulate real-world attack scenarios, investigate security events, and document the findings in a structured and professional manner.

I look forward to continuing to grow my skills in Security Operations, Incident Response, and Threat Detection.
