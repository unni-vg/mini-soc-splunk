# Splunk Alert Queries – Mini SOC Project

This document contains the final SPL queries used to detect and alert on
security events in the Mini SOC built using Splunk.

---

## SSH Brute Force Attempt

Detects multiple failed SSH login attempts from the same source IP
within a short time window.

Severity: High  
Log Source: /var/log/auth.log  
Alert Type: Scheduled

```spl
index=soc_lab "Failed password"
| rex field=_raw "from (?<src_ip>(\d{1,3}\.){3}\d{1,3}|::1)"
| stats count by src_ip
| where count >= 5
```

## Web Application Attack Detected (Obfuscation Aware)

Detects common web application attacks such as Path Traversal,
Cross-Site Scripting (XSS), and SQL Injection, including encoded
and obfuscated payloads.

Severity: Medium
Log Source: /var/log/apache2/access.log
Alert Type: Scheduled
```spl
index=soc_lab source="/var/log/apache2/access.log"
| eval req=lower(_raw)
| where 
    match(req,"(\.\./|%2e%2e%2f|%252e%252e)") OR
    match(req,"(<script>|%3cscript%3e|%253cscript)") OR
    match(req,"('|%27|%2527)\s*(or|and)\s*('|%27|%2527)") OR
    match(req,"(union(\s|%20)+select)")
| stats count by host
```

