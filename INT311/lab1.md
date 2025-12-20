


## **INT311 - Basic Computer Skills for Digital Forensics – Lab 1**

### **Lab Title:**  
**Foundational Concepts: Number Systems, Date Formats, ASCII Codes, Disk Drives, and Computer Forensics**

---

### **Objective:**
This lab will introduce you to essential concepts in digital forensics, including number system conversions, date formats, ASCII code understanding, disk drive structure, file systems, and basic system verification using Linux commands. By the end of this lab, you will have a deeper understanding of the low-level operations of computers, which are crucial for digital forensics.

---

### **Part 1: Number Systems and Conversion**

1. **Binary to Decimal Conversion:**
   - Convert the binary number `1010111101` to its decimal equivalent.
   - **Hint:** Use the positional value method to calculate the decimal equivalent of the binary number.
   
   **Question:**  
Explain the step-by-step process of converting a binary number to decimal. Provide another binary number (

```bash
11011011
```


2. **Hexadecimal Conversions:**
   - Convert the hexadecimal number `0xABCD` to its decimal equivalent.
   
   **Question:**  
   Discuss the importance of hexadecimal notation in computing. Provide an example where hexadecimal notation is advantageous over decimal (e.g., in memory addressing or representing RGB color values).

---

### **Part 2: Date Formats and Conversion**

1. **Unix Timestamp Conversion:**
   - Convert the Unix timestamp `1626258000` to a human-readable date format (in UTC).
   - **Hint:** You can use an online converter, a Python script, or a Linux command (`date`).
   
   **Question:**  
   Describe the Unix epoch and its significance in computing time.

2. **Date Format Differences:**
   - Explain the differences between the date formats `MM/DD/YYYY` and `YYYY-MM-DD`.
   
   **Question:**  
   When would you use each format in programming and why? Consider regional differences, programming standards, and sorting functionality in databases.

---

### **Part 3: ASCII Code Understanding**

1. **ASCII Table Creation:**
   - Create a table listing the ASCII codes for characters `A`, `B`, `C`, `a`, `b`, `c`.

2. **Python ASCII Code Conversion:**
   - Write a Python script that converts ASCII codes to characters and vice versa for the characters listed above.
   
   **Example Code Snippet:**
   ```python
   # Convert characters to ASCII codes
   ascii_values = {char: ord(char) for char in ['A', 'B', 'C', 'a', 'b', 'c']}
   print(ascii_values)

   # Convert ASCII codes back to characters
   characters = {value: chr(value) for value in ascii_values.values()}
   print(characters)
   ```

3. **Extended ASCII Codes:**
   - Research and list ASCII codes for extended characters beyond the standard English alphabet (e.g., symbols or foreign language characters).
   
   **Question:**  
   Explain how extended ASCII characters are used in computing, such as encoding special symbols in file names or supporting internationalization.

---

### **Part 4: Disk Drives and File Systems**

1. **Disk Geometry Calculations:**
   - Given the following disk parameters:
     - Sectors per track: `400`
     - Number of heads: `12`
     - Cylinders: `17,000`
   
   **Tasks:**  
   a. Calculate the total number of sectors in the disk.  
   b. Discuss how disk geometry impacts disk performance and storage capacity.

2. **File Systems Overview:**
   - **Question:**  
   Describe the structure and functionality of a file system. Compare and contrast different types of file systems used in modern operating systems, such as FAT32, NTFS, and EXT4.
   
   **Discussion Point:**  
   Highlight their advantages and disadvantages, such as speed, security, and compatibility.

---

### **Part 5: Computer Forensics and System Verification**

1. **System Verification Using Linux Commands:**
- Use Linux commands (

```bash
lscpu
```

   
   **Task:**  
   Document the verification process step-by-step, detailing the commands used and the output observed. Include screenshots if possible.

2. **Challenges in Computer Forensics:**
   - **Question:**  
   Discuss why computer forensics can be challenging. Focus on topics like data recovery (deleted files, overwritten data), integrity verification (ensuring data hasn’t been tampered with), and legal implications (e.g., maintaining chain of custody).

3. **Forensic Tools and Techniques:**
   - **Question:**  
   Provide examples of tools (e.g., Autopsy, FTK Imager) and techniques (e.g., file carving, memory analysis) used in computer forensics to overcome the challenges mentioned above.

---

### **Submission Requirements:**

- Submit a PDF file containing:
  - Answers to all questions and discussions.
  - Python code snippets for the ASCII conversion task.
  - Step-by-step documentation of your system verification process with screenshots.
  
- Ensure that your file is well-organized and includes your name and student ID at the top of the document.

---

### **Grading Criteria:**

- **Correctness:** Accuracy of answers and calculations.
- **Clarity:** Well-explained processes and justifications.
- **Code:** Proper functioning of Python scripts.
- **Research:** Depth of research in explaining technical concepts.
- **Documentation:** Thorough and clear documentation of system verification steps.

---

### **Important Notes:**

- This lab is designed to strengthen your understanding of fundamental computer operations and their relevance to digital forensics.
- Feel free to experiment and explore beyond the lab instructions to deepen your knowledge. However, ensure that all required tasks are completed for submission.

---

Good luck!