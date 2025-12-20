# **INT305: Secure User Access Management in Linux – Lab 4**

## **Lab 4: Advanced User Access Control and Security Auditing**

---

### **Objective**

By the end of this lab, students will be able to:
- Implement advanced user access control mechanisms in Linux
- Perform security audits on user accounts and permissions
- Configure and manage password policies and account expiration
- Monitor and analyze user activity logs
- Apply principle of least privilege in user management

---

### **Prerequisites**

- Completion of INT305 Labs 1-3
- Basic understanding of Linux user management
- Familiarity with file permissions and ACLs
- Access to a Linux system (Kali Linux, Ubuntu, or similar)
- Root or sudo privileges

---

### **Learning Outcomes**

After completing this lab, students will:
- Understand advanced security configurations for user accounts
- Be able to implement password aging and complexity requirements
- Know how to audit user access and identify security risks
- Be proficient in using security tools for user management
- Understand compliance requirements for user access control

---

### **Materials Needed**

- Linux-based system (Kali Linux, Ubuntu, or CentOS)
- Terminal access with sudo privileges
- Text editor (nano, vim, or gedit)
- Internet access for package installation (if needed)

---

## **Part 1: Password Policy Configuration**

### **Exercise 1.1: Configure Password Aging**

Password aging ensures that users change their passwords regularly, reducing the risk of compromised credentials.

1. **View current password aging settings for a user:**

```bash
sudo chage -l username
```

2. **Set password expiration policies:**

```bash
# Set password to expire after 90 days
sudo chage -M 90 username

# Set minimum days between password changes
sudo chage -m 7 username

# Set warning period before password expiration
sudo chage -W 14 username

# Set account expiration date
sudo chage -E 2025-12-31 username
```

3. **Configure system-wide password aging in `/etc/login.defs`:**

```bash
sudo nano /etc/login.defs
```

Modify the following parameters:

```
PASS_MAX_DAYS   90
PASS_MIN_DAYS   7
PASS_WARN_AGE   14
```

**Question 1.1:** Why is it important to set a minimum number of days between password changes?

**Question 1.2:** What are the security implications of setting PASS_MAX_DAYS too high or too low?

---

### **Exercise 1.2: Implement Password Complexity Requirements**

1. **Install the PAM password quality checking library:**

```bash
sudo apt update
sudo apt install libpam-pwquality -y
```

2. **Configure password complexity in `/etc/security/pwquality.conf`:**

```bash
sudo nano /etc/security/pwquality.conf
```

Add or modify the following settings:

```
# Minimum password length
minlen = 12

# Require at least one digit
dcredit = -1

# Require at least one uppercase character
ucredit = -1

# Require at least one lowercase character
lcredit = -1

# Require at least one special character
ocredit = -1

# Number of characters in the new password that must not be present in the old password
difok = 3

# Reject passwords which contain more than 2 same consecutive characters
maxrepeat = 2

# Check whether the password contains the user name
usercheck = 1
```

3. **Test the password policy:**

```bash
# Try to set a weak password
sudo passwd testuser
```

**Question 1.3:** What happens when you try to set a password that doesn't meet the complexity requirements?

**Question 1.4:** How do password complexity requirements help prevent brute-force attacks?

---

## **Part 2: Account Security Auditing**

### **Exercise 2.1: Identify Inactive User Accounts**

1. **Find users who haven't logged in for 90+ days:**

```bash
# List all users with their last login date
sudo lastlog | grep -v "Never"

# Find users who haven't logged in for 90 days
sudo lastlog -b 90
```

2. **Check for accounts with empty passwords:**

```bash
sudo awk -F: '($2 == "") {print $1}' /etc/shadow
```

3. **List all users with UID 0 (root privileges):**

```bash
awk -F: '($3 == "0") {print $1}' /etc/passwd
```

**Warning:** Only the root account should have UID 0. Any other accounts with UID 0 represent a serious security risk.

4. **Find accounts without passwords or with locked passwords:**

```bash
sudo passwd -S -a
```

**Question 2.1:** Why are inactive accounts a security risk?

**Question 2.2:** What actions should be taken for accounts that haven't been used in 90+ days?

---

### **Exercise 2.2: Audit User Permissions and Group Memberships**

1. **List all users and their groups:**

```bash
# Show all groups for a specific user
groups username

# Show all users in a specific group
getent group groupname
```

2. **Find users with sudo privileges:**

```bash
# Check sudo group members
getent group sudo

# Check sudoers file
sudo cat /etc/sudoers
```

3. **Identify users with shell access:**

```bash
# List users with valid login shells
grep -v '/nologin\|/false' /etc/passwd
```

4. **Find files owned by specific users:**

```bash
# Find all files owned by a user
sudo find / -user username -ls 2>/dev/null

# Find SUID files (potential security risk)
sudo find / -perm -4000 -type f -ls 2>/dev/null
```

**Question 2.3:** Why are SUID files a potential security concern?

**Question 2.4:** What is the principle of least privilege, and how does it apply to user management?

---

## **Part 3: User Activity Monitoring**

### **Exercise 3.1: Analyze Authentication Logs**

1. **View recent authentication attempts:**

```bash
# View successful logins
sudo last -a

# View failed login attempts
sudo lastb

# View authentication log
sudo tail -f /var/log/auth.log
```

2. **Check for suspicious login patterns:**

```bash
# Count failed login attempts by user
sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-5)}' | sort | uniq -c | sort -nr

# Check for root login attempts
sudo grep "root" /var/log/auth.log | grep "Failed"
```

3. **Monitor current logged-in users:**

```bash
# Show who is currently logged in
w

# Show detailed information about logged-in users
who -a

# Show user login history
last -n 20
```

**Question 3.1:** What patterns might indicate a brute-force attack attempt?

**Question 3.2:** Why is it important to monitor root login attempts?

---

### **Exercise 3.2: Implement Account Lockout Policies**

1. **Configure account lockout after failed login attempts:**

Edit `/etc/pam.d/common-auth`:

```bash
sudo nano /etc/pam.d/common-auth
```

Add the following line:

```
auth required pam_tally2.so deny=5 unlock_time=1800 onerr=fail
```

This locks an account for 30 minutes (1800 seconds) after 5 failed login attempts.

2. **Check failed login attempts for a user:**

```bash
sudo pam_tally2 --user=username
```

3. **Manually unlock a locked account:**

```bash
sudo pam_tally2 --user=username --reset
```

**Question 3.3:** What are the trade-offs between security and usability when implementing account lockout policies?

---

## **Part 4: Sudo Access Management**

### **Exercise 4.1: Configure Fine-Grained Sudo Permissions**

1. **Edit the sudoers file safely:**

```bash
sudo visudo
```

2. **Grant specific command access to a user:**

```
# Allow user to run specific commands without password
username ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart apache2, /usr/bin/systemctl status apache2

# Allow user to run commands as specific user
username ALL=(webuser) /usr/bin/vim /var/www/html/*

# Allow group members to run all commands with password
%developers ALL=(ALL:ALL) ALL
```

3. **Create a sudo log file:**

Add to `/etc/sudoers`:

```
Defaults logfile="/var/log/sudo.log"
Defaults log_input, log_output
```

4. **Test sudo permissions:**

```bash
# Switch to the test user
su - username

# Try running a command with sudo
sudo systemctl status apache2
```

**Question 4.1:** Why is it recommended to use `visudo` instead of directly editing `/etc/sudoers`?

**Question 4.2:** What are the security implications of using NOPASSWD in sudo configurations?

---

## **Part 5: Security Compliance and Best Practices**

### **Exercise 5.1: Perform a Security Audit Checklist**

Create a script to automate security checks:

```bash
#!/bin/bash
# User Access Security Audit Script

echo "=== User Access Security Audit ==="
echo ""

echo "1. Checking for users with UID 0:"
awk -F: '($3 == "0") {print $1}' /etc/passwd
echo ""

echo "2. Checking for accounts with empty passwords:"
sudo awk -F: '($2 == "") {print $1}' /etc/shadow
echo ""

echo "3. Checking for users with sudo access:"
getent group sudo
echo ""

echo "4. Checking password aging policies:"
grep "^PASS" /etc/login.defs
echo ""

echo "5. Finding SUID files:"
sudo find / -perm -4000 -type f 2>/dev/null | head -10
echo ""

echo "6. Recent failed login attempts:"
sudo lastb | head -10
echo ""

echo "7. Currently logged in users:"
w
echo ""

echo "=== Audit Complete ==="
```

Save this script as `security_audit.sh` and run it:

```bash
chmod +x security_audit.sh
sudo ./security_audit.sh
```

**Question 5.1:** What additional checks would you add to this security audit script?

---

### **Exercise 5.2: Implement User Access Review Process**

1. **Create a user access report:**

```bash
#!/bin/bash
# Generate user access report

echo "User Access Report - $(date)" > user_access_report.txt
echo "======================================" >> user_access_report.txt
echo "" >> user_access_report.txt

echo "All User Accounts:" >> user_access_report.txt
awk -F: '{print $1 " (UID: " $3 ")"}' /etc/passwd >> user_access_report.txt
echo "" >> user_access_report.txt

echo "Users with Shell Access:" >> user_access_report.txt
grep -v '/nologin\|/false' /etc/passwd | awk -F: '{print $1}' >> user_access_report.txt
echo "" >> user_access_report.txt

echo "Last Login Information:" >> user_access_report.txt
sudo lastlog >> user_access_report.txt

cat user_access_report.txt
```

2. **Document findings and recommendations:**

Create a file `security_recommendations.txt` with your findings.

**Question 5.2:** How often should user access reviews be conducted in a production environment?

---

## **Part 6: Practical Challenge**

### **Challenge: Secure a Multi-User System**

You have been tasked with securing a Linux server that will host multiple users from different departments. Implement the following security measures:

1. Create three user groups: `developers`, `analysts`, and `admins`
2. Create at least 2 users in each group
3. Configure password policies requiring:
   - Minimum 14 characters
   - At least one uppercase, lowercase, digit, and special character
   - Password expiration every 60 days
   - Minimum 10 days between password changes
4. Grant sudo access to `admins` group for all commands
5. Grant sudo access to `developers` group for only web server management commands
6. Configure account lockout after 3 failed login attempts
7. Create a script that generates a weekly security audit report
8. Document all configurations and justify your security decisions

**Deliverable:** Submit a report documenting:
- All commands used
- Configuration files modified
- Security rationale for each decision
- Test results demonstrating the configurations work as expected

---

## **Summary**

In this lab, you have learned:
- How to implement and enforce password policies
- Techniques for auditing user accounts and identifying security risks
- Methods for monitoring user activity and detecting suspicious behavior
- Best practices for sudo access management
- How to create automated security audit scripts
- The importance of regular user access reviews

These skills are essential for maintaining secure multi-user Linux systems and ensuring compliance with security policies.

---

## **Additional Resources**

- [Linux PAM Documentation](http://www.linux-pam.org/)
- [CIS Linux Benchmark](https://www.cisecurity.org/benchmark/distribution_independent_linux)
- [NIST Password Guidelines](https://pages.nist.gov/800-63-3/)
- [Linux Security Hardening Guide](https://www.cyberciti.biz/tips/linux-security.html)

---

## **Submission Requirements**

Submit the following:
1. Screenshots of completed exercises
2. Your security audit script
3. User access report
4. Answers to all questions
5. Documentation of the practical challenge

**Note:** Ensure all sensitive information (passwords, actual usernames) is redacted from your submission.
