
## **INT302: Kali Linux Tools and System Security – Lab 7: IoT & Enterprise Network Forensic Investigation Using Wireshark**

---

### **Lab Overview**

In this lab, participants will conduct a **network forensic investigation** involving **BookWorld**, a major online bookstore. Recently, unusual behavior has been detected in BookWorld's **database activity**, including spikes in query volumes and server resource usage, suggesting the possibility of a **cyberattack**.

You are part of a **Digital Forensics team**. The business is concerned about the **integrity of customer data** and its internal systems. Your mission is to:

* Conduct a thorough forensic analysis of the network traffic
* Identify how the attacker gained access
* Assess the scope of the breach
* Prepare your findings in a comprehensive report

⚠️ **Important Instruction:**
This lab is intentionally designed **without step-by-step filtering hints**. You are expected to **apply the packet analysis, filtering, and pivoting techniques learned in Lab 6** to successfully complete Lab 7.

---

### **Lab Objectives**

By the end of this lab, you will be able to:

1. Analyze enterprise network traffic using advanced forensic techniques.
2. Identify indicators of compromise (IoCs) related to web and database abuse.
3. Apply appropriate Wireshark filtering strategies based on investigative goals.
4. Trace attacker activity from initial access to possible data exfiltration.
5. Produce a professional forensic report documenting findings, timelines, and remediation recommendations.

---

### **Tools Used**

* **Wireshark** – Primary network forensic analysis tool
* **tshark** – Command-line packet analysis
* **NetworkMiner (optional)** – Artifact and credential extraction
* **WHOIS / GeoIP tools** – External IP attribution

---

### **Prerequisites**

* Completion of **Lab 6: Advanced Packet Analysis Techniques**
* Solid understanding of HTTP, TCP/IP, DNS, and database protocols
* Ability to independently construct and apply Wireshark filters
* Access to the provided PCAP file:
  [BookWorld Network Breach PCAP](https://drive.google.com/file/d/1IV_V5weV8jBTqzgzLJxEKM0VjCpB1RmU/view)

---

## **Lab Steps**

---

### **Step 1: Incident Response Analysis**

#### **1. Scenario Setup**

* You are assigned to investigate unusual activity at **BookWorld**.
* Security monitoring detected:

  * Spikes in database query volumes
  * Abnormal server resource usage
  * External IPs interacting with customer database systems

**Mission Objectives:**

* Identify the attacker’s entry point
* Determine affected systems and services
* Assess potential customer data exposure
* Prepare a comprehensive forensic report with evidence

---

#### **2. Initial Traffic Inspection**

1. Open the PCAP file in Wireshark.
2. Set the correct time format (**UTC**).
3. Begin with a **broad inspection of network traffic**.

**Exercise 1:**

* Describe the overall traffic behavior.
* Do you observe repeated connections or unusual communication patterns?
* What early indicators suggest malicious activity?

---

### **Step 2: Identifying Suspicious Hosts**

1. Use Wireshark statistics and conversation analysis features.
2. Identify:

   * External systems communicating excessively with BookWorld servers
   * Internal servers receiving abnormal traffic volumes

**Exercise 2:**

* Identify at least one suspicious external IP address.
* Justify why this IP is considered suspicious based on traffic behavior.

---

### **Step 3: Web and Database Traffic Investigation**

#### **1. Web Application Abuse Analysis**

Attackers often exploit web applications to:

* Abuse authentication mechanisms
* Inject malicious payloads
* Extract sensitive data

**Exercise 3:**

* Identify suspicious web requests.
* Which endpoints or parameters appear abnormal?
* Do you observe patterns consistent with brute-force, enumeration, or data extraction?

---

#### **2. Database Interaction Analysis**

Investigate traffic involving backend data stores.

**Exercise 4:**

* Identify which database services appear to be targeted.
* What traffic patterns suggest enumeration, abuse, or unauthorized access?

---

### **Step 4: DNS and Command-and-Control Analysis**

#### **1. DNS Traffic Inspection**

**Exercise 5:**

* Identify unusual or suspicious domain queries.
* Do any domains appear unrelated to BookWorld operations or algorithmically generated?

---

#### **2. Data Exfiltration Indicators**

Analyze outbound traffic patterns.

**Exercise 6:**

* Is there evidence of large or abnormal data transfers?
* Which protocol or method appears to be used for exfiltration?

---

### **Step 5: Attack Timeline Reconstruction**

1. Identify:

   * Initial access
   * Exploitation phase
   * Data exfiltration phase
2. Use packet timestamps to reconstruct the incident timeline.

**Exercise 7:**

* Reconstruct the attack sequence step by step.
* At what point was customer data most at risk?

---

### **Step 6: Reporting Findings**

#### **1. Forensic Report Preparation**

Your report must include:

* Executive summary
* Attack timeline
* Entry point and exploited services
* Affected systems and data
* Indicators of Compromise (IPs, domains, ports)
* Supporting evidence (screenshots and packet references)

**Exercise 8:**

* Submit a **professional forensic investigation report**.

---

#### **2. Presentation of Findings**

**Exercise 9:**

* Prepare a presentation as if briefing **BookWorld executives**.
* Focus on impact, risk, and remediation—not technical jargon.

---

### **Conclusion**

This lab tests your ability to **think like a forensic analyst**, not follow instructions blindly. By applying the skills learned in **Lab 6**, you investigated a realistic enterprise breach scenario, identified attacker behavior, reconstructed an attack timeline, and produced professional forensic documentation.

Failure to apply independent analysis techniques will be reflected in assessment outcomes.


