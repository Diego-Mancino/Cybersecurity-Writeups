# 🔐 2FA Bypass - PortSwigger Lab


## 🎯 Objective

The goal of this lab is to bypass the two-factor authentication (2FA) mechanism and gain unauthorized access to another user's account.


## 🧠 What is 2FA Bypass?

Two-Factor Authentication (2FA) is a security mechanism that requires a second form of verification after entering valid credentials.

A 2FA bypass occurs when an attacker is able to access an account without completing the second authentication step, often due to improper implementation or missing authorization checks.


## 🔍 Recon

The application provides a login functionality followed by a 2FA verification step.

After loggin in with valid credentials, a 4-digit code is required, which is sent to the user's email through an internal email client.
