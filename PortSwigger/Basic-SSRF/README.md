# SSRF - Basic Lab (PortSwigger)

## 🎯 Objective

The goal of this lab is to exploit a Server-Side Request Forgery (SSRF) vulnerability in the stock check functionality to access an internal administrative interface.

## 🧠 What is SSRF?

Server-Side Request Forgery (SSRF) is a vulnerability that allows an attacker to make the server send requests to internal or external systems.
This can be used to access internal services that are not normally accessible from the outside.

## 🔍 Recon

While exploring the application, a "Check stock" feature was identified on the product page.
By intercepting the request using Burp Suite, it was observed that the application uses the 'stockApi' parameter to fetch stock information from an internal system.

## 💥 Exploitation

The 'stockApi' parameter was modified to target internal IP addresses.
Using Burp Intruder, the last octet of the IP address was fuzzed from 1 to 254 to identify internal hosts.

## 🎯 Result

One of the requests returned a valid response from an internal administrative interface.
This allowed access to the admin panel, where the user "carlos" was deleted to complete the lab.

The objetive of the lab was successfully achieved.


## 📸 Screenshots

### Initial Page
![Initial](images/initial-page.png)

### Product Page
![Product](images/product-page.png)

### Intercepted Request
![Intercept](images/intercept-request.png)

### Intruder Configuration
![Intruder Config](images/intruder-config.png)

### Intruder Results
![Intruder Results](images/intruder-results.png)

### Repeater Response
![Repeater](images/repeater-response.png)

### Lab Solved
![Solved](images/lab-solved.png)
