# SOC Dashboard Panels – Mini SOC Project

This document describes the dashboard panels used in the Mini SOC
Security Monitoring Dashboard built using Splunk.

---

## Active Security Alerts

Displays the total number of security alerts triggered within the
selected time range.

```spl
index=_internal source=*scheduler.log*
| search savedsearch_name IN (
    "SSH Brute Force Attempt",
    "Web Application Attack Detected (Obfuscation Aware)"
)
| stats count
```
## Alerts by Attack Type

Visualizes the number of alerts grouped by attack category to help
prioritize incident response.

```spl
index=_internal source=*scheduler.log*
| search savedsearch_name IN (
    "SSH Brute Force Attempt",
    "Web Application Attack Detected (Obfuscation Aware)"
)
| stats count by savedsearch_name
```
## Top Attacker IP Addresses

Displays the most frequent source IPs involved in detected attacks.

```spl
index=soc_lab
| stats count by src_ip
| sort -count
| head 10
```
