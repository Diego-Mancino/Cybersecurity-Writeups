# Cybersecurity & Offensive Security Portfolio

Welcome to my cybersecurity portfolio.

This repository documents my hands-on practice in **penetration testing, web application security, vulnerability assessment, and privilege escalation** across authorized training environments including **Hack The Box, TryHackMe, and PortSwigger Web Security Academy**.

My goal is not only to document successful exploitation, but to demonstrate the methodology behind the testing process: from reconnaissance and enumeration to vulnerability analysis, exploitation, privilege escalation, impact assessment, and remediation.

---

## ⭐ Featured Projects

Selected projects and write-ups highlighting offensive security, vulnerability assessment, system hardening, and hands-on cybersecurity practice.

### 🔹 Authorized Web Security Assessment — INTECSSA

**Web Security Assessment | Reconnaissance | Service Enumeration | Technology Fingerprinting | Risk Analysis**

An authorized, non-intrusive assessment of INTECSSA's public-facing web environment, covering passive reconnaissance, asset discovery, service enumeration, technology fingerprinting, HTTP security configuration review, manual validation, risk assessment, and remediation recommendations.

➡️ [View Web Security Assessment](./Projects/Web-Security-Assessment-Lab/)


### 🔹 Windows Detection & Monitoring Lab — Wazuh, Sysmon & MITRE ATT&CK

**SOC Operations | Security Monitoring | Windows Event Analysis | MITRE ATT&CK**

Built an isolated Windows monitoring environment using Wazuh and Sysmon. Investigated six controlled security scenarios involving process execution, account activity, authentication failures, network connections, and privileged group modifications.

Analyzed Windows Security and Sysmon telemetry, investigated Wazuh alerts, and validated MITRE ATT&CK mappings, including a level 12 alert triggered by an administrative group membership change.

➡️ [View Windows Detection & Monitoring Lab](Projects/Windows-Detection-Monitoring-Lab/)

### 🔹 Active Directory Offensive Security Lab
Active Directory | Kerberos | AS-REP Roasting | SMB | DCSync | Pass-the-Hash | MITRE ATT&CK
A full domain-compromise chain covering user enumeration, Kerberos pre-authentication abuse, credential recovery, SMB share analysis, domain credential extraction through DRSUAPI, and Pass-the-Hash authentication, including security findings, mitigations, and MITRE ATT&CK mapping.

➡️ [View Active Directory Offensive Security Lab](./Projects/Active%20Directory%20Offensive%20Security%20Lab/)

### 🔹 Windows Server 2022 Hardening — Defensive Security Lab

**Windows Server | Hardening | Microsoft Defender | Firewall | RDP | Security Auditing**

A defensive security project focused on hardening a Windows Server 2022 Domain Controller by reviewing the initial security baseline and strengthening endpoint protection, patch management, firewall configuration, password policies, Remote Desktop exposure, and audit logging.

➡️ [View Windows Server 2022 Hardening Lab](./Projects/Windows-Server-2022-Hardening-Lab/)



### 🔹 Nessus Vulnerability Assessment — Metasploitable2 Lab

**Vulnerability Assessment | Nessus | CVSS | Risk Prioritization | Remediation**

A hands-on vulnerability assessment performed with Nessus Essentials against Metasploitable2 in an isolated lab environment. The project compares basic and advanced scan configurations, reviews findings by severity and technical impact, prioritizes high-risk vulnerabilities, and documents remediation recommendations.

➡️ [View Nessus Vulnerability Assessment Lab](./Projects/Nessus-Vulnerability-Assessment-Lab/)


---


### 🔹 Hack The Box — Cronos

**Linux | DNS Enumeration | SQL Injection | Command Injection | Privilege Escalation**

A complete attack chain beginning with DNS enumeration and zone transfer, followed by authentication bypass through SQL injection, command injection leading to remote code execution, and Linux privilege escalation through an insecure privileged scheduled task.

➡️ [View Cronos Write-up](./HackTheBox/Cronos/)

### 🔹 TryHackMe — Startup

**Linux | FTP | Web Exploitation | Network Traffic Analysis | Privilege Escalation**

A multi-stage compromise involving anonymous FTP access, a writable web-accessible directory, remote code execution through a PHP payload, analysis of captured network traffic with Wireshark, credential discovery, and Linux privilege escalation.

➡️ [View Startup Write-up](./TryHackMe/Startup/)

### 🔹 Hack The Box — Devel

**Windows | FTP | IIS | File Upload | Remote Code Execution | Privilege Escalation**

A Windows penetration testing scenario involving anonymous FTP access to an IIS web root, ASPX payload execution, initial access, and privilege escalation to SYSTEM through a known local vulnerability.

➡️ [View Devel Write-up](./HackTheBox/Devel/)


---


### 🔹 PortSwigger — IDOR

**Web Application Security | Broken Access Control | Authorization**

A focused web security lab demonstrating an Insecure Direct Object Reference (IDOR) vulnerability and how insufficient server-side authorization controls can allow unauthorized access to another user's resources.

➡️ [View IDOR Write-up](./PortSwigger/IDOR/)


---


## 📂 Repository Contents

### Hack The Box

Penetration testing labs covering Linux and Windows systems, web exploitation, service enumeration, remote code execution, and privilege escalation.

➡️ [Browse Hack The Box Write-ups](./HackTheBox/)

---

### TryHackMe

Hands-on security labs covering network enumeration, web security, Linux exploitation, credential discovery, traffic analysis, and privilege escalation.

➡️ [Browse TryHackMe Write-ups](./TryHackMe/)

---

### PortSwigger Web Security Academy

Focused web application security labs covering common vulnerabilities and weaknesses in authentication, authorization, and server-side functionality.

➡️ [Browse PortSwigger Write-ups](./PortSwigger/)

---

### Technical Projects

Hands-on cybersecurity projects focused on vulnerability assessment, system hardening, security analysis, and defensive security.

- [Authorized Web Security Assessment — INTECSSA](./Projects/Web-Security-Assessment-Lab/)
- [Windows Server 2022 Hardening — Defensive Security Lab](./Projects/Windows-Server-2022-Hardening-Lab/)
- [Nessus Vulnerability Assessment — Metasploitable2 Lab](./Projects/Nessus-Vulnerability-Assessment-Lab/)
- [Network Vulnerability Detection & Traffic Analysis — Nmap, NSE & Wireshark](./Projects/Nmap-Wireshark-Network-Security-Lab/)

➡️ [Browse all Technical Projects](./Projects/)

---

## 🎯 Technical Focus

- Penetration Testing & Ethical Hacking
- Web Application Security
- Vulnerability Assessment
- Reconnaissance & Enumeration
- Linux & Windows Security
- Privilege Escalation
- Network Security
- OSINT
- Technical Documentation

---

## 🛠️ Tools & Technologies

### Reconnaissance & Enumeration

Nmap · Gobuster · Nikto · enum4linux · smbclient · dig

### Web Application Security

Burp Suite · SQLmap

### Exploitation & Credential Testing

Metasploit Framework · Hydra · John the Ripper · Netcat

### Network Analysis

Wireshark

### Systems & Scripting

Linux · Windows · Bash · PowerShell

### Utilities

wget · curl

---

## 🔎 Methodology

My write-ups generally follow a structured penetration testing workflow:

**Reconnaissance → Enumeration → Vulnerability Analysis → Exploitation → Privilege Escalation → Impact → Mitigation**

Where relevant, I document not only the commands and tools used, but also the reasoning behind each step, the security impact of the identified weaknesses, and possible remediation measures.

---

## 📚 Platforms

- Hack The Box
- TryHackMe
- PortSwigger Web Security Academy

All exercises documented in this repository were performed in intentionally vulnerable or authorized training environments.

---

## ⚠️ Disclaimer

The content in this repository is provided for **educational and cybersecurity training purposes only**.

All techniques documented here were performed against systems specifically designed or authorized for security testing. They should never be used against systems without explicit authorization.

---

## 👤 About Me

I am a junior cybersecurity professional focused on **Offensive Security, Penetration Testing, Web Security, and Vulnerability Assessment**, currently building my practical experience through continuous hands-on training and technical documentation.

I am currently looking for my first professional opportunity in cybersecurity in **Barcelona, Spain**.

➡️ **LinkedIn:** [Diego Mancino](https://www.linkedin.com/in/diego-mancino/)
