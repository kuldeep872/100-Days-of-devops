# Day 09 - MariaDB Troubleshooting 🛠️

## 📌 Task
- Troubleshoot MariaDB service.
- Check logs and configuration.
- Fix errors and verify service status.

---

## 🛠️ Commands Used
```bash
# Check MariaDB service status
sudo systemctl status mariadb

# Start or restart service if stopped
sudo systemctl start mariadb
sudo systemctl restart mariadb

# Check error logs (path may vary)
sudo cat /var/log/mariadb/mariadb.log | tail -n 50
# Verify MariaDB version
mysql --version
```
<img width="1085" height="571" alt="image" src="https://github.com/user-attachments/assets/c777072c-bfc7-4469-b28f-e225014aef0b" />
