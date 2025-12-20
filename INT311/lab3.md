

## **INT311 - Basic Computer Skills for Digital Forensics – Lab 3**

### **Lab Title:**  
**Exploring the Windows File System, Networking, and Batch Scripting**

---

### **Objective:**
This lab aims to provide students with practical experience in managing files and folders in the Windows operating system, understanding networking functionalities, and creating and executing batch files. By completing this lab, students will enhance their file management skills and learn how to automate tasks using batch scripts, alongside foundational networking commands.

---

### **Part 1: Create Folders and Files**

1. **Folder Creation:**
   - Create a new folder named **`workspace4`** on your desktop.
   
   **Task:**
   - Verify that the folder has been created successfully.

2. **File Creation:**
   - Inside the **`workspace4`** folder, create three text files:
     - **`file1.txt`**
     - **`file2.txt`**
     - **`file3.txt`**

   **Task:**
   - Open each text file and write a brief description of its purpose. Save and close the files.

---

### **Part 2: File Copy & Deletion**

1. **File Copying:**
   - Copy **`file1.txt`** and **`file2.txt`** to the **`workspace4`** folder.

   **Task:**
   - Confirm that the files have been copied correctly.

2. **File Deletion:**
   - Delete **`file3.txt`** from the **`workspace4`** folder.

   **Task:**
   - Ensure that the file has been deleted and does not appear in the folder.

---

### **Part 3: Networking and Searching for Information**

1. **Networking Commands:**
   - Use the following commands in the Command Prompt to gather information about your network:
- **

```bash
ipconfig
```

- **

```bash
ping www.google.com
```

     - **`tracert www.google.com`**: Trace the route packets take to reach Google.
- **

```bash
netstat -a
```


   **Task:**
   - Document the output of each command and explain what information you gathered.

2. **Network Access:**
   - Access a shared network folder (if available) or create a simple text file within your local network that can be accessed by another user.

   **Task:**
   - Describe how you accessed the network folder and any challenges encountered.

3. **Searching for Information:**
- Use the Windows search feature to locate all

```bash
.txt
```


   **Task:**
   - List the steps you took to perform the search and the results obtained.

---

### **Part 4: Creating a Batch File**

1. **Batch File Creation:**
   - Create a batch file named **`sys_info.bat`** with the following content:
   ```bat
   @echo off
   echo System Information:
   systeminfo
   pause
   ```

   **Task:**
   - Save the batch file in the **`workspace4`** folder.

2. **Making the Batch File Callable:**
   - To make **`sys_info.bat`** callable from any folder, follow these steps:

   a. **Create a new folder** to store batch files (if not already done), e.g., **`C:\Scripts`**.
   
   b. **Copy** the **`sys_info.bat`** file from **`workspace4`** to **`C:\Scripts`**.

   c. **Modify the Path Variable:**
   - Add the new folder (**`C:\Scripts`**) to the system PATH environment variable:
     - Right-click on **This PC** or **Computer** and select **Properties**.
     - Click on **Advanced system settings**.
     - In the **System Properties** window, click on the **Environment Variables** button.
     - In the **System variables** section, find and select the **Path** variable, then click **Edit**.
     - Click **New** and add **`C:\Scripts`** to the list.
     - Click **OK** to save the changes.

   **Task:**
   - Confirm that the path has been successfully modified.

3. **Executing the Batch File:**
   - Open the Command Prompt and type **`sys_info.bat`** from any folder.

   **Task:**
   - Document the output you receive and verify that the batch file executed successfully.

---

### **Submission Requirements:**

- Submit a PDF document containing:
  - Screenshots of each step taken in the lab (folder and file creation, file copying, deletion, batch file creation, and execution).
  - A brief explanation of each task performed, including any challenges faced and how they were overcome.

- Ensure your document is organized, clearly labeled, and includes your name and student ID at the top.

---

### **Grading Criteria:**

- **Correctness:** Accuracy of folder and file creation, copying, deletion, and batch file execution.
- **Clarity:** Clear explanations and documentation of the process.
- **Depth:** Thoroughness of explanations regarding the steps taken and any challenges encountered.
- **Documentation:** Professional presentation of findings with appropriate screenshots and organization.

---

### **Important Notes:**

- This lab is designed to enhance your understanding of file management in the Windows environment and to give you hands-on experience with batch scripting and networking commands.
- Be sure to explore the potential of batch files to automate other tasks in the future!

---

Good luck!