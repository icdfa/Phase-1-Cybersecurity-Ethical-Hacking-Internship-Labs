

## **INT302: Kali Linux Tools and System Security – Lab 3: Subdomain Hunting**

### **Lab Overview**
In this lab, you will learn how to identify subdomains associated with a target domain using various tools. Subdomain hunting is a crucial part of reconnaissance in penetration testing, as it helps identify additional attack surfaces that may not be immediately visible. We will utilize `sublist3r` for subdomain enumeration, `dirb` for directory discovery, and `KnockPy` for gathering information from public sources.

---

### **Lab Objectives**
By the end of this lab, you will:
1. Perform subdomain enumeration using `sublist3r`.
2. Discover hidden directories on a target web server using `dirb`.
3. Utilize `KnockPy` to gather additional information about the target domain.

---

### **Tools Used**
- **Kali Linux**: A Linux distribution tailored for penetration testing.
- **sublist3r**: A tool designed for subdomain enumeration.
- **dirb**: A web content scanner for discovering hidden directories.
- **KnockPy**: A tool for gathering emails and subdomains from public sources.

---

### **Prerequisites**
- Basic knowledge of Kali Linux and command-line operations.
- Internet access to perform scans on live web servers.
- Tools `sublist3r`, `dirb`, and `KnockPy` installed in your Kali Linux environment (they usually come pre-installed).

---

### **Lab Steps**

#### **Step 1: Subdomain Enumeration Using `sublist3r`**

`sublist3r` is an effective tool for finding subdomains of a target domain.

**Instructions:**
1. Open your **Terminal** in Kali Linux.
2. Use the `sublist3r` command followed by the target domain.

   **Command Syntax**:
   ```bash
   sublist3r -d <target domain>
   ```

   **Example**:
   ```bash
   sublist3r -d example.com
   ```

**Expected Output**:  
The output will display a list of subdomains associated with the specified domain.

#### **Exercise 1**:  
Run the `sublist3r` command for the following domains:
- `github.com`
- `google.com`

**Record Your Findings**:
1. **Subdomains for github.com**:
   - __________
2. **Subdomains for google.com**:
   - __________

---

#### **Step 2: Directory Discovery Using `dirb`**

`dirb` is a powerful tool for discovering hidden directories and files on web servers.

**Instructions:**
1. In the terminal, run the `dirb` command followed by the target URL.

   **Command Syntax**:
   ```bash
   dirb <target URL>
   ```

   **Example**:
   ```bash
   dirb https://example.com
   ```

**Expected Output**:  
The command will return a list of directories and files found on the web server.

#### **Exercise 2**:  
Perform a directory discovery scan on the following targets:
- `http://example.com`
- `http://example.org`

**Record Your Findings**:
1. **Directories for example.com**:
   - __________
2. **Directories for example.org**:
   - __________

---



## **Step 3: Subdomain Enumeration Using `KnockPy`**

`KnockPy` is a reconnaissance tool used for **subdomain enumeration**. It helps identify subdomains associated with a target domain, which is a critical phase in information gathering and attack surface mapping.

### **Objective**

Set up `KnockPy` in a Python virtual environment and use it to enumerate subdomains of a target domain.

---

### **Instructions**

#### **1. Create a Python Virtual Environment**

From your terminal, create and activate a virtual environment to avoid dependency conflicts.

```bash
python3 -m venv knock-env
source knock-env/bin/activate
```

---

#### **2. Clone the KnockPy Repository**

Clone the official KnockPy repository from GitHub.

```bash
git clone https://github.com/guelfoweb/knock.git
cd knock
```

---

#### **3. Upgrade Required Python Tools**

Ensure `pip`, `setuptools`, and `wheel` are up to date.

```bash
pip install --upgrade pip setuptools wheel
```

---

#### **4. Install KnockPy**

Install KnockPy and its dependencies.

```bash
pip install .
```

**If you encounter dependency issues**, run the following commands:

```bash
pip install -r requirements.txt
pip install .
```

---

#### **5. Verify Installation**

Confirm that KnockPy is installed successfully.

```bash
knockpy --version
```

---

#### **6. Run Subdomain Enumeration**

Execute KnockPy against the target domain using reconnaissance mode.

```bash
knockpy -d example.com --recon
```

---

### **Expected Output**

The output will display:

* Discovered subdomains
* IP addresses (if available)
* DNS and reconnaissance-related information for the target domain

---

### **Exercise 3**

Use `KnockPy` to enumerate subdomains for the following domain:

* **Target Domain:** `example.com`

---

### **Record Your Findings**

* **Discovered Subdomains and Information:**

  * ---
  * ---
  * ---

---


### **Submission Instructions**
Submit your results from all exercises, including:
- Detected subdomains from `sublist3r`.
- Discovered directories from `dirb`.
- Information gathered using `KnockPy`.

---

### **Conclusion**
In this lab, you explored techniques for subdomain hunting and directory discovery using various tools. This knowledge is essential for identifying potential vulnerabilities and attack vectors in a target's infrastructure.

---
