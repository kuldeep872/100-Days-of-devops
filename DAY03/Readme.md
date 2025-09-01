# Day 03 - Create User Without Home Directory 🏠❌

## 📌 Task
- Create a new Linux user.  
- Do **not** create a home directory for this user.  
- Verify that no home directory exists.  

---

## 🛠️ Commands Used

```bash
# Create user without home directory
sudo useradd -M devuser3

# Set password (optional)
sudo passwd devuser3

# Verify user entry in /etc/passwd
grep devuser3 /etc/passwd

# Check if home directory exists
ls -ld /home/devuser3
```

## 📝 Notes
- useradd -M → create user without home directory.
- Default behavior of useradd is to create /home/username (unless disabled in /etc/login.defs).
- grep username /etc/passwd → check user details.
- ls -ld /home/username → confirm home directory existenc

- ## ✅ Outcomes
- User devuser3 is created successfully.
- /etc/passwd shows user entry.
- No /home/devuser3 directory is created


