









## 🔎 Reconnaissance

An initial reconnaissance phase was performed to identify exposed services and potential entry points into the target machine.

A network scan was conducted using Nmap to detect open ports, running services, and system information.

nmap -sV -sS -O 10.129.158.61

The scan results revealed that only port 80 (HTTP) was open.

Since this was the only exposed service, the focus of the assessment shifted towards analyzing the web application as the primary attack surface.
























