# 🖥️ Windows Security Logs Monitoring
📌 Overview

Windows Security Logs are one of the most important data sources for detecting malicious activity in enterprise environments. These logs record authentication events, privilege assignments, process creation, and system modifications.

In this SOC Home Lab, Windows Security Logs from the Windows 10 VM are forwarded to Splunk Enterprise running on the Windows 11 host.
🧱 Log Collection Architecture

### Log Source
```
Windows Event Viewer → Security Log
```
### Log Forwarding
```
Splunk Universal Forwarder
```
### Destination
```
Splunk Enterprise (Windows 11 Host)
IP: 192.168.56.1
Port: 9997
```
### Splunk Index

### windows
📂 Log Source Configuration

Windows logs are collected through the Splunk Universal Forwarder configuration.

File location:
```
C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf
```
Configuration used:
```
[WinEventLog://Security]
disabled = 0
index = windows

[WinEventLog://System]
disabled = 0
index = windows

[WinEventLog://Application]
disabled = 0
index = windows
```
After configuration, the forwarder service was restarted to begin log collection.

### 🔍 Important Windows Event IDs

The following security event IDs are monitored in the SOC lab.

| Event ID |	Description                |	Security Use Case | 
|-----------|-----------------------------|--------------------- |
| 4624     | Successful Logon            | User authentication tracking |
| 4625     | Failed Logon                | Brute-force attack detection |
| 4672     | Special Privileges Assigned | Privileged account monitoring |
| 4688     | Process Creation            | Malware / suspicious process detection |
| 4697     | Service Installed           | Persistence detection |

These events help analysts identify suspicious login behavior, privilege escalation attempts, and unauthorized system modifications.

### 🚨 Detection Use Cases
Falid Login Attempt Detection
```
index=windows EventCode=4625
```

![Lab Architecture](../architecture/Example%201.png)
