


## Introduction

This writeup documents the exploitation process of the TryHackMe **LazyAdmin** machine.

The objective of this challenge was to identify exposed services, enumerate the web application, gain initial access, and escalate privileges to obtain full system compromise.

The attack path involved discovering hidden web content, obtaining sensitive credentials from exposed files, abusing file upload functionality to obtain a reverse shell, and leveraging misconfigured sudo permissions for privilege escalation.


## Reconnaissance

An initial Nmap scan was performed to identify open ports, running services, and potential attack vectors on the target machine.

```bash
nmap -sC -sV -T4 -O 10.129.167.91
```

The scan revealed that the target exposed an HTTP service on port 80, indicating the presence of a web application as the primary attack surface.

Service version detection and default script scanning were enabled to gather additional information during the reconnaissance phase.


## Enumeration

### Directory Enumeration

Since the initial web application exposed limited functionality, directory brute-forcing was performed using Gobuster.

```bash
gobuster dir -u http://10.129.167.91 -w /usr/share/wordlists/dirb/common.txt
```

The scan revealed the /content directory, suggesting the presence of additional hidden resources and a possible content management system.

Further enumeration was performed against the newly discovered /content directory.

```bash
gobuster dir -u http://10.129.167.91/content -w /usr/share/wordlists/dirb/common.txt
```

This revealed several interesting directories, including:

**- /as** → administrative login panel
**- /inc** → internal application files and exposed resources


### Sensitive File Discovery

Browsing the `/content/inc` directory exposed several application files and a publicly accessible MySQL backup directory.

Inside the `mysql_backup` directory, a SQL backup file was discovered and downloaded for offline analysis.


### Credential Extraction

Reviewing the SQL dump revealed credentials associated with the `manager` account.

The password was stored as the following MD5 hash:

`42f749ade7f9e195bf475f37a44cafcb`

Because MD5 is considered cryptographically weak and vulnerable to cracking attacks, the hash was successfully recovered using an online hash database.

Recovered credentials:

- Username: `mmanager`
- Password: `Password123`


### Administrative Access

The recovered credentials were used to authenticate to the SweetRice administrative panel located at: `/content/as`.

Successfull authentication granted administrative access to the web application.

















