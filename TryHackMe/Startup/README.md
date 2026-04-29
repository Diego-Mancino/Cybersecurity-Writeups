




## 📖 Introduction

This writeup documents the process of compromising the **Startup** machine from TryHackMe.

The lab focuses on exploiting a misconfigured FTP service that allows file upload, leading to Remote Code Execution (RCE). Further enumeration reveals sensitive network traffic containing credentials, which are used to gain access to another user and escalate privileges to root.


## 🔍 Reconnaissance

The first step is to identify open ports and exposed services on the target machine. This helps us understand the attack surface and identify potential entry points.

To achieve this, an Nmap scan was performed using the following command:

```bash
nmap -sC -sV 10.129.140.31
```

This scan revealed several open ports and services:

- FTP (21/tcp) -> Anonymous login enabled
- SSH (22/tcp)
- HTTP (80/tcp)

The FTP service immediately stands out as a potential entry point. The scan indicates that anonymous access is allowed and reveals the presence of files such as:

- `important.jpg`
- `notice.txt`

This suggests that the FTP server is misconfigured and may allow file interaction, making it a strong candidate for initial access.

Although the web service (port 80) is also available, no useful information is observed at this stage, so the focus remains on the FTP service for further exploitation.


## 📂 Enumeration

To continue the assessment, the FTP service was accessed using anonymous credentials:

```bash
ftp 10.129.140.31
```

Anonymous login was successful, confirming the misconfiguration identified during the reconnaissance phase.

Once inside the FTP server, basic enumeration was performed using commands such as:

```bash
ls
```

Although some files were present, they did not provide any immediately useful information. However, further inspection revealed that the `ftp` directory had write permissions, allowing file uploads.

At this point, attention shifted to the web service to understand how uploaded files might be exposed.

Directory enumeration was performed using Gobuster:
```bash
gobuster dir -u http://10.129.140.31 -w /usr/share/wordlists/dirb/small.txt
```

This revealed the `/files` directory.

Accessing this directory in the browser showed that it was linked to the FTP upload location. More specifically:

```bash
htttp://10.129.140.31/files/ftp/
```

This indicates that the files uploaded via FTP are publicly accesible through the web server, creating a potential path for exploitation.

















