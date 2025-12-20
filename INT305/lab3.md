### Strengthening System Security on Linux Servers

### **Objective**:

- To understand and apply fundamental Linux security measures for file systems, network services, remote access, and system monitoring.
- To gain hands-on experience with tools and practices for enhancing system security.

#### **Exercise 1: Locate and Open the `adduser.conf` File**

1. **Find the `adduser.conf` File**:
    
- The

```bash
adduser.conf
```

    

```bash
ls /etc/adduser.conf
```

        
2. **Open the File for Review**:
    
- Use a text editor (e.g.,

```bash
nano
```

    

```bash
sudo nano /etc/adduser.conf
```

        
    - Read through the default configuration settings for user creation.

---

#### **Exercise 2: Analyze Key Configuration Parameters**

1. **Default Group Settings**:
    
    - Look for the parameter `GROUP=100`. This defines the default primary group for new users.
    - 
2. **Home Directory Settings**:
    
    - Identify the parameter `DHOME=/home`, specifying where new users' home directories will be created.
3. **Skel Directory**:
    
- Locate

```bash
SKEL=/etc/skel
```

4. **Default Shell**:
    
    - Check the parameter `DSHELL=/bin/`, which defines the default login shell for new users.
5. **Useful Fields in `adduser.conf`**:
    
    - **FIRST_UID**: The first UID (User ID) to be assigned to new users.
    - **LAST_UID**: The last UID number that can be assigned to regular users.
    - **FIRST_GID**: The first GID (Group ID) to be assigned to a user’s primary group.
    - **LAST_GID**: The last GID number available for regular user groups.
    - **USERGROUPS**: Controls whether to create a user with a group of the same name (yes or no).
    - **HOME**: Specifies the default directory location for user home directories.
    - **LOGIN_SHELL**: Specifies the default login shell for new users (e.g., `/bin/`).

---

#### **Exercise 3: Modify the Configuration**

1. **Change Default Home Directory Location**:
    
    - Modify the `DHOME` value to `/mnt/users` in the `adduser.conf` file. Save the file.
2. **Customize UID and GID Ranges**:
    
    - Change `FIRST_UID` to `2000` and `LAST_UID` to `2999`.
    - Change `FIRST_GID` to `3000` and `LAST_GID` to `3999`.
3. **Disable User-Specific Groups**:
    
    - Set `USERGROUPS=no` in the configuration file.
4. **Add Custom Files to the Skel Directory**:
    
    - Create a custom file in `/etc/skel`:
        

```bash
echo "Welcome to your new account!" | sudo tee /etc/skel/welcome.txt
```

        
5. **Set a Different Default Shell**:
    
    - Change `DSHELL` to `/bin/sh`. Save the file.

---

#### **Exercise 4: Test the Changes**

1. **Create a New User**:
    
    - Use the `adduser` command to create a new user:
        

```bash
sudo adduser testuser
```

        
2. **Verify the Changes**:
    
    - Check the home directory of the new user:
        

```bash
ls /mnt/users/testuser
```

        
    - Confirm that the `welcome.txt` file exists in the home directory.
    - Verify the UID, GID, and default shell for the new user:
        

```bash
grep testuser /etc/passwd
```

        
---

### **Access Control Lists (ACLs)**

#### **Scenario**

You are a system administrator managing a shared project folder for a development team. The project folder is shared among three team members: Alice, Bob, and Charlie.

- **Alice**: Needs full read, write, and execute permissions for the folder.
- **Bob**: Can only read files but should not modify or delete them.
- **Charlie**: Needs both read and write permissions but should not delete files.

Your Exercise is to configure the folder's permissions using **Access Control Lists (ACLs)** to meet these requirements.

---

### **Objective**

Understand and implement ACLs to assign fine-grained permissions to specific users for a shared directory.

---
#### **Exercise 1: Create the Project Folder and Test Files**

1. Create the project folder:
    

```bash
sudo mkdir /projects/team_project
```

    
2. Create test files in the folder:
    

```bash
sudo touch /projects/team_project/{file1.txt,file2.txt}
```

    
3. Change ownership of the folder to a generic group (e.g.,

```bash
developers
```

    

```bash
sudo chown -R root:developers /projects/team_project
```

    
4. Set default permissions to allow group access:
    

```bash
sudo chmod 770 /projects/team_project
```

    
---

#### **Exercise 2: Configure ACLs for Each User**

1. **Grant Alice Full Permissions (Read, Write, Execute)**:


```bash
sudo setfacl -m u:alice:rwx /projects/team_project
```

    
2. **Grant Bob Read-Only Permissions**:
    

```bash
sudo setfacl -m u:bob:rx /projects/team_project
```

    
3. **Grant Charlie Read and Write Permissions Without Deletion**:
    
    - To prevent deletion, set the sticky bit and assign specific write permissions:
        

```bash
sudo chmod +t /projects/team_project sudo setfacl -m u:charlie:rw /projects/team_project
```

        
4. **Verify the ACL Settings**:
    
    - Check the ACLs for the directory:
        
    `getfacl /projects/team_project`
        
---

#### **Exercise 3: Test the Permissions**

1. Switch to each user and test their access rights:
    
    - For Alice:
        

```bash
sudo su - alice cd /projects/team_project echo "Alice can write" > file1.txt
```

        
    - For Bob:
        

```bash
sudo su - bob cd /projects/team_project cat file1.txt echo "Bob can write" >> file1.txt  # This should fail.
```

        
    - For Charlie:
        

```bash
sudo su - charlie cd /projects/team_project echo "Charlie can write" > file2.txt rm file1.txt  # This should fail due to the sticky bit.
```

        

---

#### **Exercise 4: Manage Default ACLs**

1. Set default ACLs so new files inherit permissions:

```bash
sudo setfacl -d -m u:alice:rwx /projects/team_project 
sudo setfacl -d -m u:bob:rx /projects/team_project 
sudo setfacl -d -m u:charlie:rw /projects/team_project
```


2. Verify default ACLs:
    
```bash
getfacl /projects/team_project
```

---

### **Deliverables**

1. Output of the

```bash
getfacl
```

2. Screenshots or logs showing test results for each user’s access rights.
3. Explanation of how the sticky bit and ACLs work together to meet the requirements.

---

### **Grading Criteria**

1. Correct application of ACLs for Alice, Bob, and Charlie.
2. Proper use of the sticky bit to prevent unauthorized deletion.
3. Clear documentation of test results and outputs.

## Sudo and Privilege Management 

---

#### **Scenario**

As a system administrator, you are Exerciseed with managing user privileges for a team of engineers. Each user has different access requirements for administrative Exercises.

1. **John**: Needs full administrative privileges to perform any Exercise.
2. **Mary**: Can manage system updates but cannot modify user accounts or access sensitive files.
3. **Paul**: Can restart and manage specific services like Apache and MySQL but cannot make any other system changes.

Your Exercise is to configure **sudo privileges** to meet these requirements.

---

### **Objective**

Understand and implement sudo configurations for fine-grained privilege management.

---
#### **Exercise 1: Create User Accounts**

1. Create the users:
    

```bash
sudo useradd -m john sudo useradd -m mary sudo useradd -m paul
```

    
2. Set passwords for the users:


```bash
sudo passwd john sudo passwd mary sudo passwd paul
```

    
---

#### **Exercise 2: Configure Sudo Privileges**

1. **Grant John Full Administrative Privileges**:
    
- Add John to the

```bash
sudo
```

    

```bash
sudo usermod -aG sudo john
```

        
    - Verify that John can execute any command:
        

```bash
su - john sudo whoami  # Should return "root"
```

        
2. **Grant Mary Privileges to Manage System Updates**:
    
    - Edit the sudoers file:
    

```bash
sudo visudo
```

        
    - Add the following rule at the end:
        

```bash
mary ALL=(ALL) NOPASSWD: /usr/bin/apt update, /usr/bin/apt upgrade
```

        
    - Test Mary’s access:
        

```bash
su - mary sudo apt update  # Should work without a password. sudo useradd testuser  # Should fail.
```

        
3. **Grant Paul Access to Manage Specific Services**:
    
    - Edit the sudoers file:
    

```bash
sudo visudo
```

        
    - Add the following rule:
        

```bash
paul ALL=(ALL) NOPASSWD: /bin/systemctl restart apache2, /bin/systemctl restart mysql
```

        
    - Test Paul’s access:
      

```bash
su - paul sudo systemctl restart apache2  # Should work. sudo systemctl restart ssh  # Should fail.
```

        

---

#### **Exercise 3: Restrict Access to the Sudo Command**

1. Prevent unauthorized users from using

```bash
sudo
```

    
- Ensure only specific users are part of the

```bash
sudo
```

     

```bash
getent group sudo
```

        
2. Remove a user from the

```bash
sudo
```



```bash
sudo deluser <username> sudo
```

    

---

#### **Exercise 4: Logging and Monitoring Sudo Usage**

1. Enable sudo logs in

```bash
/var/log/auth.log
```

    
2. Test logging by running a command as a sudo user and checking the log:
    

```bash
sudo tail -f /var/log/auth.log
```

    
3. Look for entries indicating which commands were executed using

```bash
sudo
```

    
---

### **Deliverables**

1. Screenshots or logs showing the

```bash
sudo
```

2. Test results confirming correct permission enforcement for John, Mary, and Paul.
3. Explanation of how the sudoers file is used to manage privileges.

---

### **Grading Criteria**

1. Correct sudo configurations for all three users.
2. Proper restriction of unauthorized commands.
3. Clear evidence of logging and monitoring sudo usage.

**Securing Network Services and Ports**

1. **List Open Ports**:
    
- Use

```bash
ss
```

    

```bash
sudo ss -tuln
```

        
2. **Close Unnecessary Ports**:
    
    - Stop an unnecessary service (e.g., Apache):
    

```bash
sudo systemctl stop apache2 sudo systemctl disable apache2
```

        

---

#### **Exercise 4: SSH and Remote Access**

1. **Secure the SSH Service**:
    
    - Edit the SSH configuration file:
     

```bash
sudo nano /etc/ssh/sshd_config
```

        
    - Change the SSH port (e.g., to 2222):
     
        `Port 2222`
        
2. **Restart SSH**:


```bash
sudo systemctl restart sshd
```

    

---

#### **Exercise 5: System Update and Patching**

1. **Check for Updates**:
    
    - Use:
     

```bash
sudo apt update sudo apt upgrade
```

        
2. **Automate Updates**:
    
    - Install `unattended-upgrades`:
      

```bash
sudo apt install unattended-upgrades sudo dpkg-reconfigure unattended-upgrades
```

        

---

### **Implementing Two-Factor Authentication (2FA) with Google Authenticator**

---

#### **Objective**

Enable Two-Factor Authentication (2FA) for system login using Google Authenticator and configure it in the

```bash
common-auth
```


---

### **Steps to Implement 2FA**

#### **Step 1: Install Google Authenticator**

1. Update the system package index:
   

```bash
sudo apt update
```

    
2. Install the Google Authenticator PAM module:
  

```bash
sudo apt install libpam-google-authenticator -y
```

    
---

#### **Step 2: Configure Google Authenticator for Your User**

1. Switch to the user account you want to configure 2FA for:

    `su - <username>`
    
2. Run the Google Authenticator setup:


```bash
google-authenticator
```

    
3. Follow the prompts:
    
    - **QR Code**: Scan the QR code using the Google Authenticator app on your smartphone.
    - **Emergency Codes**: Save the emergency backup codes provided (these can be used if you lose access to the app).
    - **Enable Time-Based Tokens**: Answer `yes` when asked if you want to enable time-based tokens.

---

#### **Step 3: Configure PAM for 2FA**

1. Open the `common-auth` file:
   

```bash
sudo nano /etc/pam.d/common-auth
```

    
2. Add the following line **at the top** of the file:


```bash
auth required pam_google_authenticator.so
```

    
3. Save and exit the file (`Ctrl+O`, `Enter`, `Ctrl+X`).
    
---

#### **Step 4: Test 2FA Configuration**

1. Open a new terminal or SSH session and attempt to log in as the configured user.
    
2. After entering the username and password, you should be prompted for the 2FA token generated by the Google Authenticator app.
    

---

#### **Step 5: (Optional) Backup and Restore**

1. If you want to set up Google Authenticator on another device, note the secret key displayed during the setup in Step 2.
    
2. Use this secret key to manually add the account on another device.
    

---

### **Deliverables**

1. **Screenshot of the Google Authenticator app** on your phone showing the account and token.
2. **Screenshot of the common-auth configuration file** showing the added line.
3. Evidence of a successful login attempt using 2FA (e.g., a terminal screenshot showing the token entry prompt and successful access).

---

### **Grading Criteria**

1. Correctly configured 2FA using Google Authenticator.
2. Screenshot of the Google Authenticator app with the account setup.
3. Proof of successful implementation (e.g., login screenshot).

### **Implementing Key-Based Authentication and Securing SSH Access**

---

#### **Scenario**

You are a cybersecurity analyst at **SecureTech Ltd**. In addition to disabling root login, the company wants to implement **key-based authentication** for enhanced SSH security. Your Exercise is to configure SSH for key-based authentication, test the setup, and ensure the root user is securely disabled.

---

### **Assignment Exercises**

#### **Part 1: Configure SSH Key-Based Authentication**
1. **Switch to the root user**

```bash
sudo su root
```

1. **Generate SSH Key Pair**
    
    - On your local machine, generate an SSH key pair (public and private keys):
        

```bash
ssh-keygen -t rsa -b 4096
```

        
- Press

```bash
Enter
```

    - When prompted, set a passphrase for added security (optional).
2. **Copy the Public Key to the Server**
    
    - Use the following command to copy your public key to the server:


```bash
ssh-copy-id <username>@<server-ip>
```

        
4. **Edit the SSH Configuration File**
    
    - Open the SSH configuration file on the server:
    

```bash
sudo nano /etc/ssh/sshd_config
```

        
    - Ensure the following lines are set:
    

```bash
PubkeyAuthentication yes PasswordAuthentication no
```

        
    - Save and exit.
5. **Restart the SSH Service**
    
    - Restart the SSH service to apply changes:
    

```bash
sudo systemctl restart ssh
```

        
6. **Test Key-Based Authentication**
    
    - Attempt to log in to the server using the private key:
    

```bash
ssh <username>@<server-ip>
```

        
    - Confirm that the login works without a password prompt.

---

#### **Part 2: Disable Root Login**

1. **Edit the SSH Configuration File**
    
- In the SSH configuration file (

```bash
/etc/ssh/sshd_config
```

        
        `PermitRootLogin no`
        
    - Save and exit.
2. **Restart the SSH Service**
    
    - Restart the SSH service again to apply the root login changes:
    

```bash
sudo systemctl restart sshd
```

        
3. **Test Root Login**
    
    - Verify that logging in as root is no longer possible:
     

```bash
ssh root@<server-ip>
```

        

---
### **Deliverables**

1. **Screenshot of the key generation process** on your local machine.
2. **Screenshot of the public key being copied to the server** and the `authorized_keys` file setup.
3. **Screenshot of the

```bash
sshd_config
```

4. **Screenshot of the SSH service restart**.
5. **Screenshot of a successful key-based login** and a failed root login attempt.

---

### **Grading Criteria**

1. SSH key pair is successfully generated and copied to the server.
2. Key-based authentication is correctly configured and tested.
3. Root login is disabled, and testing confirms it.
4. All required screenshots are submitted.

---

### **Configuring User Account Security with `login.defs`**

---

#### **Scenario**

You are a system administrator for **CyberShield Inc.**, a company that handles sensitive client data. To comply with security policies, you are Exerciseed with strengthening user account security by configuring parameters in the

```bash
login.defs
```


Your goal is to ensure that all user accounts adhere to these policies for better security management.

---

## Exercises

#### **Part 1: Exploring `login.defs`**

1. **Locate the

```bash
login.defs
```

    
    - Use the following command to locate the file:


```bash
sudo nano /etc/login.defs
```

        
2. **Review Key Fields**
    
    - Find and take note of the following fields and their current values:
-

```bash
PASS_MAX_DAYS
```

-

```bash
PASS_MIN_DAYS
```

-

```bash
PASS_WARN_AGE
```

        - `UID_MIN` and `UID_MAX`: Range of UIDs for regular user accounts.
        - `GID_MIN` and `GID_MAX`: Range of GIDs for regular groups.

#### **Part 2: Configure `login.defs` for Secure Account Management**

1. **Set Password Policies**
    
    - Edit the file to set the following values:
      
        `PASS_MAX_DAYS   90 PASS_MIN_DAYS   7 PASS_WARN_AGE   14`
        
2. **Set UID and GID Ranges**
    
    - Define the range for user IDs and group IDs to restrict system users:
        
        `UID_MIN         1000 UID_MAX         60000 GID_MIN         1000 GID_MAX         60000`
        
3. **Save and Exit**
    
    - Save your changes and close the editor.

#### **Part 3: Testing the Configuration**

1. **Create a Test User**
    
    - Add a new user to verify the settings:
      

```bash
sudo useradd testuser
```

        
2. **Check Password Expiration**
    
- Use the

```bash
chage
```

        

```bash
sudo chage -l testuser
```

        
3. **Modify the Password**
    
- Set a password for the test user and verify compliance with the

```bash
PASS_MIN_DAYS
```

             

```bash
sudo passwd testuser
```

        
4. **Attempt Early Password Change**
    
    - Log in as the test user and try changing the password before 7 days have passed:


```bash
passwd
```

        

---

### **Deliverables**

1. **Screenshot of the edited `login.defs` file** showing updated fields.
2. **Screenshot of the

```bash
chage
```

3. **Screenshot of an attempt to change the password before the minimum days have elapsed** and the resulting error.

---

### **Grading Criteria**

1. The `login.defs` file is correctly edited with the specified values.
2. Password policies are accurately reflected in the

```bash
chage
```

3. The system enforces the minimum password age when an early change is attempted.
4. All required screenshots are submitted.

---
### **Configuring System Auditing with `auditd`**

---

#### **Scenario**

You are the security administrator for **SecureNet Corp.**, a company dealing with sensitive data. To improve security and comply with regulatory standards, you are Exerciseed with setting up system auditing to track critical events. You will use the

```bash
auditd
```


Your goal is to configure

```bash
auditd
```


---

### Exercises**

#### **Part 1: Install and Configure `auditd`**

1. **Install `auditd`**
    
    - First, ensure that `auditd` is installed on your system:
    

```bash
sudo apt update sudo apt install auditd
```

        
2. **Start and Enable `auditd` Service**
    
    - Start the `auditd` service and enable it to run on boot:
      

```bash
sudo systemctl start auditd sudo systemctl enable auditd
```

        
3. **Verify `auditd` Status**
    
    - Check the status of the `auditd` service:
     

```bash
sudo systemctl status auditd
```

        

#### **Part 2: Configure Audit Rules**

1. **View Current Audit Rules**
    
    - List the current audit rules to see the default configuration:
    

```bash
sudo auditctl -l
```

        
2. **Add Audit Rule to Monitor User Logins**
    
    - Add an audit rule to monitor successful and failed login attempts by editing the rules file:
      

```bash
sudo nano /etc/audit/rules.d/audit.rules
```

        
        Add the following lines to monitor user logins:
        
        `-w /var/log/auth.log -p wa -k user-logins`
        
3. **Add Rule to Monitor Access to Sensitive Files**
    
- Add audit rules to monitor access and modification of critical system files, such as

```bash
/etc/passwd
```

    

```bash
-w /etc/passwd -p wa -k passwd-modifications
```

        
4. **Save and Apply Rules**
    
    - After making the changes, save the file and reload the audit rules:
      

```bash
sudo service auditd restart
```

        

#### **Part 3: Generate Audit Logs**

1. **Simulate a User Login**
    
    - Log in to the system with a test user:
     

```bash
sudo useradd testuser sudo passwd testuser
```

        
2. **Check the Audit Logs**
    
    - Review the audit logs for entries related to login activities:
        

```bash
sudo ausearch -k user-logins
```

        
3. **Simulate a Modification of a Critical File**
    
- As the root user, modify the

```bash
/etc/passwd
```

    

```bash
sudo nano /etc/passwd
```

        
        Save and exit.
4. **Check for File Modification Logs**
    
- Review the audit logs for any changes to the

```bash
/etc/passwd
```

     

```bash
sudo ausearch -k passwd-modifications
```

        

#### **Part 4: Testing and Verification**

1. **Test System Reboot**
    
    - Reboot the system and verify that the audit daemon is still running:
      

```bash
sudo reboot sudo systemctl status auditd
```

        
2. **Check for Audit Log Integrity**
    
    - Check the integrity of the logs to ensure they haven't been tampered with:
      

```bash
sudo ausearch -i
```

        

---

### **Deliverables**

1. **Screenshot of the `auditd` status** after installation and service startup.
2. **Screenshot of the audit rules** from

```bash
/etc/audit/rules.d/audit.rules
```

3. **Screenshot of the output** from

```bash
ausearch
```

4. **Screenshot of the test file modification** logs related to

```bash
/etc/passwd
```

5. **Screenshot of the audit log verification** after the system reboot.

