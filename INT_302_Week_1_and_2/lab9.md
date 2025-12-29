
## **INT302: Kali Linux Tools and System Security – Lab 9: Information Gathering with Shodan**

---

### **Lab Overview**

In this lab, participants will learn how to use **Shodan**, a powerful search engine for internet-connected devices, to discover exposed systems, services, and potential security risks. The lab provides hands-on experience in identifying publicly accessible infrastructure and understanding the external attack surface of organizations.

---

### **Lab Objectives**

By the end of this lab, you will be able to:

1. Understand how Shodan indexes internet-connected devices.
2. Configure and use the Shodan CLI in Kali Linux.
3. Discover exposed services, ports, and devices using Shodan queries.
4. Analyze and document findings for security assessments.

---

### **Tool Used**

* **Shodan**: A search engine that identifies internet-connected devices, services, and systems using banners, ports, and metadata.

---

### **Prerequisites**

* Basic understanding of reconnaissance and information gathering.
* Familiarity with Linux command-line operations.
* Internet access.

---

## **Lab Steps**

---

### **Step 1: Setting Up Shodan**

1. **Create a Shodan Account**

   * Visit the Shodan website and create an account.
   * Obtain your **Shodan API key** from your account dashboard.

2. **Install Shodan CLI** (if not already installed):

   ```bash
   pip install shodan
   ```

3. **Configure Shodan with Your API Key**:

   ```bash
   shodan init <YOUR_API_KEY>
   ```

**Exercise 1:**

* Verify that Shodan is correctly configured by running:

  ```bash
  shodan info
  ```
* Record your API plan and query limits. __________

---

### **Step 2: Basic Shodan Searches**

1. **Search by Domain or Organization Name**:

   ```bash
   shodan search example.com
   ```

2. **Search by IP Address**:

   ```bash
   shodan host <IP_ADDRESS>
   ```

**Exercise 2:**

* What information does Shodan reveal about the target (open ports, services, banners)? __________

---

### **Step 3: Service and Port Enumeration**

1. **Search for Specific Services**:

   ```bash
   shodan search port:22
   ```

2. **Search for Web Servers**:

   ```bash
   shodan search port:80
   ```

3. **Search for Databases Exposed to the Internet**:

   ```bash
   shodan search port:3306
   ```

**Exercise 3:**

* Identify at least two services exposed on the internet and explain why they could pose a security risk. __________

---

### **Step 4: Advanced Shodan Queries**

1. **Country-Based Search**:

   ```bash
   shodan search country:NG
   ```

2. **Filter by Organization**:

   ```bash
   shodan search org:"Organization Name"
   ```

3. **Multiple Filters Combined**:

   ```bash
   shodan search port:443 country:US
   ```

**Exercise 4:**

* Perform a search using at least two filters. Document the devices and services discovered. __________

---

### **Step 5: Identifying Security Exposure**

1. **Search for Commonly Exposed Devices**:

   * Routers
   * CCTV cameras
   * Industrial control systems (ICS)
   * IoT devices

   Example:

   ```bash
   shodan search "webcam"
   ```

2. **Analyze Service Banners**

   * Review version numbers.
   * Identify outdated or vulnerable software.

**Exercise 5:**

* Identify one potentially vulnerable system and explain why it may be at risk. __________

---

### **Step 6: Reporting and Analysis**

1. **Document Findings**

   * Target searched
   * Query used
   * Services discovered
   * Potential security implications

2. **Ethical Consideration**

   * Discuss why Shodan should only be used for **defensive security, research, and authorized assessments**.

**Exercise 6:**

* Explain how Shodan findings can be useful during a penetration testing or blue team engagement. __________

---

### **Conclusion**

In this lab, you gained practical experience using **Shodan** to discover internet-exposed systems and services. You learned how attackers and defenders alike can use publicly available data to understand an organization’s external attack surface and improve security posture.

