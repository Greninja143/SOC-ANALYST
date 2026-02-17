

# 🖥️ Host Setup – Windows 11 (Splunk SIEM Server)

## 📌 Overview

The Windows 11 host machine serves as the **central SIEM server** in this SOC home lab.
It runs **Splunk Enterprise** and collects logs from multiple virtual machines for analysis, alerting, and monitoring.

---

## 🧰 Host Specifications

| Component    | Details           |
| ------------ | ----------------- |
| OS           | Windows 11        |
| RAM          | 8 GB+ Recommended |
| Storage      | 50 GB+ Free Space |
| Role         | SIEM Server       |
| Network Mode | NAT / Host-Only   |

---

## 🔧 Software Installed

### 1️⃣ Splunk Enterprise (Free Trial)

* Version: Latest stable version
* Web Interface:

```
http://localhost:8000
```

* Default Management Port:

```
8089
```

* Log Receiving Port:

```
9997
```

---

## 🔌 Splunk Configuration

### Step 1: Enable Receiving Port

Navigate to:

```
Settings → Forwarding and Receiving → Configure Receiving → Add New
```

Add:

```
Port: 9997
```

This allows endpoints (Windows 10 & Linux VM) to forward logs.

---

### Step 2: Create Index

Created a dedicated index for lab logs:

```
Index Name: windows
```

Purpose:

* Separate lab logs from default index
* Better log organization
* Cleaner detection queries

---

### Step 3: Configure Data Inputs

Enabled:

* Windows Security Logs
* System Logs
* Application Logs

Verification Query:

```spl
index=windows
```

---

## 🌐 Network Configuration

| Machine         | IP Address     |
| --------------- | -------------- |
| Windows 11 Host | 192.168.56.1   |
| Windows 10 VM   | 192.168.56.101 |
| Linux VM        | 192.168.56.102 |
| Kali Linux      | 192.168.56.103 |

All systems are connected via a **Virtual Lab Network (NAT / Host-Only)**.

---

## 🔄 Data Flow

1. Windows 10 and Linux VMs generate security logs.
2. Logs are forwarded to Splunk on port 9997.
3. Splunk indexes logs in the `windows` index.
4. SPL queries analyze logs for suspicious behavior.
5. Alerts are generated based on detection rules.

---

## 🔐 Security Considerations

* Strong admin password configured
* Windows Firewall configured to allow Splunk ports
* Only internal lab network allowed to send logs
* No external exposure to public internet

---

## 📊 Role in SOC Workflow

The Windows 11 host acts as:

* Central log aggregator
* Detection engine
* Alert generation platform
* Dashboard visualization system
* Incident documentation reference

---

## ✅ Outcome

✔ Successfully deployed Splunk Enterprise
✔ Enabled log receiving on port 9997
✔ Created dedicated index for lab monitoring
✔ Configured data ingestion
✔ Prepared environment for attack simulation

---

# 📎 Related Files

* `windows10-vm.md`
* `linux-vm.md`
* `kali-attacker.md`
* `detections/`
* `alerts/`
* `dashboards/`

---
