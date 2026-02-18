# Setting Up Splunk & Universal Forwarder on Windows 10 & Linux

# Splunk Universal Forwarder Setup on Windows 10
#### Step 1: Downloading the Universal Forwarder
The Splunk Universal Forwarder can be downloaded from the official Splunk download page.
<img src="Images/uniforwared_d.jpg" width="900">
<img src="Images/uniforwared_d2.jpg" width="900">
https://www.splunk.com/en_us/download.html

This software will send the log data from a system to your Splunk instance.

#### Step 2: Installing the Universal Forwarder
Run the Installer file.
<img src="Images/Run Installer.png" width="900">

#### Step 3: Configure the Forwader
  1. License Agreement: Accept the license agreement.
  <img src="Images/Licence.png" width="900">
  
  2. Create Login Credintials.
  <img src="Images/credentials.png" width="900">
  
  3. Deployment Server: You can set a the deployment Server if you have one. Or can skip like me.
  <img src="Images/development_server.png" width="900">
  
  4. Listener Configuration: Specify the IP address of Splunk Enterprise instance (on Window 11 host). Also ensure that listener is set on port 9997.
  <img src="Images/listner.png" width="900">
  
#### Click Install to begin installation.
<img src="Images/install.png" width="900">

#### After Installation finish the process.
<img src="Images/Finish.png" width="900">

### ✅ Windows Logs Configuration 
Methods to enable log collection:

### 🟢 Configure inputs.conf
#### Step 1: Go to this folder
```
C:\Program Files\SplunkUniversalForwarder\etc\system\local\
```
If inputs.conf does not exist → create it.

#### Step 2: Add This Configuration
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
Step 3: Restart Forwarder

Open PowerShell as Admin:
```
Restart-Service SplunkForwarder
```
Step 4: Verify in Splunk
```
index=windows host="Windows10"
```
If logs appear → working ✅



---

# 🐧 Splunk Universal Forwarder Setup on Linux

## ✅ Step 1️⃣ Download Universal Forwarder

Go to Splunk official site and download Linux `.tgz` version
for your architecture (usually x86_64).

Or via CLI:

```
wget https://download.splunk.com/products/universalforwarder/releases/<VERSION>/linux/splunkforwarder-<VERSION>-Linux-x86_64.tgz
```

Replace `<VERSION>` with latest version.

---

# ✅ Step 2️⃣ Extract & Move to /opt

```
tar -xvzf splunkforwarder-*.tgz
sudo mv splunkforwarder /opt/
```

---

# ✅ Step 3️⃣ Start Splunk Forwarder

```
cd /opt/splunkforwarder/bin
sudo ./splunk start --accept-license
```

Create admin credentials when prompted.

---

# ✅ Step 4️⃣ Configure Forward Server (Very Important)

Add your Splunk server:

```
sudo ./splunk add forward-server 192.168.56.1:9997
```

Verify:

```
sudo ./splunk list forward-server
```

You should see:

```
Active forwards:
192.168.56.1:9997
```

---

# ✅ Step 5️⃣ Configure Log Inputs

Edit:

```bash
sudo nano /opt/splunkforwarder/etc/system/local/inputs.conf
```

Add this:

```ini
[monitor:///var/log/auth.log]
disabled = 0
index = linux

[monitor:///var/log/syslog]
disabled = 0
index = linux
```

---

# ✅ Step 6️⃣ Restart Forwarder

```
sudo ./splunk restart
```

---

# ✅ Step 7️⃣ Enable Auto-Start on Boot (Important)

```
sudo ./splunk enable boot-start
```

This ensures forwarder starts automatically.

---

# ✅ Step 8️⃣ Verify in Splunk (Windows 11 Host)

Go to Splunk Web and search:

```
index=linux
```

Or filter by host:

```
index=linux host="linux-server"
```

If logs appear → Success ✅

---

# 🔎 Troubleshooting

If logs not appearing:

### 1️⃣ Check Forward Server

```
sudo ./splunk list forward-server
```

### 2️⃣ Check Forwarder Status

```
sudo ./splunk status
```

### 3️⃣ Check Logs

```
sudo tail -f /opt/splunkforwarder/var/log/splunk/splunkd.log
```

---

# 🔥 SOC-Level Enhancement

Instead of using system folder, create a dedicated app:

```
sudo mkdir -p /opt/splunkforwarder/etc/apps/linux_monitor/local
sudo nano /opt/splunkforwarder/etc/apps/linux_monitor/local/inputs.conf
```

This is how enterprise environments do it.

---


