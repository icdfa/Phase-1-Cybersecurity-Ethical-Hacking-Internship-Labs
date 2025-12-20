

## **INT313 - Computer and Digital Forensics – Lab 3**

### **Lab Title:**  
**Disk Imaging Techniques: Acquisition Methods for USB Drives**

---

### **Objective:**
This lab aims to provide students with a comprehensive understanding of disk images and the techniques used to acquire USB drives in both Windows and Linux environments. By the end of this lab, students will have hands-on experience using FTK Imager and the `dd` command for forensic imaging.

---

### **Part 1: Understanding Disk Images**

1. **What is a Disk Image?**
   - Define a disk image and its importance in digital forensics.
   - **Deliverable:** Write a brief explanation (100-150 words) discussing the purpose and benefits of creating disk images in forensic investigations.

---

### **Part 2: Acquisition of USB Drives**

#### **Task 1: Acquisition Using FTK Imager (Windows)**

1. **Setup FTK Imager:**
   - Download and install FTK Imager from the official website.

2. **Create a Disk Image:**
   - **Step 1:** Connect your USB flash drive to the Windows machine.
   - **Step 2:** Open FTK Imager and select `File > Create Disk Image`.
   - **Step 3:** Choose the connected USB drive from the list of available drives.
   - **Step 4:** Select the output format (e.g., E01 or RAW) and specify a destination for the image file.
   - **Step 5:** Click `Finish` to create the disk image.

3. **Deliverable:** Capture screenshots of each step in FTK Imager, including the final image file location.

---

#### **Task 2: Acquisition Using `dd` Command (Linux)**

1. **Setup Linux Environment:**
   - Use a Linux distribution (e.g., Ubuntu) and connect your USB flash drive.

2. **Create a Disk Image:**
- **Step 1:** Identify the USB drive using the

```bash
lsblk
```

   - **Step 2:** Use the `dd` command to create a disk image. Replace `/dev/sdX` with the correct identifier for your USB drive.
     ```bash
     sudo dd if=/dev/sdX of=~/usb_image.img bs=4M status=progress
     ```
   - **Step 3:** Wait for the process to complete. This may take some time depending on the size of the USB drive.

3. **Deliverable:** Document the command used and capture a screenshot of the terminal output showing the image creation progress.

---

#### **Task 3: Acquisition via Network**

1. **Network Imaging:**
   - Discuss the concept of acquiring disk images over a network.
- **Note:** In this lab, students will not perform network acquisition, but will learn about tools like

```bash
FTK Imager
```

   - **Deliverable:** Write a short paragraph (100 words) on the advantages and challenges of acquiring disk images via network methods.

---

### **Part 3: Forensic Research Preparation**

1. **Forensic Research USB Flash Drive:**
   - **Important Note:** Each student is encouraged to purchase a small USB flash drive specifically for forensic research.
   - **Deliverable:** Prepare a plan on how to use the USB drive for future forensic exercises, including potential experiments or imaging tasks.

---

### **Submission Requirements:**

- Submit a PDF file containing:
  - Your definition of a disk image.
  - Screenshots from the FTK Imager acquisition process.
- Documentation and screenshots from the

```bash
dd
```

  - Summary of network imaging methods.
  - Your forensic research plan for the USB flash drive.

---

### **Grading Criteria:**

- **Correctness:** Accuracy of commands executed and images acquired.
- **Clarity:** Clear explanations of the process and techniques used.
- **Documentation:** Thorough documentation of steps taken, including screenshots.
- **Presentation:** Well-organized submission with proper formatting.

---

### **Important Notes:**

- Ensure you follow best practices for handling and imaging forensic evidence.
- This lab is designed to provide hands-on experience with disk imaging techniques crucial for digital forensics investigations.

---

Good luck with your lab!