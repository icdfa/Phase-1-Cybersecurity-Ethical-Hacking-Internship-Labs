# Linux Command-Line Practical Evaluation Sheet
##  Week One

**Student Name:** ________________________  
**Date:** ________________________  
**Instructor:** ________________________  
**Score:** _____ / 100

---

## Instructions

This evaluation sheet contains a series of hands-on practical tasks that students must complete sequentially in the Linux terminal. The instructor should observe each task, verify the student's understanding, and record observations. Students should complete each task and demonstrate their work to the instructor before moving to the next task.

---

## SECTION 1: SHELL NAVIGATION & ORIENTATION

### Task 1.1: Determine Current Location
**Objective:** Student demonstrates understanding of current working directory.

**Task:** Execute the command to display your current working directory.

**Command to execute:**
```bash
pwd
```

**Expected output:** A file path showing the current directory (e.g., `/home/ubuntu`)

**Observation Checklist:**
- [ ] Student knows the correct command
- [ ] Student executes command correctly
- [ ] Student can explain what pwd means
- [ ] Student understands the output

**Student's output:**
```
_________________________________________________________________
```

**Instructor Notes:**
```
_________________________________________________________________
_________________________________________________________________
```

---

### Task 1.2: List Directory Contents
**Objective:** Student can list files and directories in the current location.

**Task:** Execute the command to list all files and directories in your current location.

**Command to execute:**
```bash
ls
```

**Expected output:** A list of files and folders in the current directory

**Observation Checklist:**
- [ ] Student executes command correctly
- [ ] Student can identify files vs. directories
- [ ] Student understands the output format

**Student's output:**
```
_________________________________________________________________
_________________________________________________________________
```

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 1.3: Detailed File Listing
**Objective:** Student can display detailed file information including permissions and ownership.

**Task:** Execute the command to list files with detailed information (long format).

**Command to execute:**
```bash
ls -l
```

**Expected output:** Detailed listing with permissions, owner, group, size, date, and filename

**Observation Checklist:**
- [ ] Student executes command correctly
- [ ] Student can identify the permissions column
- [ ] Student can identify the owner column
- [ ] Student can identify the file size column
- [ ] Student can identify the date modified column
- [ ] Student can identify the filename column

**Sample output interpretation:**
```
-rwxr-xr-- 1 student staff 4096 Jan 29 10:30 evidence.txt
```

**Questions for student:**
1. What are the permissions for the owner? _______________
2. What are the permissions for the group? _______________
3. Who is the owner of this file? _______________
4. What is the file size? _______________

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 1.4: Navigate to Home Directory
**Objective:** Student understands how to navigate using relative paths.

**Task:** Navigate to your home directory using the tilde (~) shortcut.

**Command to execute:**
```bash
cd ~
```

**Verification command:**
```bash
pwd
```

**Expected output:** `/home/ubuntu` or similar home directory path

**Observation Checklist:**
- [ ] Student knows the ~ shortcut
- [ ] Student executes navigation correctly
- [ ] Student verifies location with pwd

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 1.5: Navigate Using Absolute Path
**Objective:** Student can navigate using absolute paths.

**Task:** Navigate to the `/tmp` directory using its absolute path.

**Command to execute:**
```bash
cd /tmp
```

**Verification command:**
```bash
pwd
```

**Expected output:** `/tmp`

**Observation Checklist:**
- [ ] Student understands absolute path concept
- [ ] Student executes navigation correctly
- [ ] Student verifies location

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 1.6: Navigate to Parent Directory
**Objective:** Student can navigate using relative path notation.

**Task:** Navigate to the parent directory using the `..` notation.

**Command to execute:**
```bash
cd ..
```

**Verification command:**
```bash
pwd
```

**Expected output:** `/` (root directory)

**Observation Checklist:**
- [ ] Student understands .. notation
- [ ] Student executes navigation correctly
- [ ] Student verifies location

**Instructor Notes:**
```
_________________________________________________________________
```

---

## SECTION 2: DIRECTORY CREATION

### Task 2.1: Create Single Directory
**Objective:** Student can create a new directory.

**Task:** Create a directory named `investigation_case_001` in your home directory.

**Commands to execute:**
```bash
cd ~
mkdir investigation_case_001
ls -l
```

**Expected output:** Directory `investigation_case_001` appears in the listing

**Observation Checklist:**
- [ ] Student knows mkdir command
- [ ] Student creates directory with correct name
- [ ] Student verifies creation with ls
- [ ] Directory appears in listing

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 2.2: Create Nested Directories
**Objective:** Student can create multiple nested directories.

**Task:** Create a nested directory structure: `evidence/forensics/digital_artifacts`

**Commands to execute:**
```bash
cd ~/investigation_case_001
mkdir -p evidence/forensics/digital_artifacts
ls -R
```

**Expected output:** Nested directory structure is created

**Observation Checklist:**
- [ ] Student knows -p flag for nested creation
- [ ] Student creates correct directory structure
- [ ] Student verifies with ls -R
- [ ] Student understands recursive listing

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 2.3: Navigate to Nested Directory
**Objective:** Student can navigate through nested directories.

**Task:** Navigate to the `digital_artifacts` directory and verify your location.

**Commands to execute:**
```bash
cd ~/investigation_case_001/evidence/forensics/digital_artifacts
pwd
```

**Expected output:** Full path to digital_artifacts directory

**Observation Checklist:**
- [ ] Student navigates correctly
- [ ] Student verifies location with pwd
- [ ] Student understands path structure

**Instructor Notes:**
```
_________________________________________________________________
```

---

## SECTION 3: FILE CREATION

### Task 3.1: Create File with Text Editor (Leafpad)
**Objective:** Student can create and edit files using a text editor.

**Task:** Create a file named `case_notes.txt` with the following content:
```
Case ID: CASE-001
Date: January 29, 2026
Investigator: [Student Name]
Status: Initial Investigation
```

**Commands to execute:**
```bash
cd ~/investigation_case_001
leafpad case_notes.txt
```

**Instructions for student:**
1. Type the content above
2. Save the file (File > Save or Ctrl+S)
3. Close the editor

**Verification command:**
```bash
cat case_notes.txt
```

**Observation Checklist:**
- [ ] Student opens text editor correctly
- [ ] Student types content accurately
- [ ] Student saves file correctly
- [ ] File content displays with cat command
- [ ] Student understands file creation process

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 3.2: Create File with Nano Editor
**Objective:** Student can create files using nano editor (command-line alternative).

**Task:** Create a file named `evidence_log.txt` using nano editor.

**Commands to execute:**
```bash
nano evidence_log.txt
```

**Instructions for student:**
1. Type: `Evidence Log - Case 001`
2. Press Enter
3. Type: `Item 1: Hard Drive - Serial #ABC123`
4. Press Ctrl+O to save
5. Press Enter to confirm filename
6. Press Ctrl+X to exit

**Verification command:**
```bash
cat evidence_log.txt
```

**Observation Checklist:**
- [ ] Student opens nano correctly
- [ ] Student types content
- [ ] Student saves with Ctrl+O
- [ ] Student exits with Ctrl+X
- [ ] File is created successfully

**Instructor Notes:**
```
_________________________________________________________________
```

---

## SECTION 4: FILE OPERATIONS - COPY

### Task 4.1: Copy File in Same Directory
**Objective:** Student can duplicate files.

**Task:** Create a backup copy of `case_notes.txt` named `case_notes_backup.txt`

**Commands to execute:**
```bash
cp case_notes.txt case_notes_backup.txt
ls -l case_notes*
```

**Expected output:** Both files appear in listing with same content

**Verification command:**
```bash
cat case_notes_backup.txt
```

**Observation Checklist:**
- [ ] Student knows cp command syntax
- [ ] Student creates backup with correct name
- [ ] Student verifies both files exist
- [ ] Content is identical

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 4.2: Copy File to Different Directory
**Objective:** Student can copy files to other directories.

**Task:** Copy `case_notes.txt` to the `evidence/forensics/` directory

**Commands to execute:**
```bash
cp case_notes.txt evidence/forensics/case_notes.txt
ls -l evidence/forensics/
```

**Expected output:** File appears in the destination directory

**Observation Checklist:**
- [ ] Student specifies destination path correctly
- [ ] File is copied successfully
- [ ] Student verifies with ls

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 4.3: Copy Directory Recursively
**Objective:** Student can copy entire directory structures.

**Task:** Create a backup of the entire `evidence` directory named `evidence_backup`

**Commands to execute:**
```bash
cp -r evidence evidence_backup
ls -R evidence_backup
```

**Expected output:** Complete directory structure is copied

**Observation Checklist:**
- [ ] Student knows -r flag for recursive copy
- [ ] Student specifies source and destination correctly
- [ ] Entire directory structure is copied
- [ ] Student verifies with ls -R

**Instructor Notes:**
```
_________________________________________________________________
```

---

## SECTION 5: FILE OPERATIONS - RENAME/MOVE

### Task 5.1: Rename File
**Objective:** Student can rename files using mv command.

**Task:** Rename `evidence_log.txt` to `evidence_log_v1.txt`

**Commands to execute:**
```bash
mv evidence_log.txt evidence_log_v1.txt
ls -l evidence_log*
```

**Expected output:** File appears with new name

**Observation Checklist:**
- [ ] Student knows mv command for renaming
- [ ] Student specifies old and new names correctly
- [ ] File is renamed successfully
- [ ] Student verifies with ls

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 5.2: Move File to Different Directory
**Objective:** Student can move files between directories.

**Task:** Move `evidence_log_v1.txt` to the `evidence/` directory

**Commands to execute:**
```bash
mv evidence_log_v1.txt evidence/
ls -l evidence/
```

**Expected output:** File appears in destination directory

**Observation Checklist:**
- [ ] Student specifies destination path correctly
- [ ] File is moved (not copied)
- [ ] File no longer exists in original location
- [ ] File appears in destination

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 5.3: Rename Directory
**Objective:** Student can rename directories.

**Task:** Rename `evidence_backup` directory to `evidence_backup_v1`

**Commands to execute:**
```bash
mv evidence_backup evidence_backup_v1
ls -d evidence*
```

**Expected output:** Directory appears with new name

**Observation Checklist:**
- [ ] Student can rename directories
- [ ] Directory is renamed successfully
- [ ] Student verifies with ls

**Instructor Notes:**
```
_________________________________________________________________
```

---

## SECTION 6: FILE OPERATIONS - DELETE

### Task 6.1: Delete Single File
**Objective:** Student can remove files safely.

**Task:** Delete the `case_notes_backup.txt` file

**Commands to execute:**
```bash
rm case_notes_backup.txt
ls -l case_notes*
```

**Expected output:** Only `case_notes.txt` remains

**Observation Checklist:**
- [ ] Student knows rm command
- [ ] Student specifies correct filename
- [ ] File is deleted
- [ ] Student verifies deletion

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 6.2: Delete Directory Recursively
**Objective:** Student can remove directories and contents.

**Task:** Delete the `evidence_backup_v1` directory and all its contents

**Commands to execute:**
```bash
rm -r evidence_backup_v1
ls -d evidence*
```

**Expected output:** Directory no longer appears in listing

**Observation Checklist:**
- [ ] Student knows -r flag for recursive deletion
- [ ] Student specifies correct directory name
- [ ] Directory and all contents are deleted
- [ ] Student verifies deletion

**Instructor Notes:**
```
_________________________________________________________________
```

---

## SECTION 7: FILE CONTENT VIEWING & SEARCHING

### Task 7.1: View File Contents
**Objective:** Student can display file contents.

**Task:** Display the contents of `case_notes.txt`

**Command to execute:**
```bash
cat case_notes.txt
```

**Expected output:** Full file contents displayed

**Observation Checklist:**
- [ ] Student knows cat command
- [ ] Student specifies correct filename
- [ ] Full contents are displayed
- [ ] Student understands output

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 7.2: Search for Text in File
**Objective:** Student can search for specific text within files.

**Task:** Search for the word "Investigation" in `case_notes.txt`

**Command to execute:**
```bash
grep "Investigation" case_notes.txt
```

**Expected output:** Line(s) containing "Investigation" are displayed

**Observation Checklist:**
- [ ] Student knows grep command
- [ ] Student specifies search term correctly
- [ ] Student specifies filename
- [ ] Matching lines are displayed

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 7.3: Search with Line Numbers
**Objective:** Student can display line numbers with search results.

**Task:** Search for "Case" in `case_notes.txt` and display line numbers

**Command to execute:**
```bash
grep -n "Case" case_notes.txt
```

**Expected output:** Matching lines with line numbers

**Observation Checklist:**
- [ ] Student knows -n flag
- [ ] Student understands line number output
- [ ] Correct lines are identified

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 7.4: Search Multiple Files
**Objective:** Student can search across multiple files.

**Task:** Search for "Case" in all `.txt` files in current directory

**Commands to execute:**
```bash
grep -l "Case" *.txt
```

**Expected output:** Filenames containing "Case"

**Observation Checklist:**
- [ ] Student knows -l flag (list filenames)
- [ ] Student uses wildcard pattern correctly
- [ ] Correct filenames are displayed

**Instructor Notes:**
```
_________________________________________________________________
```

---

## SECTION 8: NETWORKING COMMANDS

### Task 8.1: Test Network Connection (Ping Domain)
**Objective:** Student can test network connectivity using domain names.

**Task:** Test network connection to google.com

**Command to execute:**
```bash
ping -c 4 google.com
```

**Expected output:** PING statistics showing successful connection

**Observation Checklist:**
- [ ] Student knows ping command
- [ ] Student specifies domain correctly
- [ ] Student uses -c flag to limit packets
- [ ] Student interprets results

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 8.2: Test Network Connection (Ping IP)
**Objective:** Student can test network connectivity using IP addresses.

**Task:** Test network connection to 8.8.8.8 (Google DNS)

**Command to execute:**
```bash
ping -c 4 8.8.8.8
```

**Expected output:** PING statistics showing successful connection

**Observation Checklist:**
- [ ] Student specifies IP address correctly
- [ ] Student uses -c flag
- [ ] Student interprets results

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 8.3: List Open TCP Ports
**Objective:** Student can identify listening network ports.

**Task:** Display all listening TCP ports on the system

**Command to execute:**
```bash
netstat -lnt
```

**Expected output:** Table showing listening ports, local addresses, and states

**Observation Checklist:**
- [ ] Student knows netstat command
- [ ] Student knows -lnt flags:
  - [ ] -l (listening)
  - [ ] -n (numeric - don't resolve names)
  - [ ] -t (TCP)
- [ ] Student can interpret output
- [ ] Student identifies SSH port (22)

**Questions for student:**
1. What port is SSH listening on? _______________
2. What does "LISTEN" state mean? _______________
3. What is the local address 0.0.0.0:* mean? _______________

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 8.4: Download File from Internet
**Objective:** Student can download files using wget.

**Task:** Download a small file from the internet using wget

**Command to execute:**
```bash
wget https://www.w3.org/WAI/WCAG21/Techniques/pdf/img/logo.png -O downloaded_logo.png
ls -l downloaded_logo.png
```

**Expected output:** File is downloaded and appears in directory listing

**Observation Checklist:**
- [ ] Student knows wget command
- [ ] Student specifies URL correctly
- [ ] Student uses -O flag to specify output filename
- [ ] File is downloaded successfully
- [ ] Student verifies with ls

**Instructor Notes:**
```
_________________________________________________________________
```

---

## SECTION 9: FILE PERMISSIONS & OWNERSHIP

### Task 9.1: Understand Permission Notation
**Objective:** Student can interpret file permissions.

**Task:** Display detailed listing and interpret permissions

**Command to execute:**
```bash
ls -l case_notes.txt
```

**Expected output:** Example: `-rw-r--r-- 1 ubuntu ubuntu 256 Jan 29 10:30 case_notes.txt`

**Permission Analysis:**

| Position | Symbol | Meaning |
|----------|--------|---------|
| 1 | - | Regular file |
| 2-4 | rw- | Owner: read, write, no execute |
| 5-7 | r-- | Group: read only |
| 8-10 | r-- | Others: read only |

**Questions for student:**
1. What is the file type? _______________
2. What permissions does the owner have? _______________
3. What permissions does the group have? _______________
4. What permissions do others have? _______________
5. Who is the owner? _______________
6. What is the group? _______________

**Observation Checklist:**
- [ ] Student can read permission string
- [ ] Student identifies file type
- [ ] Student identifies owner permissions
- [ ] Student identifies group permissions
- [ ] Student identifies other permissions

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 9.2: Change File Permissions
**Objective:** Student can modify file permissions.

**Task:** Change `case_notes.txt` permissions to read-only for owner (400)

**Commands to execute:**
```bash
chmod 400 case_notes.txt
ls -l case_notes.txt
```

**Expected output:** Permissions change to `-r--------`

**Observation Checklist:**
- [ ] Student knows chmod command
- [ ] Student understands permission numbers:
  - [ ] 4 = read
  - [ ] 2 = write
  - [ ] 1 = execute
- [ ] Student applies permissions correctly
- [ ] Student verifies with ls

**Instructor Notes:**
```
_________________________________________________________________
```

---

### Task 9.3: Restore File Permissions
**Objective:** Student can restore standard permissions.

**Task:** Change `case_notes.txt` permissions back to standard (644)

**Commands to execute:**
```bash
chmod 644 case_notes.txt
ls -l case_notes.txt
```

**Expected output:** Permissions change to `-rw-r--r--`

**Observation Checklist:**
- [ ] Student applies correct permissions
- [ ] Student verifies with ls

**Instructor Notes:**
```
_________________________________________________________________
```

---

## SECTION 10: COMPREHENSIVE SCENARIO

### Task 10.1: Digital Forensics Investigation Scenario
**Objective:** Student applies all learned skills in a realistic scenario.

**Scenario:** You are a cybercrime investigator who has gained access to a compromised system. You need to:
1. Determine your current location
2. Navigate to the evidence directory
3. Create a new case folder
4. Document findings
5. Search for suspicious files
6. Check network activity
7. Backup evidence

**Step-by-step tasks:**

**Step 1:** Determine current location and list contents
```bash
pwd
ls -l
```

**Step 2:** Navigate to evidence directory
```bash
cd ~/investigation_case_001/evidence
pwd
```

**Step 3:** Create new case subfolder
```bash
mkdir case_2026_001
cd case_2026_001
```

**Step 4:** Create investigation report
```bash
nano investigation_report.txt
```
(Type: Investigation started on January 29, 2026)

**Step 5:** Search for files containing "suspicious"
```bash
grep -r "suspicious" ~/investigation_case_001
```

**Step 6:** Check network ports
```bash
netstat -lnt | grep LISTEN
```

**Step 7:** Create backup of case
```bash
cd ~/investigation_case_001
cp -r evidence evidence_backup_final
ls -R evidence_backup_final
```

**Observation Checklist:**
- [ ] Student navigates correctly
- [ ] Student creates directories
- [ ] Student creates documentation
- [ ] Student searches files
- [ ] Student checks network info
- [ ] Student creates backup
- [ ] Student demonstrates understanding of all commands

**Instructor Notes:**
```
_________________________________________________________________
_________________________________________________________________
```

---

## EVALUATION SUMMARY

| Section | Tasks | Status | Comments |
|---------|-------|--------|----------|
| 1. Navigation | 1.1-1.6 | [ ] Pass [ ] Fail | |
| 2. Directory Creation | 2.1-2.3 | [ ] Pass [ ] Fail | |
| 3. File Creation | 3.1-3.2 | [ ] Pass [ ] Fail | |
| 4. Copy Operations | 4.1-4.3 | [ ] Pass [ ] Fail | |
| 5. Rename/Move | 5.1-5.3 | [ ] Pass [ ] Fail | |
| 6. Delete Operations | 6.1-6.2 | [ ] Pass [ ] Fail | |
| 7. View & Search | 7.1-7.4 | [ ] Pass [ ] Fail | |
| 8. Networking | 8.1-8.4 | [ ] Pass [ ] Fail | |
| 9. Permissions | 9.1-9.3 | [ ] Pass [ ] Fail | |
| 10. Scenario | 10.1 | [ ] Pass [ ] Fail | |

---

## Overall Assessment

**Total Score:** _____ / 100

**Strengths:**
```
_________________________________________________________________
_________________________________________________________________
```

**Areas for Improvement:**
```
_________________________________________________________________
_________________________________________________________________
```

**Recommendations:**
```
_________________________________________________________________
_________________________________________________________________
```

**Instructor Signature:** ________________________  
**Date:** ________________________

---

## Notes for Instructors

This evaluation sheet is designed to be completed over one or more training sessions. Each task should be demonstrated by the student with the instructor observing and recording observations. The student should be able to explain what each command does and why they are using it.

For  training, emphasize:
- The importance of understanding file permissions for evidence preservation
- How to safely navigate and examine systems without altering evidence
- The role of networking commands in identifying suspicious activity
- Proper documentation and backup procedures for forensic evidence
