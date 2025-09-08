# Day 11 ✅
## 📌 Task: Deploy Web Application on Tomcat Server

---

### 🎯 Objective
- Install & configure **Apache Tomcat** on `stapp01`.
- Deploy `ROOT.war` web application.
- Verify deployment locally.

---

### 🛠️ Steps & Commands

1️⃣ **SSH into server**
```bash
ssh tony@stapp01
# Accept host key if prompted

2️⃣ Install Tomcat
sudo yum install -y tomcat tomcat-webapps tomcat-admin-webapps

3️⃣ Start & Enable Tomcat
sudo systemctl enable tomcat
sudo systemctl start tomcat
sudo systemctl status tomcat

4️⃣ Verify Tomcat
curl http://localhost:3003
# Should show Tomcat homepage

5️⃣ Deploy WAR file
scp /tmp/ROOT.war tony@stapp01:/tmp/
sudo mv /tmp/ROOT.war /usr/share/tomcat/webapps/

6️⃣ Check Deployment
ls -l /usr/share/tomcat/webapps/
curl http://localhost:3003/
# Sample app page should appear

7️⃣ Check logs if issues
sudo tail -f /var/log/tomcat/catalina.out
```

## 📘 Notes
- Tomcat installed and running successfully ✅
- ROOT.war deployed successfully ✅
- Access app using http://localhost:3003/
- Permissions require sudo to move .war files
- Logs help troubleshoot deployment issues

