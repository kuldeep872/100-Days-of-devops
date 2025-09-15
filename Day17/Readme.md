# Day 17 ✅
## 📌 Task: Install and Configure PostgreSQL

---

### 🎯 Objective
- Install and configure PostgreSQL on the Nautilus DB Server (stdb01).
- Create a database user kodekloud_joy with password YchZHRcLkL.
- Create a database kodekloud_db9.
- Grant full permissions of kodekloud_db9 to kodekloud_joy.
- Verify connectivity with the new use

---

### 🛠️ Steps & Commands

```bash
1️⃣ SSH into Nautilus DB Server
ssh peter@stdb01
# password: Sp!dy

2️⃣ Switch to postgres user
sudo su - postgres
psql

3️⃣ Create User
CREATE USER kodekloud_joy WITH PASSWORD 'YchZHRcLkL';

4️⃣ Create Database
CREATE DATABASE kodekloud_db9;

5️⃣ Grant Permissions
GRANT ALL PRIVILEGES ON DATABASE kodekloud_db9 TO kodekloud_joy;

6️⃣ Exit
\q
exit

7️⃣ Verify Connection
psql -U kodekloud_joy -d kodekloud_db9 -h localhost
# Enter password: YchZHRcLkL


```
## 📘 Notes
- PostgreSQL was already installed on stdb01.
- Created a dedicated user and database as per Nautilus requirements.
- Granted full permissions so that the application can connect with no issues.
- Verified login with psql to ensure configuration was successful..

## 📊 Setup Flow
```
 Install PostgreSQL (already installed)
        ↓
 Create DB User & Set Password
        ↓
   Create Application Database
        ↓
 Grant Privileges to User
        ↓
 Verify Access with psql

```
<img width="1821" height="837" alt="image" src="https://github.com/user-attachments/assets/b9ed7de8-fb8f-4fb0-ace2-0ed7ffad232f" />



