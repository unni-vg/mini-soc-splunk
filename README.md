# Mini SOC using Splunk

This project demonstrates a **Mini Security Operations Center (SOC)** built using **Splunk Enterprise** to detect, alert, and monitor common cyber attacks.

## 🔹 What this project does
- Detects **SSH brute-force attacks** from Linux authentication logs
- Detects **web application attacks** (SQL Injection, XSS, Path Traversal)
- Uses **obfuscation-aware detection logic**
- Triggers **scheduled alerts**
- Visualizes alerts in a **SOC-style dashboard**

## 🔹 Log Sources
- `/var/log/auth.log` – SSH authentication events
- `/var/log/apache2/access.log` – Web server access logs

## 🔹 Alerts Implemented
- **SSH Brute Force Attempt** (High severity)
- **Web Application Attack Detected (Obfuscation Aware)** (Medium severity)

## 🔹 Dashboard
The dashboard shows:
- Active security alerts
- Alerts by attack type
- Top attacker IP addresses

## 🔹 Tools Used
- Splunk Enterprise
- Ubuntu Linux
- Apache Web Server

## 🔹 Purpose
This project is built for **learning and demonstrating SOC / SIEM skills** for entry-level cybersecurity roles.
