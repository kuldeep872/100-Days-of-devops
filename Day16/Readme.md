# Day 16 ✅
## 📌 Task: Install and Configure Nginx as a Load Balancer (LBR)

---

### 🎯 Objective
- Install and configure Nginx on the Load Balancer server (stlb01).
- Configure HTTP load balancing for all 3 App Servers (stapp01, stapp02, stapp03).
- Ensure traffic is distributed across backend app servers running Apache on port 8089.
- Verify successful load balancing via curl and StaticApp

---

### 🛠️ Steps & Commands

```bash
1️⃣ Install Nginx
# On stlb01 (LBR server)
sudo yum install -y nginx   # (for RHEL/CentOS)
# or
sudo apt-get install -y nginx   # (for Ubuntu/Debian)

2️⃣ Configure Load Balancing
sudo vi /etc/nginx/nginx.conf

# Add/Update inside http block:
http {
    upstream backend {
        server stapp01.stratos.xfusioncorp.com:8089;
        server stapp02.stratos.xfusioncorp.com:8089;
        server stapp03.stratos.xfusioncorp.com:8089;
    }

    server {
        listen 80;
        location / {
            proxy_pass http://backend;
        }
    }
}

3️⃣ Verify Nginx Config
sudo nginx -t

4️⃣ Restart & Enable Nginx
sudo systemctl restart nginx
sudo systemctl enable nginx

5️⃣ Verify Load Balancer
# From LBR server
curl http://172.16.238.14
# Response: "Welcome to xFusionCorp Industries!"

# Refresh multiple times → responses served from different App Servers

```
## 📘 Notes
- Apache on all App Servers was confirmed to be running on port 8089.
- Configured upstream block with all App Servers for round-robin load balancing.
- Verified syntax with nginx -t before restarting.
- Accessed site via StaticApp button → Application served successfully ✅.

## 📊 Setup Flow
```
 Install Nginx on LBR
        ↓
 Configure Upstream with App Servers
        ↓
   Add Nginx Server Block
        ↓
 Verify Config & Restart Service
        ↓
 Access via StaticApp / curl

```
<img width="1888" height="827" alt="image" src="https://github.com/user-attachments/assets/0c684eb0-b76b-44c1-a557-a701ce1fa91b" />



