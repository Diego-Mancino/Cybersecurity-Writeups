




## 📖 Introduction

This writeup documents the process of compromising the **Startup** machine from TryHackMe.

The lab focuses on exploiting a misconfigured FTP service that allows file upload, leading to Remote Code Execution (RCE). Further enumeration reveals sensitive network traffic containing credentials, which are used to gain access to another user and escalate privileges to root.


## 🔍 Reconnaissance

The first step is to identify open ports and exposed services on the target machine. This helps us understand the attack surface and identify potential entry points.

To achieve this, an Nmap scan was performed using the following command:

```bash
nmap -sC -sV 10.129.140.31
```

This scan revealed serveal open ports and services:

- FTP (21/tcp) -> Anonymous login enabled
- SSH (22/tcp)
- HTTP (80/tcp)
















