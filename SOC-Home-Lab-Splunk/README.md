🛡️ SOC Home Lab – Splunk SIEM
📌 Project Overview

This project documents a SOC home lab environment designed to simulate real-world enterprise monitoring and attack detection. Splunk SIEM runs on a Windows 11 host and collects logs from multiple endpoints, while attacks are launched from Kali Linux to validate detections and alerts.

🧪 Lab Architecture

Host: Windows 11 (Splunk SIEM)

Victim 1: Windows 10 VM

Victim 2: Linux VM

Attacker: Kali Linux

SIEM: Splunk
Virtualization: VMware / VirtualBox

🔄 Data Flow

Endpoints generate security events

Logs forwarded to Splunk

SPL queries analyze activity

Alerts trigger on malicious behavior

Incidents documented

🔍 Attacks Simulated

Brute-force login attacks (Windows & Linux)

Suspicious PowerShell execution

Privilege escalation activity

Persistence via service creation

🚨 Detections Implemented

Failed login threshold detection

PowerShell abuse detection

Privileged logon monitoring

Service installation alerts

📊 Dashboards

Authentication activity overview

Suspicious process execution

Privileged account activity

🧾 Incident Response

Each detection includes:

Alert description

IOC details

Timeline

MITRE ATT&CK mapping

Recommended remediation
