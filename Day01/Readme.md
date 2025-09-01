# Day 01 - Linux User Setup with Non-Interactive Shell 🐧

## 📌 Task
- Create a new Linux user.
- Assign the user a **non-interactive shell** (like `/sbin/nologin`).
- Ensure the user cannot log in but can still own files or run processes.

## 🛠️ Commands Used
```bash
# Create user with non-interactive shell
sudo useradd -s /sbin/nologin devuser

# Verify user shell
grep devuser /etc/passwd
```
--------

## 📝 Notes
- `/sbin/nologin` is used for system/service accounts that don’t need shell access.  
- The user cannot log in but can still own files, run services, or processes.  
- This is a security best practice for service users.  

## ✅ Outcomes
- User `devuser` was successfully created.  
- Shell verified as `/sbin/nologin`.  
- When trying `su - devuser`, login is denied.
