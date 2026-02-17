# 🐧 Linux VM – Monitored Server Endpoint

## 📌 Overview

The Linux virtual machine acts as a **monitored server endpoint** within the SOC home lab.
It generates authentication and system logs that are forwarded to the SIEM for detection and analysis.

Logs from this system are collected and analyzed by **Splunk Enterprise** running on the Windows 11 host.

---

## 🧰 VM Specifications

| Component    | Details                 |
| ------------ | ----------------------- |
| OS           | Ubuntu / Debian (Linux) |
| RAM          | 2–4 GB                  |
| Role         | Monitored Server        |
| Network Mode | NAT / Host-Only         |
| Example IP   | 192.168.56.102          |

---

## 🔧 Log Collection Configuration

### 1️⃣ Log Sources Monitored

Primary log files:

```text
/var/log/auth.log
/var/log/syslog
```

Purpose:

* SSH login attempts
* Failed authentication events
* Privilege escalation activity
* System service activity

---

### 2️⃣ Log Forwarding Method

Logs are forwarded to Splunk using:

* Splunk Universal Forwarder
  **OR**
* Syslog forwarding (if configured)

Example Forwarder Target:

```text
192.168.56.1:9997
```

---

## 🔎 Key Log Events Monitored

| Log Type             | Detection Purpose            |
| -------------------- | ---------------------------- |
| SSH Failed Login     | Brute-force detection        |
| SSH Successful Login | Account compromise detection |
| sudo usage           | Privilege escalation         |
| New service/process  | Persistence detection        |

---

## 🚨 Attack Simulations Performed

The Linux VM was targeted from Kali Linux to simulate common server-side attacks.

---

### 🔴 1️⃣ SSH Brute Force Attack

Tool used from Kali:

* Hydra (for SSH brute-force simulation)

Generated logs example:

```text
Failed password for invalid user test from 192.168.56.103
```

Detection goal:

* Multiple failed SSH attempts from same IP

---

### 🔴 2️⃣ Successful SSH Login After Failures

Pattern observed:

* Multiple failed logins
* Followed by successful authentication

SOC Insight:

> Indicates possible credential compromise.

---

### 🔴 3️⃣ Privilege Escalation Monitoring

Command tested:

```bash
sudo su
```

Log monitored:

```text
sudo: user : TTY=pts/0 ; COMMAND=/bin/su
```

Detection focus:

* Unusual sudo activity
* Privileged account misuse

---

## 🔄 Log Flow Process

1. Linux system generates authentication logs.
2. Logs written to `/var/log/auth.log`.
3. Forwarder sends logs to Splunk SIEM.
4. Logs indexed in:

```spl
index=linux
```

(or shared index depending on configuration)
5. SPL queries analyze suspicious patterns.
6. Alerts trigger based on defined thresholds.

---

## 🔍 Verification Query (Splunk)

Basic search:

```spl
index=linux host="Linux-VM"
```

SSH brute-force detection example:

```spl
index=linux "Failed password"
| stats count by src_ip
| where count > 5
```

---

## 📊 Role in SOC Workflow

The Linux VM represents:

* A typical enterprise Linux server
* A remote-access exposed system (SSH)
* A high-value authentication log source
* A forensic artifact source during incident response

---

## 🔐 Security Monitoring Focus

* Authentication monitoring
* Remote access abuse detection
* Privilege escalation attempts
* Persistent service creation

---

## ✅ Outcome

✔ Configured Linux VM as monitored server
✔ Enabled log forwarding to Splunk
✔ Simulated SSH brute-force attacks
✔ Detected suspicious login behavior
✔ Validated SIEM alerting mechanism

---

## 📎 Related Files

* `host-setup.md`
* `windows10-vm.md`
* `kali-attacker.md`
* `detections/`
* `alerts/`
* `incidents/`

---

