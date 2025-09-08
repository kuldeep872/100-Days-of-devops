# Day 08 - Install Ansible ⚙️

## 📌 Task
- Install Ansible on a Linux server.
- Verify installation.
- Run a sample ad-hoc command.

---

## 🛠️ Commands Used
```bash
# Update packages
sudo apt update   # (Debian/Ubuntu)
# or
sudo yum install epel-release -y   # (RHEL/CentOS)

# Install Ansible
sudo apt install ansible -y
# or
sudo yum install ansible -y

# Verify installation
ansible --version

# Run a simple ad-hoc command (localhost ping)
ansible localhost -m ping
```

## 📝 Notes
- Ansible is an agentless automation tool (no client install required).
- Uses SSH for remote communication.
- Ad-hoc commands are quick one-liners, playbooks are reusable configs
 ## ✅ Outcomes
- Ansible installed successfully.
- Version verified with ansible --version.
- First ad-hoc command (ping) executed on localhost
<img width="862" height="367" alt="day8" src="https://github.com/user-attachments/assets/ef9f6b50-8977-4dd2-8832-01f4caea818f" />
<img width="907" height="413" alt="day8a" src="https://github.com/user-attachments/assets/bd748d49-4347-4ca3-9fb8-43828a8187b9" />



