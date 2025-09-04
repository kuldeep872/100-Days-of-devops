
# Day 07 - Create User with Specific Shell 🐚👤

## 📌 Task
- Create a new Linux user.
- Assign a specific login shell instead of the default /bin/bash.
- Verify the shell assignment.  

---

## 🛠️ Commands Used

```bash
# Create user with /sbin/nologin shell
sudo useradd -s /sbin/nologin devuser7

# OR create user with /bin/sh shell
sudo useradd -s /bin/sh devuser7

# Set password (optional)
sudo passwd devuser7

# Verify user details in /etc/passwd
grep devuser7 /etc/passwd

```

## 📝 Notes
- useradd -s /path/to/shell username → sets a custom shell.
- Common shells:
   - /bin/bash → default interactive shell.
   - /bin/sh → lightweight POSIX shell.
   - /sbin/nologin → prevents login (useful for service accounts).
- /etc/shells → lists all valid shells.
- grep username /etc/passwd → confirms shell assigned

- ## ✅ Outcomes
- User devuser7 is created successfully.
- /etc/passwd entry shows the assigned shell.
- User behavior depends on the shell:
   - If /bin/bash, user gets normal shell access.
   - If /sbin/nologin, login is denied with a message
  <img width="1232" height="569" alt="day7a" src="https://github.com/user-attachments/assets/c5c99b48-4d9e-4359-a642-043075ebde45" />
<img width="1310" height="611" alt="day7" src="https://github.com/user-attachments/assets/b030a7ec-22ef-4548-9f38-334597b29bff" />

