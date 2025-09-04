# Day 04 - Script Execution Permissions 📜🔐

## 📌 Task
- A script xfusioncorp.sh was placed in /tmp on App Server 2.
- Initially, it had no executable permissions.
- Goal: Grant executable permissions so all users can run it.
- Ensure correct permissions are applied (755).
---

## 🛠️ Commands Used

```bash
# SSH into App Server 2
ssh steve@stapp02

# Try running the script (fails due to missing permissions)
./tmp/xfusioncorp.sh

# Add executable permission for all users (requires sudo)
sudo chmod a+x /tmp/xfusioncorp.sh

# Set standard script permissions (owner rwx, others rx)
sudo chmod 755 /tmp/xfusioncorp.sh

# Verify permissions
ls -l /tmp/xfusioncorp.sh

```

## 📝 Notes
- Without x permission → script cannot be executed.
- a+x gives execute access to all users.
- 755 is the standard for shared scripts:
- Owner: read, write, execute
- Group: read, execute
- Others: read, execute
