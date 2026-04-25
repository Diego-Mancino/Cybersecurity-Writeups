









## 🔎 Reconnaissance

An initial reconnaissance phase was performed to identify exposed services and potential entry points into the target machine.

A network scan was conducted using Nmap to detect open ports, running services, and system information.

nmap -sV -sS -O 10.129.158.61

The scan results revealed that only port 80 (HTTP) was open.

Since this was the only exposed service, the focus of the assessment shifted towards analyzing the web application as the primary attack surface.


## 🔍 Enumeration & Vulnerability Analysis

To begin the enumeration phase, the **HTTP service** was accessed through a web browser to analyze the application manually.

Further inspection revealed the presence of a **user guide**, which disclosed that the application was running **Fuel CMS version 1.4.1**. This information was critical, as it enabled targeted vulnerability research.

A search for known vulnerabilities affecting this version led to the discovery of a **Remote Code Execution (RCE)** vulnerability (**CVE-2018-16763**). This flaw allows attackers to execute arbitrary system commands via the `filter` parameter in the following endpoint:

```text
/fuel/pages/select/?filter=
```

Additional research across security advisories and exploit databases confirmed that this vulnerability is publicly known and exploitable.

A working exploit was then identified in a public GitHub repository:

👉 [Fuel CMS 1.4.1 RCE Exploit](https://github.com/ice-wzl/Fuel-1.4.1-RCE-Updated/blob/main/Fuel-Updated.py)

This exploit is written in **Python** and leverages the vulnerable endpoint to achieve **remote command execution** on the target system.

The script was downloaded and prepared for use in the next phase of the attack.






















