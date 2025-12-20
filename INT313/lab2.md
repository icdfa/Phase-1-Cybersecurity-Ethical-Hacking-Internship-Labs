

## **INT313 - Computer and Digital Forensics – Lab 2**

### **Lab Title:**  
**Comparative Analysis of Autopsy and The Sleuth Kit (TSK)**

---

### **Objective:**
This lab aims to familiarize students with the differences between Autopsy and The Sleuth Kit (TSK), understand the architecture of TSK, and perform a practical examination of a USB drive image using TSK commands to recover deleted files.

---

### **Part 1: Overview of Autopsy and The Sleuth Kit**

1. **Autopsy vs. The Sleuth Kit:**
   - Provide a brief overview of the differences between Autopsy and TSK in terms of functionality and user interface.
   - **Deliverable:** Write a comparison (150-200 words) to include in your lab report.

2. **TSK Architecture:**
   - Research and summarize the layers of the TSK architecture.
   - **Deliverable:** Create a diagram or list showing the layers of TSK and the tools provided at each layer.

---

### **Part 2: Examining a USB File Using TSK**

1. **Setup TSK:**
   - Download the USB drive image from [this link](https://www.dropbox.com/s/nw23q14vzsykyup/Ch01InChap01.dd).

2. **Using TSK Commands:**
   - Follow the PowerPoint presentations provided in class to practice all Linux commands related to The Sleuth Kit.
   - **Task:** Determine how many deleted files are in the disk image.
     - Use the command:
       ```bash
       fls -r Ch01InChap01.dd
       ```

3. **Recovering Deleted Files:**
   - **Task:** Recover the deleted file `letter1.txt` using TSK commands.
   - **Command Example:**
     ```bash
     icat Ch01InChap01.dd <inode_number> > recovered_letter1.txt
     ```
   - **Deliverable:** Document the command used and any relevant outputs.

---

### **Part 3: Demonstrating Recovery Tools**

1. **Recovering Deleted Files:**
- Demonstrate the recovery of all deleted files using three different tools introduced in class (e.g.,

```bash
fls
```

   - **Deliverable:** For each tool, provide:
     - The command used.
     - The inputs required (e.g., URL or custom inputs).
     - The expected outputs.
     - An explanation of how each command works and how its parameters influence the output.

2. **Selecting Questions:**
   - Based on your last four student ID or SSN digits, use the modulus operation to determine which questions to answer. For example, if your last four digits are `1234`, calculate:
     - `1234 mod 28` to get the index for your questions (2, 3, 4).
   - **Deliverable:** Document the selected questions and your responses in the lab report.

---

### **Part 4: Documentation and Screenshots**

1. **Capture and Document:**
   - Capture all screenshots of your terminal output, commands executed, and recovered files.
   - If you used your own inputs for recovery, upload those inputs along with your lab report.

2. **Lab Report Submission:**
   - Submit a PDF file containing:
     - Your comparison of Autopsy and TSK.
     - Overview of TSK architecture.
     - The commands used for recovering deleted files, including inputs, outputs, and explanations.
     - Screenshots of the entire process.
     - Responses to the selected questions.

---

### **Grading Criteria:**

- **Correctness:** Accuracy of commands executed and results obtained.
- **Clarity:** Clear explanations of processes, commands, and outcomes.
- **Documentation:** Thorough documentation of steps, findings, and screenshots.
- **Presentation:** Well-organized submission with proper formatting.

---

### **Important Notes:**

- This lab is designed to provide practical experience with TSK for digital forensics investigations.
- Ensure that you follow the Linux commands introduced in the lecture and do not mount the image during this process.

---

Good luck with your lab!