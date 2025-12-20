
# **Lab 1: Investigate Kali Linux**

## **Objectives**
In this lab, you will complete the following objectives:
- Familiarize yourself with the Kali Linux GUI.
- Master the Kali Linux shell and its utilities.
- Understand and perform advanced file and directory operations.
- Learn about file permissions and how to manipulate them.
- Practice using text processing and search tools.

## **Background / Scenario**
As your skills progress, efficiency in the Linux environment becomes critical. This lab builds on foundational knowledge by introducing more complex tasks and command combinations that are daily routines for security professionals.

## **Required Resources**
- Kali Linux virtual machine (VM) customized for Internship Training course.
- Internet access.

---

## **Instructions**

### **Part 1: Advanced Directory Navigation & Creation**

1.  **Navigate to your home directory:**
    ```bash
    cd ~
    ```
    **Exercise 1.1:** What is the difference between `cd ~` and `cd /home/kali`?

2.  **Create a complex directory structure in one command:**
    ```bash
    mkdir -p Lab1/{recon/{hosts,services},exploits,logs,evidence/{screenshots,packets}}
    ```
    **Exercise 1.2:** Use `tree` or `ls -R` to view the recursive structure you just created.

3.  **Navigate through the directories:**
    ```bash
    cd Lab1/recon/hosts
    pwd
    cd ../../evidence/packets
    pwd
    ```
    **Exercise 1.3:** Explain how the `../` syntax works in directory navigation.

### **Part 2: Comprehensive File Operations**

1.  **Create multiple practice files:**
    ```bash
    cd ~/Lab1
    touch scan_results.txt passlist.txt logfile.log config.conf secret.key data.xml
    ```

2.  **Copy with verification:**
    ```bash
    cp scan_results.txt scan_results_backup.txt
    cp passlist.txt ../passlist_backup.txt
    ```
    **Exercise 2.1:** Verify both copies were created successfully using `ls`.

3.  **Move and rename files:**
    ```bash
    mv config.conf exploits/
    mv logfile.log logs/application.log
    ```
    **Exercise 2.2:** Check that the files were moved and renamed correctly.

4.  **Bulk file operations:**
    ```bash
    mkdir temp_files
    touch temp_files/{1..10}.tmp
    ```
    **Exercise 2.3:** Delete all `.tmp` files in the `temp_files` directory with one `rm` command.

### **Part 3: File Content Management**

1.  **Create and view file content:**
    ```bash
    echo "Important findings from network scan" > scan_report.txt
    echo "Additional notes on vulnerabilities" >> scan_report.txt
    cat scan_report.txt
    ```

2.  **Compare file differences:**
    ```bash
    echo "Version 1.0" > config_old.txt
    echo "Version 2.0" > config_new.txt
    diff config_old.txt config_new.txt
    ```
    **Exercise 3.1:** What does the output of `diff` show you?

3.  **Search within files:**
    ```bash
    echo "ERROR: Authentication failed" >> logfile.txt
    echo "SUCCESS: User logged in" >> logfile.txt
    echo "ERROR: Connection timeout" >> logfile.txt
    grep "ERROR" logfile.txt
    ```
    **Exercise 3.2:** Use `grep -c` to count how many ERROR messages are in the file.

4.  **View partial file content:**
    ```bash
    head -3 logfile.txt
    tail -2 logfile.txt
    ```
    **Exercise 3.3:** Create a command that shows only lines 2-3 of logfile.txt using `head` and `tail`.

### **Part 4: Advanced Permission Exercises**

1.  **Check current permissions:**
    ```bash
    cd ~/Lab1
    ls -l
    ```

2.  **Create permission test files:**
    ```bash
    touch secret_file.txt admin_tool.sh public_read.txt
    ```

3.  **Modify permissions using symbolic method:**
    ```bash
    chmod u+x admin_tool.sh
    chmod o-r secret_file.txt
    chmod a+w public_read.txt
    ```
    **Exercise 4.1:** After each command, run `ls -l` and explain what changed.

4.  **Modify permissions using octal method:**
    ```bash
    chmod 755 admin_tool.sh
    chmod 600 secret_file.txt
    chmod 644 public_read.txt
    ```
    **Exercise 4.2:** What do each of these octal numbers (755, 600, 644) represent in terms of permissions?

5.  **Change file ownership (if possible):**
    ```bash
    sudo chown root secret_file.txt
    ls -l secret_file.txt
    ```

### **Part 5: Search and Find Operations**

1.  **Find files by name:**
    ```bash
    find ~/Lab1 -name "*.txt"
    find ~/Lab1 -name "scan*"
    ```

2.  **Find files by type:**
    ```bash
    find ~/Lab1 -type f
    find ~/Lab1 -type d
    ```
    **Exercise 5.1:** What's the difference between the outputs?

3.  **Find files by size:**
    ```bash
    find ~/Lab1 -size +1k
    find ~/Lab1 -size -100c
    ```

4.  **Find and execute commands:**
    ```bash
    find ~/Lab1 -name "*.sh" -exec chmod +x {} \;
    ```
    **Exercise 5.2:** What did this command accomplish?

### **Part 6: Text Processing Challenges**

1.  **Sorting output:**
    ```bash
    echo -e "apple\norange\nbanana\napple" > fruits.txt
    sort fruits.txt
    sort fruits.txt | uniq
    ```

2.  **Word counting:**
    ```bash
    wc scan_report.txt
    wc -l logfile.txt
    ```
    **Exercise 6.1:** What do the three numbers from `wc` represent?

3.  **Text transformation:**
    ```bash
    echo "hello world" | tr 'a-z' 'A-Z'
    echo "hello:world:test" | cut -d':' -f2
    ```

### **Part 7: Compression and Archiving**

1.  **Create archives:**
    ```bash
    tar -czf lab1_backup.tar.gz ~/Lab1
    tar -tzf lab1_backup.tar.gz
    ```

2.  **Extract archives:**
    ```bash
    mkdir extracted
    tar -xzf lab1_backup.tar.gz -C extracted/
    ```
    **Exercise 7.1:** Verify the extraction was successful.

### **Part 8: System Monitoring Exercises**

1.  **Process monitoring:**
    ```bash
    ps aux
    ps -ef | grep kali
    ```

2.  **Disk usage:**
    ```bash
    df -h
    du -sh ~/Lab1
    ```
    **Exercise 8.1:** How much space does your Lab1 directory use?

3.  **System information:**
    ```bash
    uname -a
    whoami
    ```

## **Challenge Exercises**

**Challenge 1:** Create a directory structure for a penetration test engagement with these requirements:
- Main directory called "Engagement_2024"
- Subdirectories for: reconnaissance, exploitation, reporting, evidence
- In the evidence directory, create subfolders for: screenshots, logs, packets
- Create a readme.txt file in each main directory

**Challenge 2:** Set up the following permission scheme:
- All `.sh` files should be executable only by the owner
- All `.txt` files should be readable by everyone but only writable by the owner
- Create one file that nobody can read, write, or execute

**Challenge 3:** Using only command line tools:
1. Find all `.log` files in your home directory
2. Count how many lines contain the word "ERROR"
3. Save the results to a file called `error_report.txt`

## **Conclusion**
You have now practiced comprehensive Linux command line operations that form the foundation of efficient security work in Kali Linux. These skills in file management, permission handling, text processing, and system navigation are essential for any cybersecurity professional.

## **Additional Resources**
- **Kali Linux Documentation**: [Kali Linux Docs](https://www.kali.org/docs/)
- **Linux Command Library**: Comprehensive command reference
- **GNU Coreutils Manual**: Detailed documentation on core utilities
