# 🔴 Kali Linux – Attack Simulation Machine

## 📌 Overview

The Kali Linux virtual machine acts as the **attacker system** in the SOC home lab.
It is used to simulate real-world attacks against monitored endpoints (Windows 10 and Linux VM) to validate SIEM detections and alert logic.

The goal is to test whether **Splunk Enterprise** correctly detects malicious activity.

---

## 🧰 VM Specifications

| Component    | Details          |
| ------------ | ---------------- |
| OS           | Kali Linux       |
| RAM          | 2–4 GB           |
| Role         | Attacker Machine |
| Network Mode | NAT / Host-Only  |
| Example IP   | 192.168.56.103   |

---

## 🎯 Attack Objectives

The attacker VM was used to simulate:

* SSH brute-force attacks (Linux VM)
* RDP / Login brute-force attempts (Windows 10 VM)
* Network reconnaissance
* Suspicious command execution
* Privilege abuse scenarios

---

# 🛠️ Tools Used

| Tool       | Purpose                       |
| ---------- | ----------------------------- |
| Hydra      | Brute-force attack simulation |
| Nmap       | Network scanning              |
| Netcat     | Network testing               |
| SSH client | Login testing                 |

---

# 🚨 Attack Scenarios Performed

---

## 1️⃣ SSH Brute Force Attack (Linux VM)

### Command Used

```bash
hydra -l testuser -P rockyou.txt ssh://192.168.56.102
```

### Target

Linux VM → `192.168.56.102`

### Logs Generated

* Multiple failed SSH login attempts
* Entries in `/var/log/auth.log`

### Detection in Splunk

```spl
index=linux "Failed password"
| stats count by src_ip
| where count > 5
```

### MITRE ATT&CK Mapping

* T1110 – Brute Force

---

## 2️⃣ Windows Login Brute Force Simulation

Manual multiple failed login attempts were generated against:

Windows 10 VM → `192.168.56.101`

### Event IDs Generated

| Event ID | Description      |
| -------- | ---------------- |
| 4625     | Failed login     |
| 4624     | Successful login |

### Detection Query

```spl
index=windows EventCode=4625
| stats count by Source_Network_Address, Account_Name
| where count > 5
```

---

## 3️⃣ Network Reconnaissance

### Nmap Scan

```bash
nmap -sV 192.168.56.0/24
```

### Purpose

* Identify open services
* Identify exposed ports
* Validate detection of unusual network activity

### Detection Concept

Monitor for:

* Multiple connection attempts
* Unusual source IP behavior

MITRE Mapping:

* T1046 – Network Service Discovery

---

## 4️⃣ Suspicious Command Testing

Tested command-line activities to generate logs:

On Windows:

* PowerShell execution
* Encoded commands

On Linux:

* sudo privilege escalation attempts

Detection Focus:

* Event ID 4688 (Windows)
* sudo logs (Linux)

---

# 🔄 Attack Validation Workflow

1. Launch attack from Kali.
2. Target Windows or Linux VM.
3. Generate security logs.
4. Logs forwarded to Splunk.
5. SPL queries analyze behavior.
6. Alert triggered.
7. Incident documented.

This validates **end-to-end SOC detection workflow**.

---

# 📊 Role in SOC Architecture

The Kali machine represents:

* External attacker
* Insider threat simulation
* Threat validation tool
* Red-team style activity

It ensures detections are:

* Accurate
* Triggering correctly
* Not producing false positives

---

# 🔐 Lab Safety Considerations

* Attacks performed only within isolated lab network.
* No internet exposure.
* No real production systems involved.
* No unauthorized activity performed.

---

# ✅ Outcome

✔ Successfully simulated real-world attacks
✔ Generated meaningful security logs
✔ Validated SIEM detection rules
✔ Mapped attacks to MITRE ATT&CK
✔ Demonstrated blue-team detection capability

---

# 📎 Related Files

* `host-setup.md`
* `windows10-vm.md`
* `linux-vm.md`
* `detections/`
* `alerts/`
* `incidents/`

---
