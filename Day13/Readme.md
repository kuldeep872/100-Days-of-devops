# Day 13 ✅
## 📌 Task: Configure iptables for Port Security
---

### 🎯 Objective
- Install iptables on all app servers (stapp01, stapp02, stapp03).
- Allow Apache traffic on port 3000 only from LBR host (172.16.238.14).
- Block port 3000 access for all other sources.
- Ensure rules remain persistent after reboot

---

### 🛠️ Steps & Commands
```bash
1️⃣ SSH into App Servers

ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03


2️⃣ Install iptables

sudo yum install -y iptables-services   # CentOS/RHEL
# or
sudo apt-get install -y iptables-persistent   # Ubuntu/Debian


3️⃣ Configure Rules

# Flush existing rules (optional, if safe)
sudo iptables -F

# Allow port 3000 only from LBR host
sudo iptables -A INPUT -p tcp -s 172.16.238.14 --dport 3000 -j ACCEPT

# Block port 3000 for all other sources
sudo iptables -A INPUT -p tcp --dport 3000 -j DROP

# Allow SSH
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Allow established/related connections
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT


4️⃣ Save Rules (Make Persistent)

# CentOS/RHEL
sudo service iptables save
sudo systemctl enable iptables
sudo systemctl start iptables

5️⃣ Verify

sudo iptables -L -n -v
# Port 3000 → ACCEPT only from 172.16.238.14
# Port 3000 → DROP from all other sources

```

## 📘 Notes
- Port 3000 is now protected ✅
- Only LBR host (172.16.238.14) can connect ✅
- Rules survive reboots ✅
- SSH access remains safe ✅


## 📊 Architecture Diagram
```
                +-------------------+
                |    stlb01 (LBR)   |
                | 172.16.238.14     |
                +-------------------+
                          |
         Allowed (port 3000) traffic only
                          |
       ------------------------------------------------
       |                       |                       |
+---------------+     +---------------+       +---------------+
|   stapp01     |     |   stapp02     |       |   stapp03     |
| Apache :3000  |     | Apache :3000  |       | Apache :3000  |
+---------------+     +---------------+       +---------------+
       ^                       ^                       ^
       |                       |                       |
   Other Clients (Blocked on port 3000 by iptables firewall)

```


