# 🔓 PortSwigger — IDOR | Broken Access Control


---


## 📌 Overview

| Field | Details |
|---|---|
| Platform | PortSwigger Web Security Academy |
| Category | Broken Access Control |
| Vulnerability | Insecure Direct Object Reference (IDOR) |
| Focus | Authorization Testing |
| Tool | Burp Suite |


---


## 🧭 Attack Path

**Observe Resource Request → Identify Predictable Object Reference → Modify Identifier → Access Unauthorized Resource → Credential Exposure → Account Compromise**


---


## 🎯 Objective

The goal of this lab is to exploit an Insecure Direct Object Reference (IDOR) vulnerability to access sensitive data belonging to another user and use it to compromise their account.


## 🧠 What is IDOR?

An Insecure Direct Object Reference (IDOR) is a type of access control vulnerability that occurs when an application exposes internal objects, such as files, database records, or user IDs, without proper authorization checks.

An attacker can manipulate these references to access resources that belong to other users.


## 🔍 Recon

The application provides a live chat feature that allows users to communicate and download chat transcripts.

After interacting with the chat and selecting the "View transcript" option, a request was observed in Burp Suite's HTTP History showing a 'GET' request to a transcript file.


## 💥 Exploitation

The identified request was sent to a Burp Repeater for further analysis.

It was observed that the application retrieves chat transcripts using a numeric identifier in the URL, such as '/download-transcript/5.txt'.

By modifying this identifier, it was possible to access transcripts belonging to other users.

When changing the value to 'download-transcript/1.txt', a transcript containing sensitive information was retrieved, including Carlos's password.


## 🎯 Result

Sensitive information from another user's chat transcript was successfully accessed, including login credentials. The application does not verify whether the requested file belongs to the authenticated user.

This demonstrates a lack of proper access control, allowing unauthorized users to retrieve data that does not belong to them.


## ⚠️ Impact

An attacker can access sensitive data from other users by manipulating direct object references.

This can lead to credential exposure and potential account compromise.


## 🧠 Key Takeaways

- IDOR vulnerabilities occur when applications fail to enforce proper access control
- Direct object references must always be protected by server-side authorization checks.
- Sensitive data can be exposed by simply modifying identifiers
- Proper authorization checks are critical when accessing user-specific resources


## 🛡️ Mitigation

- Enforce server-side authorization checks on every request for user-specific resources.
- Verify that the authenticated user is authorized to access the requested object.
- Do not rely on unpredictable or hidden identifiers as an access control mechanism.
- Apply the principle of least privilege when exposing sensitive user data.
- Perform regular access control testing across endpoints that reference user-owned resources.




## 📸 Screenshots



### Chat Interface

![Chat](images/chat-interface.png)


### HTTP History - Transcript Request

![History](images/http-history.png)


### Burp Repeater - Modified Request

![Repeater](images/idor-request.png)


### Sensitive Data Retrieved

![Data](images/sensitive-data.png)


### Lab Solved

![Solved](images/lab-solved.png)
















