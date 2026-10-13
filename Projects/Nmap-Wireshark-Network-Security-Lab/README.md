# Network Vulnerability Detection & Traffic Analysis — Nmap, NSE & Wireshark


## Overview

This project documents a hands-on network security assessment performed in a controlled VirtualBox lab using Kali Linux and Metasploitable2.

The assessment combined Nmap, NSE, and Wireshark to identify exposed services, detect vulnerable software, analyze network traffic, and demonstrate the security impact of unencrypted protocols.

The workflow included full TCP port scanning, targeted service and version enumeration, operating system and SMB discovery, vulnerability validation with Nmap NSE scripts, and packet analysis of FTP and HTTP communications.

The objective was to understand how exposed services and insecure network protocols can increase attack surface, reveal sensitive information, and create opportunities for exploitation.



## Scope

The assessment was performed exclusively within an isolated VirtualBox laboratory environment.

The scope included:

- Discovery of active hosts and exposed TCP services
- Full TCP port scanning against the Metasploitable2 target
- Service and version enumeration
- Operating system and SMB discovery
- Targeted vulnerability detection using Nmap NSE scripts
- Validation of selected vulnerable services
- Capture and analysis of network traffic with Wireshark
- Inspection of FTP and HTTP communications transmitted without encryption
- Reconstruction of content transferred through HTTP

The target system was a deliberately vulnerable Metasploitable2 virtual machine used exclusively for cybersecurity training.

No testing was performed against external or production systems.



## Lab Environment

The assessment was conducted in an isolated VirtualBox environment using two virtual machines connected through a Host-Only network.

| Machine | Role | IP Address | Network Configuration |
|---|---|---|---|
| Kali Linux | Security assessment workstation | `192.168.100.50` | Host-Only + Bridged Adapter |
| Metasploitable2 | Vulnerable target system | `192.168.100.100` | Host-Only |

Kali Linux was used to run Nmap, NSE scripts, and Wireshark for reconnaissance, vulnerability detection, and traffic analysis.

Metasploitable2 was used as the intentionally vulnerable target system.

The Host-Only network isolated the laboratory traffic from external systems, while the Bridged Adapter on Kali Linux provided Internet connectivity when required for updates and tool access.

This configuration allowed all scanning and packet-analysis activities to be performed safely within a controlled environment.



## Methodology

The assessment followed a structured workflow combining network reconnaissance, targeted vulnerability validation, and traffic analysis:

1. **Full TCP port scanning** to identify exposed services.
2. **Service and version enumeration** on relevant open ports.
3. **SMB and host discovery** using targeted Nmap NSE scripts.
4. **Vulnerability validation** against selected vulnerable services.
5. **Traffic capture and protocol analysis** with Wireshark.
6. **Cleartext communication review** for FTP and HTTP traffic.
7. **HTTP object reconstruction** from captured network traffic.
8. **Security analysis and remediation recommendations** based on the identified findings.


## Network Discovery & Port Scanning

The first stage of the assessment focused on identifying the exposed TCP attack surface of the Metasploitable2 target.

A full TCP SYN scan was performed against `192.168.100.100` to enumerate all open ports across the complete TCP port range.

The scan revealed numerous exposed services, confirming that the target presented a broad attack surface suitable for further service enumeration and vulnerability analysis.

Rather than immediately performing aggressive vulnerability checks against every port, the results were used to select relevant services for deeper inspection in the following stages.


## OS & Service Detection

After identifying the exposed TCP ports, targeted service and version detection was performed against the most relevant services.

Nmap identified multiple network services and software versions, including:

- vsFTPd 2.3.4 on FTP
- OpenSSH 4.7p1
- Apache HTTP Server
- Samba / SMB services
- MySQL
- VNC
- Apache Tomcat

Additional SMB discovery was performed using Nmap NSE to obtain host and system information from the target.

This stage provided the context required to identify outdated or vulnerable services and determine which findings required targeted validation.


## NSE Vulnerability Detection

After identifying potentially vulnerable services, targeted Nmap NSE scripts were used to validate selected findings.

The FTP service on port `21` was identified as running **vsFTPd 2.3.4**, a version known to contain a backdoor.

A dedicated NSE check was performed using the `ftp-vsftpd-backdoor` script.

The script confirmed that the service was vulnerable and reported successful interaction with the backdoor, demonstrating the potential for remote command execution with root privileges.

This stage showed the value of moving from broad enumeration to targeted validation rather than relying only on service version information.



## Wireshark Traffic Capture

After completing the Nmap reconnaissance and vulnerability-validation stages, network traffic between Kali Linux and Metasploitable2 was captured using Wireshark.

Traffic was generated intentionally using several protocols, including:

- ICMP
- FTP
- HTTP

The capture was performed on the Host-Only interface used by the isolated laboratory network.

This allowed the communication between both virtual machines to be analyzed without unrelated external network traffic.

The captured packets were later filtered and reviewed to identify insecure communications and data transmitted without encryption.


## Cleartext Credential Exposure

FTP traffic captured with Wireshark showed that authentication data was transmitted without encryption.

By filtering the capture for FTP traffic, the `USER` and `PASS` commands could be observed directly in the packet contents.

This demonstrated that credentials sent through FTP can be exposed to anyone with access to the same network segment.

The analysis confirmed that legacy cleartext protocols significantly increase the risk of credential interception and unauthorized access.


## HTTP Traffic Analysis & Object Reconstruction

HTTP traffic captured between Kali Linux and Metasploitable2 was analyzed with Wireshark to identify information transmitted without encryption.

By filtering the capture for HTTP traffic, requests such as `GET` could be inspected directly, including requested paths and application resources.

Because the traffic was transmitted in cleartext, Wireshark was also able to identify and export HTTP objects transferred during the session.

A reconstructed image was successfully extracted from the packet capture, demonstrating that unencrypted HTTP traffic can expose complete application content to anyone able to observe the network communication.

This highlights the importance of using HTTPS to protect both user data and application resources in transit.



## Security Findings

The assessment identified several security weaknesses across exposed services and network communications.

### Key Findings

- **Broad TCP attack surface**  
  The Metasploitable2 host exposed numerous TCP services, increasing the number of potential entry points available to an attacker.

- **Outdated and vulnerable services**  
  Service enumeration identified legacy software versions, including **vsFTPd 2.3.4**, which was later validated as vulnerable through a targeted NSE check.

- **Insecure remote and application protocols**  
  Services such as FTP and HTTP transmitted information without encryption.

- **Cleartext credential exposure**  
  FTP authentication commands, including `USER` and `PASS`, were visible directly in captured network traffic.

- **Unencrypted HTTP content exposure**  
  HTTP requests and transferred objects could be inspected and reconstructed from packet captures.

- **Information disclosure through exposed services**  
  Service banners, software versions, SMB information, and host details provided useful reconnaissance data that could assist further attack planning.

These findings demonstrate how excessive service exposure, outdated software, and unencrypted protocols can combine to significantly increase a system's attack surface.


## Mitigation Recommendations

Based on the identified findings, the following mitigation measures were recommended:

- **Reduce unnecessary service exposure** by disabling services that are not operationally required.
- **Patch or upgrade vulnerable software**, including outdated services such as vsFTPd 2.3.4.
- **Replace cleartext protocols** such as FTP and HTTP with encrypted alternatives like SFTP/FTPS and HTTPS.
- **Restrict remote and network-accessible services** using firewall rules and network segmentation.
- **Harden exposed services** by reviewing default configurations, unnecessary banners, and insecure settings.
- **Protect authentication traffic** by ensuring credentials are never transmitted over unencrypted protocols.
- **Apply secure protocol configurations** and remove legacy or obsolete services where possible.
- **Monitor network traffic** for unusual connections, exposed credentials, and suspicious communication patterns.
- **Perform regular vulnerability assessments** to detect outdated software, exposed services, and configuration weaknesses.

These measures would reduce the attack surface, protect sensitive information in transit, and decrease the likelihood of successful exploitation.



## Conclusion

This project demonstrated how network reconnaissance and packet analysis can be combined to identify security weaknesses within a controlled laboratory environment.

Nmap and NSE were used to map the target's exposed attack surface, identify vulnerable services, and validate selected findings. Wireshark was then used to analyze FTP and HTTP traffic, revealing cleartext credentials and reconstructable application content.

The assessment showed that outdated services, excessive exposure, and unencrypted protocols can significantly increase security risk.

Overall, the exercise reinforced the importance of combining service enumeration, targeted vulnerability validation, and network traffic analysis to better understand how weaknesses can be identified and mitigated.


## Lessons Learned

This project reinforced several important network-security principles:

- Broad service exposure increases the number of potential attack paths.
- Service and version enumeration provides valuable context for identifying vulnerable software.
- Targeted NSE scripts can help validate suspected vulnerabilities without relying only on banner information.
- Cleartext protocols such as FTP and HTTP can expose credentials, requests, and application content.
- Packet analysis can reveal information that is not always visible through vulnerability scanners alone.
- Security assessments are more effective when reconnaissance, vulnerability validation, and traffic analysis are combined.
- Reducing attack surface, patching vulnerable services, and enforcing encrypted protocols are essential mitigation measures.















