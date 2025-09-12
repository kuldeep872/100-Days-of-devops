# Day 14 ✅
## 📌 Task: Linux Process Troubleshooting
---

### 🎯 Objective
- Troubleshoot and fix faulty processes on app servers.
- Resolve service startup issues caused by **port conflicts**.
- Ensure Apache (httpd) is running on the required port. 

---

### 🛠️ Steps & Commands
```bash
1️⃣ Check Service Status

sudo systemctl status httpd

🔴 On stapp01, Apache failed with the error:

(98)Address already in use: AH00072: make_sock: could not bind to address [::]:8084
no listening sockets available, shutting down
httpd.service: Failed with result 'exit-code'.

2️⃣ Verify Port Usage

sudo ss -tulnp | grep 8084
📌 Found that Sendmail was already using port 8084:

tcp LISTEN 0 10 127.0.0.1:8084 users:(("sendmail",pid=669,fd=4))

3️⃣ Kill / Stop Conflicting Process

# Stop and disable sendmail
sudo systemctl stop sendmail
sudo systemctl disable sendmail

4️⃣ Restart Apache

sudo systemctl start httpd
sudo systemctl enable httpd
5️⃣ Verify Service

sudo systemctl status httpd
sudo ss -tulnp | grep 8084
✅ Now Apache is running and listening on port 8084.

tcp LISTEN 0 511 *:8084 users:(("httpd",pid=996,fd=3), ...)

```

## 📘 Notes
- Root cause: Port conflict (Sendmail was occupying port 8084).
- Fix: Stopped Sendmail → restarted Apache → verified port binding.
- Applied the same troubleshooting steps on stapp02 and stapp03 → all servers healthy


## 📊 Troubleshooting Flow
```
   Check Service Status (systemctl)
              ↓
     Error: Port Already in Use
              ↓
   Identify Conflicting Process (ss/lsof)
              ↓
      Stop / Disable Conflicting Service
              ↓
        Restart Required Service
              ↓
        Verify Service & Port Binding

```
<img width="896" height="425" alt="day14" src="https://github.com/user-attachments/assets/fcd2819b-6de9-4591-b6d8-16a6bdb54eab" />


