# 💻 Windows 10 VM – Monitored Endpoint

## 📌 Overview

The Windows 10 virtual machine acts as a **monitored endpoint (victim system)** in the SOC home lab.
It generates Windows Security Events that are forwarded to the SIEM for detection and analysis.

Logs from this system are collected by **Splunk Enterprise** running on the Windows 11 host.

---

## 🧰 VM Specifications

| Component    | Details            |
| ------------ | ------------------ |
| OS           | Windows 10         |
| RAM          | 4 GB               |
| Role         | Monitored Endpoint |
| Network Mode | NAT / Host-Only    |
| Example IP   | 192.168.56.101     |

---

## 🔧 Software Installed

### 1️⃣ Splunk Universal Forwarder

Purpose:

* Forward Windows logs to Splunk SIEM (Windows 11 Host)

Configuration:

```text
Receiving Indexer: 192.168.56.1:9997
```

---

## 📂 Log Sources Enabled

The following Windows Event Logs are monitored:

| Log Type    | Purpose                           |
| ----------- | --------------------------------- |
| Security    | Authentication & privilege events |
| System      | System changes                    |
| Application | Application logs                  |

---

## 🔎 Important Event IDs Monitored

| Event ID | Description                 |
| -------- | --------------------------- |
| 4624     | Successful login            |
| 4625     | Failed login                |
| 4672     | Special privileges assigned |
| 4688     | Process creation            |
| 4697     | Service installed           |

These logs are critical for detecting:

* Brute-force attacks
* Privilege escalation
* Suspicious process execution
* Persistence mechanisms

---

## 🚨 Attack Simulations Performed

This VM was targeted by Kali Linux to simulate real-world attacks.

### 🔴 1️⃣ Brute Force Login Attempts

* Multiple failed login attempts generated
* Event ID: 4625
* Detection in Splunk using threshold-based logic

### 🔴 2️⃣ Suspicious PowerShell Execution

* Encoded PowerShell commands tested
* Event ID: 4688
* Detected using command-line filtering

### 🔴 3️⃣ Privileged Account Monitoring

* Admin login activity monitored
* Event ID: 4672

---

## 🔄 Log Forwarding Flow

1. Windows 10 generates security events.
2. Splunk Universal Forwarder collects logs.
3. Logs are sent to:

```text
192.168.56.1:9997
```

4. Logs are indexed in:

```text
index=windows
```

5. SPL queries analyze events.
6. Alerts trigger if suspicious behavior is detected.

---

## 🔍 Verification Query (Splunk)

```spl
index=windows host="Windows10"
```

Example brute-force detection query:

```spl
index=windows EventCode=4625
| stats count by Source_Network_Address, Account_Name
| where count > 5
```

---

## 📊 Role in SOC Workflow

The Windows 10 VM represents:

* A typical enterprise workstation
* A log-generating endpoint
* A target for authentication-based attacks
* A source of forensic evidence during investigations

---

## ✅ Outcome

✔ Successfully configured Windows 10 as monitored endpoint
✔ Enabled log forwarding via Splunk Universal Forwarder
✔ Simulated attack scenarios
✔ Detected suspicious activity in SIEM
✔ Validated alert logic

---

## 📎 Related Files

* `host-setup.md`
* `linux-vm.md`
* `kali-attacker.md`
* `detections/`
* `alerts/`

---
