
# Day 05 - SELinux Installation & Configuration 🔐🐧

## 📌 Task
- Install required SELinux packages on App Server 2.
- Permanently disable SELinux (it will be re-enabled later if needed).
- Do not reboot now (maintenance reboot is already planned).
- After reboot, SELinux should remain disabled.  

---

## 🛠️ Commands Used

```bash
# SSH into App Server 2
ssh tony@stapp02

# Install SELinux packages
sudo yum install -y selinux-policy selinux-policy-targeted policycoreutils

# Disable SELinux permanently
sudo sed -i 's/^SELINUX=.*/SELINUX=disabled/' /etc/selinux/config

# Verify configuration file
cat /etc/selinux/config | grep SELINUX

# Check SELinux status (may still be enforcing until reboot)
sestatus

```

## 📝 Notes
- yum install selinux-policy selinux-policy-targeted policycoreutils → installs required SELinux packages.
- /etc/selinux/config → main config file to set enforcing, permissive, or disabled.
- sed -i 's/^SELINUX=.*/SELINUX=disabled/' → modifies config to disable SELinux.
- sestatus → shows the current runtime status, which may still be enforcing until reboot.
- After reboot, sestatus will report disabled

- ## ✅ Outcomes
- SELinux packages installed successfully.
- /etc/selinux/config shows SELINUX=disabled.
- SELinux will be disabled permanently after scheduled reboot
<img width="840" height="390" alt="day5" src="https://github.com/user-attachments/assets/2be94f64-a41e-4210-98c4-14e2e4a078a4" />

<img width="893" height="418" alt="day5a" src="https://github.com/user-attachments/assets/2e955363-25f5-4c0f-a30e-c565a1846191" />
