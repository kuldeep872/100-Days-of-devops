# Day 10 - Linux Bash Scripts 📜

## 📌 Task
- Write and execute a basic Bash script.
- Automate simple system tasks.

---

## 🛠️ Commands Used
```bash
# Create a script file
nano backup.sh

# Example script content
#!/bin/bash
echo "Backup started..."
date
tar -czf /tmp/etc-backup.tar.gz /etc
echo "Backup completed!"

# Save and exit (CTRL+O, CTRL+X)

# Give execute permission
chmod +x backup.sh

# Run the script
./backup.sh
```

<img width="1092" height="624" alt="image" src="https://github.com/user-attachments/assets/25ffc1b8-143e-48ec-9313-fc9f8279580a" />
