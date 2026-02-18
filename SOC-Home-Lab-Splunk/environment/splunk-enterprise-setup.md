# 🖥️ Splunk Enterprise Setup – Windows 11 Host

---

# ✅ Step 1️⃣ Download Splunk Enterprise

Go to Splunk official website
Download **Windows 64-bit MSI installer**

📸 **Screenshot to capture:**

* Splunk download page
* Selected Windows 64-bit version

Save as:

```
splunk-download-page.png
```

---

# ✅ Step 2️⃣ Run Installer

Double-click the `.msi` file.

You will see the setup wizard.

📸 Screenshot:

* First installation screen

Save as:

```
splunk-install-wizard.png
```

---

# ✅ Step 3️⃣ Accept License

Check:

```
I accept the license agreement
```

Click Next.

📸 Screenshot:

* License agreement page

Save as:

```
splunk-license.png
```

---

# ✅ Step 4️⃣ Set Admin Username & Password

You must create:

```
Username: admin
Password: StrongPassword123!
```

⚠️ Use strong password.

📸 Screenshot:

* Admin credential setup page (blur password)

Save as:

```
splunk-admin-setup.png
```

---

# ✅ Step 5️⃣ Install

Click Install.

Wait 2–5 minutes.

📸 Screenshot:

* Installation progress bar

Save as:

```
splunk-install-progress.png
```

---

# ✅ Step 6️⃣ Launch Splunk Web

After installation, open browser:

```text
http://localhost:8000
```

Login with:

* Username: admin
* Password: (your password)

📸 Screenshot:

* Splunk login page

Save as:

```
splunk-login-page.png
```

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

📸 Screenshot:

* Receiving port configuration popup

Save as:

```
splunk-receiving-port.png
```

---

# ✅ Step 8️⃣ Verify Installation Using SPL

Go to Search & Reporting app.

Run:

```spl
index=_internal
```

If logs appear → Splunk working ✅

📸 Screenshot:

* Search results page





