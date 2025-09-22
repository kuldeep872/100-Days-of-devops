# Day 18 ✅
## 📌 Task: Configure LAMP Server

---

### 🎯 Objective
- Install and configure Apache (httpd), PHP, and their dependencies on all App Servers (stapp01, stapp02, stapp03).
- Configure Apache to listen on port 5003.
- Install and configure MariaDB on DB Server (stdb01).
- Create a database and user with proper privileges.
- Configure WordPress to connect to the database.
- Verify connectivity and access WordPress via the Load Balancer (LBR)

  ---

### 🛠️ Steps & Commands

```bash
1️⃣ SSH into App Server
ssh tony@stapp01   # (do the same on stapp02 & stapp03)

2️⃣ Install Apache, PHP and dependencies
sudo -i
yum install -y httpd php php-mysqlnd php-gd php-xml php-mbstring

3️⃣ Configure Apache to listen on port 5003
cp /etc/httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf.bak
sed -i 's/^Listen 80/Listen 5003/' /etc/httpd/conf/httpd.conf
sed -i 's/<VirtualHost \*:80>/<VirtualHost *:5003>/g' /etc/httpd/conf.d/*.conf 2>/dev/null || true

4️⃣ Enable & Restart Apache
systemctl enable httpd
systemctl restart httpd
ss -tuln | grep 5003    # verify listening port

------------------------------------------

5️⃣ SSH into DB Server
ssh peter@stdb01

6️⃣ Install & Configure MariaDB (already installed in lab)
systemctl enable mariadb
systemctl start mariadb

7️⃣ Update bind-address
echo -e "[mysqld]\nbind-address=0.0.0.0" > /etc/my.cnf.d/server.cnf
systemctl restart mariadb

8️⃣ Create Database & User
mysql -u root -p
CREATE DATABASE kodekloud_db10;
CREATE USER 'kodekloud_tim'@'%' IDENTIFIED BY 'YchZHRcLkL';
GRANT ALL PRIVILEGES ON kodekloud_db10.* TO 'kodekloud_tim'@'%';
FLUSH PRIVILEGES;
exit;

------------------------------------------

9️⃣ Configure WordPress (only once, since /var/www/html is shared)
cd /var/www/html
cp wp-config-sample.php wp-config.php
vi wp-config.php

# Update these values:
define('DB_NAME', 'kodekloud_db10');
define('DB_USER', 'kodekloud_tim');
define('DB_PASSWORD', 'YchZHRcLkL');
define('DB_HOST', 'stdb01');

------------------------------------------

🔟 Verify
# On LBR link provided in the lab
App should be able to connect to DB successfully
```

## 📘 Notes
- Apache and PHP installed on all app servers.
- Apache configured to run on port 5003.
- MariaDB configured on DB server with external access (bind-address=0.0.0.0).
- Database kodekloud_db10 and user kodekloud_tim created with full privileges.
- WordPress configured once since /var/www/html is a shared directory across app servers.
- Verified application access via LBR

## 📊 Setup Flow
```
 Install Apache + PHP on App Servers
        ↓
 Configure Apache on port 5003
        ↓
   Setup MariaDB on DB Server
        ↓
 Create DB + User + Grant Privileges
        ↓
 Configure WordPress (shared dir)
        ↓
   Verify via LBR (App → DB OK)
```
<img width="918" height="388" alt="Day18" src="https://github.com/user-attachments/assets/8bcb3706-a2b1-4289-a4f7-0468fdbb092c" />

