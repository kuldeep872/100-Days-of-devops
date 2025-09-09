# Day 12 ✅
## 📌 Task: Configure Apache HTTPD on Port 8083
---

### 🎯 Objective
- Install & configure Apache HTTPD on stapp01.
- Change default port to 8083.
- Resolve service startup issues (port conflicts, firewall, SELinux).
- Verify service is running and accessible

---

### 🛠️ Steps & Commands
```bash
1️⃣ SSH into server

ssh tony@stapp01
# Accept host key if prompted


2️⃣ Install Apache HTTPD

sudo yum install -y httpd


3️⃣ Backup & Update Config

sudo cp /etc/httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf.bak
sudo vi /etc/httpd/conf/httpd.conf
# Change: Listen 80 → Listen 8083


4️⃣ Validate Config

sudo apachectl -t
# Output: Syntax OK


5️⃣ Check for Port Conflicts

sudo netstat -tulnp | grep 8083
# If another service is using port 8083, stop it:
sudo systemctl stop sendmail
sudo systemctl disable sendmail


6️⃣ Start & Enable HTTPD

sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl status httpd


7️⃣ Firewall & SELinux Adjustments

# Open port in iptables
sudo iptables -I INPUT -p tcp --dport 8083 -j ACCEPT
sudo iptables-save | sudo tee /etc/sysconfig/iptables

# Allow custom port if SELinux is enforcing
getenforce
sudo semanage port -a -t http_port_t -p tcp 8083 2>/dev/null || \
sudo semanage port -m -t http_port_t -p tcp 8083


8️⃣ Verify Service

# Local test
curl -I http://localhost:8083

# Remote test (from jumphost)
curl http://stapp01:8083

```

## 📘 Notes
- Apache HTTPD installed and running successfully ✅
- Config updated to listen on port 8083 ✅
- Conflict with sendmail resolved ✅
- Firewall/SELinux configured for new port ✅
- Access web server using: http://stapp01:8083/ ✅
## 🛠️ Troubleshooting
- Error: Address already in use: AH00072
    - Cause: Another service is using port 8083.
    - Fix: Identify and stop it →
      ```
       sudo netstat -tulnp | grep 8083
       sudo systemctl stop <service>
       sudo systemctl disable <service>
      ```

- Error: No route to host (from jumphost)
     - Cause: Firewall or SELinux blocking port.
     - Fix:
```
        Open port in firewall (iptables/firewalld).
        Add port to SELinux http context using semanage.
```
- Error: 403 Forbidden
     - Cause: Apache test page shows by default, but no custom content in /var/www/html/.
     - Fix: Place website files in /var/www/html/ or configure DocumentRoot.

- Error: Syntax error in httpd.conf
      - Fix: Run
```
         sudo apachectl -t
```
and correct the misconfigured line.

## 📊 Architecture Diagram
```
              +------------------+
              |   Jumphost       |
              | (curl client)    |
              +------------------+
                        |
                        |  HTTP request (port 8083)
                        v
              +--------------------------+
              | stapp01                  |
              | Apache HTTPD             |
              | Listening on port :8083  |
              +--------------------------+
                        |
                        |  Serves test page / content
                        v
              +--------------------------+
              |   Web Browser / User     |
              +--------------------------+
```



<img width="918" height="419" alt="day12" src="https://github.com/user-attachments/assets/3e756543-3100-43b0-8b47-e339b5ea20f6" />

