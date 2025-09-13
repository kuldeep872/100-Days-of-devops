# Day 15 ✅
## 📌 Task: Setup SSL for Nginx

---

### 🎯 Objective
- Install and configure **Nginx** on App Server 2.  
- Deploy a **self-signed SSL certificate** for secure HTTPS access.  
- Configure a simple **index.html** page and verify connectivity.  

---

### 🛠️ Steps & Commands

```bash
1️⃣ Install Nginx
# On App Server 2
sudo yum install -y nginx   # (for RHEL/CentOS)
# or
sudo apt-get install -y nginx   # (for Ubuntu/Debian)

2️⃣ Move SSL Certificate & Key
sudo mkdir -p /etc/nginx/ssl
sudo mv /tmp/nautilus.crt /etc/nginx/ssl/
sudo mv /tmp/nautilus.key /etc/nginx/ssl/
sudo chmod 600 /etc/nginx/ssl/nautilus.*

3️⃣ Configure Nginx SSL
sudo vi /etc/nginx/conf.d/nautilus.conf

# Add:
server {
    listen 443 ssl;
    server_name localhost;

    ssl_certificate     /etc/nginx/ssl/nautilus.crt;
    ssl_certificate_key /etc/nginx/ssl/nautilus.key;

    root /usr/share/nginx/html;
    index index.html;
}

4️⃣ Create index.html
echo "Welcome!" | sudo tee /usr/share/nginx/html/index.html

5️⃣ Restart Nginx
sudo systemctl restart nginx
sudo systemctl enable nginx

6️⃣ Verify SSL Access
curl -Ik https://<app-server-ip>/
```
## 📘 Notes
- SSL certificate & key were provided at /tmp/nautilus.crt and /tmp/nautilus.key.
- Moved them to a secure location /etc/nginx/ssl/.
- Configured nautilus.conf for SSL and enabled HTTPS on port 443.
- Verified with curl → response returned HTTP/1.1 200 OK ✅

## 📊 Setup Flow
```
 Install Nginx
       ↓
Move SSL Certificate & Key
       ↓
 Configure Nginx for SSL
       ↓
 Create index.html
       ↓
 Restart & Enable Nginx
       ↓
 Verify HTTPS Access
```
<img width="908" height="417" alt="day15" src="https://github.com/user-attachments/assets/6186d330-4238-49f3-9b47-8de7fc1c0f4f" />


