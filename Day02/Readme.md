# Day 02 - Linux User Setup with Non-Interactive Shell 👤

## 📌 Task
Create a new Linux user.

Set an account expiry date for the user.

Verify that the expiry date is correctly applied

---

## 🛠 Commands Used
```bash
# Create a new user with expiry date (format: YYYY-MM-DD)
sudo useradd -e YYYY-MM-DATE devuser2

# Set password for the new user
sudo passwd devuser2

# Verify expiry date of the user
sudo chage -l devuser2
```

## 📝 Notes
useradd -e <date> is used to set account expiry.
 
Once expired, the user cannot log in, but files owned by them remain.
 
chage -l <username> is a very useful command to check password aging and expiry details.
 

---

## ✅ Outcomes
A new user devuser2 exists with an expiry date.

chage -l devuser2 shows the expected Account expires date.

After the expiry date, the account will not allow login (files remain).  
