🛡️ Active Directory Incident Response Lab
> **A hands-on Red Team vs Blue Team cybersecurity lab focused on Active Directory attack simulation, SIEM-based detection, incident investigation, and response.**



## 📌 Project Overview

This project is a full incident response simulation conducted in an isolated Active Directory lab environment.

The objective was to simulate a realistic attack against a Windows Active Directory Domain Controller from a Kali Linux attacker machine, while using Splunk Enterprise, Sysmon, and Windows Security Logs to detect, investigate, and reconstruct the attack.

Rather than focusing only on offensive techniques, the project follows the complete security operations workflow:

**Reconnaissance → Identity Discovery → Initial Access → Discovery → Privilege Escalation → Persistence → Data Exfiltration → Defense Evasion → Investigation**

The exercise demonstrates how attacker activity can leave behind security telemetry and how a SOC analyst can correlate those events to understand what happened, identify indicators of compromise (IOCs), reconstruct the attack timeline, and recommend appropriate response actions.

---


## 🎯 Project Objectives

The objectives of this project were to:

- Build a small Active Directory lab environment
- Simulate a realistic attack against a Windows Domain Controller
- Perform reconnaissance and identity discovery
- Simulate password spraying and unauthorized authentication
- Detect suspicious activity using Splunk Enterprise
- Investigate Windows Security Events and Sysmon logs
- Correlate multiple security events during an investigation
- Reconstruct the complete attack timeline
- Identify Indicators of Compromise (IOCs)
- Map observed attack activity to relevant MITRE ATT&CK techniques
- Recommend containment, eradication, and recovery actions

---



## 🖥️ Lab Environment

| Component | Technology |
|---|---|
| Attacker Machine | Kali Linux |
| Target Machine | Windows Server — Active Directory Domain Controller |
| SIEM | Splunk Enterprise |
| Endpoint Monitoring | Sysmon |
| Log Collection | Splunk Universal Forwarder |

The attack simulation was performed inside an isolated lab environment to safely reproduce attacker behavior and investigate the resulting security events.

---


## ⚔️ Attack Lifecycle

The simulation covered the following stages:

1. **Reconnaissance**
2. **Username Enumeration**
3. **Password Spraying**
4. **Initial Access**
5. **Discovery**
6. **Privilege Escalation**
7. **Persistence**
8. **Data Exfiltration**
9. **Defense Evasion**

Each phase included both simulated attacker activity and defensive investigation using collected security telemetry.

---


## 🔍 SOC Investigation Approach

The investigation followed a structured incident response process:

```text
Attack Simulation
       ↓
Security Telemetry Generated
       ↓
Splunk Detection
       ↓
Event Correlation
       ↓
Investigation
       ↓
Attack Timeline Reconstruction
       ↓
IOC Identification
       ↓
Containment & Response Recommendations

---



# 📸 Project Screenshots

## Lab Environment

<img width="745" height="388" alt="sscreenshots/01-lab-environment.png" src="https://github.com/user-attachments/assets/319c162d-5868-4ec6-9512-15cc8959af81" />




## Reconnaissance

Using Nmap, the attacker identified exposed services running on the Domain Controller.

<img width="1440" height="900" alt="screenshots/02-nmap-scan.png" src="https://github.com/user-attachments/assets/f456a1bd-2a4c-46ba-afcf-52c2af9b2663" />

---

## Username Enumeration

Valid Active Directory usernames were identified before attempting authentication attacks.

<img width="2880" height="1800" alt="screenshots/03-kerbrute-enumeration.png" src="https://github.com/user-attachments/assets/e7f0b988-ecb7-49be-8466-51b6fea7a3b0" />


---

## Password Spraying Detection

Splunk detected multiple failed logon attempts followed by a successful authentication using Windows Event IDs **4625** and **4624**.

<img width="2880" height="1800" alt="screenshots/04-password-spraying.png" src="https://github.com/user-attachments/assets/d94dc475-e5fc-4033-a4b0-723ea2440e7f" />
<img width="2880" height="1800" alt="screenshots:004-password-spraying" src="https://github.com/user-attachments/assets/f9f50f90-dc09-410f-9f66-e4a54af76913" />



---

## Privilege Escalation

After gaining access, the compromised account was added to the Domain Admins group. Splunk captured the related security events used to investigate the privilege escalation.


<img width="2880" height="1800" alt="screenshots/05-privilege-escalation.png" src="https://github.com/user-attachments/assets/0b8b5057-8379-48c5-896e-bd04f381ebb7" />
<img width="2880" height="1800" alt="screenshots:005-privilege-escalation" src="https://github.com/user-attachments/assets/91d85a54-bf23-4760-b60f-65792b1dd583" />
<img width="2880" height="1800" alt="screenshots:015-privilege-escalation" src="https://github.com/user-attachments/assets/0b488542-0bd4-4c89-9252-328946f5b4f6" />




---

## Persistence

To maintain long-term access, a new privileged account was created. Windows Security Events were used to identify the account creation and group membership changes.


<img width="1440" height="900" alt="screenshots/06-persistence.png" src="https://github.com/user-attachments/assets/e35d5d93-67df-43cf-9cd1-ac33614b7c25" />
<img width="1440" height="900" alt="screenshots:006-persistence" src="https://github.com/user-attachments/assets/0ddb7735-b7c0-4197-bc65-fb2260bcc88d" />
<img width="1440" height="900" alt="screenshots:106-persistence" src="https://github.com/user-attachments/assets/5d3341f8-2675-4996-86c2-69bc9cd7ea81" />


 


---

## Data Exfiltration

The attacker accessed the administrative SMB share and copied sensitive files from the Domain Controller. Splunk logs helped identify the unauthorized network share access.

<img width="1440" height="900" alt="screenshots/07-data-exfiltration.png" src="https://github.com/user-attachments/assets/7a750023-78a6-4745-b70d-58a37e983905" />
<img width="1440" height="900" alt="screenshots/007-data-exfiltration.png" src="https://github.com/user-attachments/assets/b3edc54e-8cf2-4e97-b2d4-734c4dbbde6a" />




---

## Defense Evasion

The attacker attempted to clear the Windows Event Logs to hide their activity. Despite this, Splunk preserved the logs before they were deleted, allowing the investigation to continue.

<img width="1440" height="900" alt="screenshots/08-defense-evasion.png" src="https://github.com/user-attachments/assets/767eb104-6d51-4548-9e2b-6249fd435c7d" />
<img width="1440" height="900" alt="screenshots:008-defense-evasion" src="https://github.com/user-attachments/assets/d73f5ba2-b96c-4dca-856a-43805e25d633" />


---

## Incident Timeline

The investigation reconstructed the complete attack timeline from reconnaissance to defense evasion.

<img width="737" height="456" alt="screenshots/09-incident-timeline.png" src="https://github.com/user-attachments/assets/8017e75c-1fc5-4c28-91d3-016fbce75e5d" />



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
