
# Day 06 - Schedule Cron Job for Root User ⏰👨‍💻

## 📌 Task
- Install cronie package on all Nautilus app servers.
- Start and enable the crond service.
- Add a cron job for the root user to run every 5 minutes.
- The cron job should write hello into /tmp/cron_text.
- Verify that the cron job is working properly.
---

## 🛠️ Commands Used

```bash
# Install cronie package
sudo yum install -y cronie

# Start and enable crond service
sudo systemctl start crond
sudo systemctl enable crond

# Add cron job for root
sudo crontab -e
# Inside editor, add:
*/5 * * * * echo hello > /tmp/cron_text

# Verify cron job entry
sudo crontab -l

# Check cron service status
sudo systemctl status crond

# Verify output file after 5 minutes
sudo cat /tmp/cron_text

```

## 📝 Notes
- cronie → package that provides the cron daemon (crond).
- systemctl start crond → starts the cron service immediately.
- systemctl enable crond → ensures cron starts on system boot.
- sudo crontab -e → edits cron for root user only.
- */5 * * * * → runs the command every 5 minutes.
- echo hello > /tmp/cron_text → overwrites the file with "hello".
- crontab -l → lists cron jobs for the current user.
- /tmp/cron_text should contain hello once cron run

- ## ✅ Outcomes
- Cron service is installed and enabled on all app servers.
- Root user has a scheduled cron job that runs every 5 minutes.
- /tmp/cron_text is created automatically and contains the text hello.

  <img width="593" height="283" alt="day6a" src="https://github.com/user-attachments/assets/1c19813b-9e00-4bbb-9aa8-b47932aaed80" />
<img width="641" height="303" alt="day6" src="https://github.com/user-attachments/assets/172407bb-e9a4-42b4-a411-21d0e01c3090" />

