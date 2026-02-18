# 🖥️ Splunk Enterprise Setup – Windows 11 Host

---

# ✅ Step 1️⃣ Download Splunk Enterprise

Go to Splunk official website
Download **Windows 64-bit MSI installer**

<img src="Images/splunk-enterprise.jpg" width="900">

* Splunk download page
* Selected Windows 64-bit version

---

# ✅ Step 2️⃣ Run Installer

Double-click the `.msi` file.

You will see the setup wizard.

<img src="Images/splunk-install-wizard.png" width="900">

---

# ✅ Step 3️⃣ Accept License

Check:

```
I accept the license agreement
```

Click Next.

<img src="Images/splunk-license.png" width="900">

* License agreement page

---

# ✅ Step 4️⃣ Set Admin Username & Password

You must create:

```
Username: admin
Password: StrongPassword123!
```

⚠️ Use strong password.

<img src="Images/splunk-admin-setup.png" width="900">

* Admin credential setup page (blur password)

---

# ✅ Step 5️⃣ Install

Click Install.

Wait 2–5 minutes.

<img src="Images/splunk-install-progress.png" width="900">

---

# ✅ Step 6️⃣ Launch Splunk Web

After installation, open browser:

```text
http://localhost:8000
```

Login with:

* Username: admin
* Password: (your password)

<img src="Images/splunk-login-page.png" width="900">

* Splunk login page

Save as:

---

# ✅ Step 7️⃣ Enable Receiving Port (9997)

In Splunk Web:

```
Settings → Forwarding and Receiving → Configure Receiving
```

Click:

```
Add New
```

Set:

```
Port: 9997
```

<img src="Images/splunk-receiving-port.png" width="900">

* Receiving port configuration popup

Save as:

---

# ✅ Step 8️⃣ Verify Installation Using SPL

Go to Search & Reporting app.

Run:

```spl
index=_internal
```

If logs appear → Splunk working ✅

<img src="Images/splunk-admin-setup.png" width="900">

* Search results page





