# TryHackMe - LazyAdmin Writeup
---




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

- Username: `manager`
- Password: `Password123`


### Administrative Access

The recovered credentials were used to authenticate against the SweetRice administrative panel located at `/content/as`.

This provided administrative access to the web application.


## Exploitation

### File Upload Abuse

After obtaining administrative access, the functionality of the SweetRice CMS was reviewed for potential file upload abuse.

The `Ads` section allowed arbitrary files to be uploaded and stored inside the web application directory structure. This behavior allowed arbitrary PHP code execution through a reverse shell payload upload.

A Netcat listener was started on the attacking machine:

```bash
nc -lvnp 4444
```

A PHP reverse shell payload was uploaded through the administrative interface.

### Reverse Shell

After uploading the payload, the file became accessible at:

`/content/inc/ads`

Accessing the uploaded PHP file triggered the reverse shell connection back to the attacking machine.

Successful code execution resulted in a shell running as the `www-data` user.


## Privilege Escalation

### Sudo Enumeration

After obtaining a shell as `www-data`, sudo privileges were enumerated using:

```bash
sudo -l
```

The output revealed that the current user was allowed to execute the following Perl script with elevated privileges:

`/usr/bin/perl /home/itguy/backup.pl`


### Exploiting Insecure Script Execution

Inspection of the Perl script revealed that it called the following command:

`system("sh", "/etc/copy.sh");`

Because the `/etc/copy.sh` file was writable by the current user, arbitrary commands could be written and executed with root privileges.

The file was modified to spawn a privileged Bash shell:

`echo 'bash -p' > /etc/copy.sh`

The vulnerable Perl script was then executed with sudo privileges:

`sudo /usr/bin/perl /home/itguy/backup.pl`

Execution of the script resulted in a root shell and full system compromise.


## Conclusion

This machine demonstrated how multiple weaknesses can be chained together to achieve full system compromise.

The attack began with web enumeration, which exposed hidden application directories and publicly accessible backup files containing sensitive information. Weak password storage using MD5 hashing allowed administrative credentials to be recovered successfully.

After gaining access to the administrative panel, an unrestricted file upload functionality within the application allowed arbitrary PHP code execution, leading to a reverse shell as the `www-data` user.

Finally, privilege escalation was possible due to a misconfigured sudo rule that executed a writable script with elevated privileges, resulting in full root access.

This lab highlights the importance of:

- Properly securing sensitive backup files
- Avoiding weak password hashing algorithms such as MD5
- Restricting arbitrary file upload and code execution functionality
- Properly securing scripts executed with elevated privileges

Overall, the machine provides a realistic example of how attackers combine enumeration, credential abuse, remote code execution, and privilege escalation techniques to compromise a Linux-based web server.


## Impact

The vulnerabilities identified in this machine could allow an attacker to fully compromise the target system through a combination of information disclosure, authenticated remote code execution, and privilege escalation.

Successful exploitation could result in:

- Exposure of sensitive information through publicly accessible backup files
- Recovery of weakly hashed credentials (MD5)
- Unauthorized administrative access to the web application
- Remote Code Execution (RCE) through arbitrary PHP file upload
- Full system compromise through privilege escalation to root

An attacker with root privileges would have complete control over the target system, including the ability to modify files, access sensitive data, maintain persistence, and pivot to other systems within the environment.

---

## Mitigation

The following security measures would significantly reduce the risk of compromise:

- Restrict public access to backup files and sensitive application directories
- Avoid weak hashing algorithms such as MD5 for password storage
- Implement secure password policies and multi-factor authentication (MFA)
- Validate and restrict file upload functionality to prevent arbitrary code execution
- Disable execution of uploaded files inside web-accessible directories
- Apply the principle of least privilege to system users and sudo permissions
- Regularly audit scripts executed with elevated privileges
- Monitor web server directories for unauthorized file uploads or modifications

🔒 This lab demonstrates how multiple security weaknesses can be chained together to achieve full system compromise.

