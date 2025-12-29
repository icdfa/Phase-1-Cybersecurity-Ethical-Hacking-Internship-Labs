
## **INT302: Kali Linux Tools and System Security – Lab 7: IoT & Enterprise Network Forensic Investigation Using Wireshark**

---

### **Lab Overview**

In this lab, participants will conduct a **network forensic investigation** involving **BookWorld**, a major online bookstore. Recently, unusual behavior has been detected in BookWorld's **database activity**, including spikes in query volumes and server resource usage, suggesting the possibility of a **cyberattack**.

You are part of a **Digital Forensics team**. The business is concerned about the **integrity of customer data** and its internal systems. Your mission is to:

* Conduct a thorough forensic analysis of the network traffic
* Identify how the attacker gained access
* Assess the scope of the breach
* Prepare your findings in a comprehensive report

This lab emphasizes **active packet filtering, protocol analysis, and evidence discovery**, giving you hands-on experience in real-world enterprise network forensics.

---

### **Lab Objectives**

By the end of this lab, you will be able to:

1. Analyze network traffic related to a real-world enterprise web application.
2. Identify indicators of compromise (IoCs) related to database abuse and web exploitation.
3. Use Wireshark filters to detect suspicious HTTP POST requests, DNS queries, and database interactions.
4. Trace attacker behavior from initial access to possible data exfiltration.
5. Produce a professional forensic report documenting findings, timelines, and remediation recommendations.

---

### **Tools Used**

* **Wireshark** – Primary network forensic analysis tool
* **tshark** – Command-line packet analysis
* **NetworkMiner (optional)** – Artifact and credential extraction
* **WHOIS / GeoIP tools** – External IP attribution

---

### **Prerequisites**

* Completion of Lab 6: Advanced Packet Analysis Techniques
* Basic understanding of HTTP, TCP/IP, DNS, and database protocols
* Access to the provided PCAP file:
  [BookWorld Network Breach PCAP](https://drive.google.com/file/d/1IV_V5weV8jBTqzgzLJxEKM0VjCpB1RmU/view)

---

## **Lab Steps**

---

### **Step 1: Incident Response Analysis**

#### **1. Scenario Setup**

* You are a member of the **Digital Forensics team** investigating unusual activity at **BookWorld**.
* Security monitoring detected:

  * Spikes in database query volumes
  * Abnormal server resource usage
  * External IPs targeting customer database servers

**Mission:**

* Identify how the attacker gained access
* Determine which systems and services were affected
* Assess whether customer data was compromised
* Prepare a comprehensive forensic report with evidence

---

#### **2. Initial Traffic Inspection**

1. Open the PCAP file in Wireshark.
2. Set the correct time format (**UTC**) and begin with **broad traffic visibility**.

**Recommended display filters:**

```bash
ip.addr == <suspected IP>
tcp
udp
```

**Exercise 1:**

* Describe the overall traffic behavior.
* Are there spikes or repeated connections to critical servers?
* What early indicators suggest malicious activity?

---

---

#### **3. Identifying Suspicious Hosts**

1. Navigate to:

   * **Statistics → Endpoints**
   * **Statistics → Conversations**
2. Identify:

   * External IPs communicating excessively with BookWorld servers
   * Internal servers receiving abnormal traffic volumes

**Exercise 2:**

* Identify at least one suspicious external IP address.
* Why does this IP stand out compared to others?

---

---

### **Step 2: Web and Database Traffic Investigation**

#### **1. HTTP Request Analysis (POST Investigation)**

Attackers often abuse **HTTP POST requests** to:

* Exploit login pages
* Inject malicious payloads
* Extract sensitive data

Apply the following filter:

```bash
http.request.method == "POST"
```

Focus on:

* Login endpoints
* Customer and order-related queries
* Repeated requests or unusually large payloads

**Exercise 3:**

* Identify suspicious POST requests.
* Which parameters or endpoints appear abnormal?
* Are there repeated requests that could indicate brute-force or data extraction?

---

---

#### **2. Database-Related Traffic**

Filter for database ports:

```bash
tcp.port == 3306    # MySQL
tcp.port == 5432    # PostgreSQL
tcp.port == 1433    # MSSQL
```

Look for:

* External systems communicating with internal databases
* Repeated query patterns
* Abnormal session lengths

**Exercise 4:**

* Which database services were targeted?
* What evidence suggests database enumeration or abuse?

---

---

### **Step 3: DNS and Command‑and‑Control Analysis**

#### **1. DNS Traffic Inspection**

Filter DNS traffic:

```bash
udp.port == 53
```

Look for:

* Unusual domains or subdomains
* Repeated DNS queries
* Long or random-looking subdomains (possible DGAs)

**Exercise 5:**

* Identify suspicious domains.
* Do the domains appear algorithmically generated or unrelated to BookWorld?

---

---

#### **2. Data Exfiltration Indicators**

Apply filters to detect large outbound transfers:

```bash
tcp.len > 1000
```

Correlate with:

* POST requests
* Database responses
* Long TCP sessions

**Exercise 6:**

* Is there evidence of data exfiltration?
* Which protocol was likely used for exfiltration?

---

---

### **Step 4: Attack Timeline Reconstruction**

1. Identify:

   * First malicious connection
   * Exploitation phase
   * Data exfiltration phase
2. Use packet timestamps to build a **timeline of events**.

**Exercise 7:**

* Reconstruct the attack sequence step by step.
* At what point was customer data most at risk?

---

---

### **Step 5: Reporting Findings**

#### **1. Forensic Report Preparation**

Your report should include:

* Executive summary of the incident
* Attack timeline and sequence of events
* Entry point and exploited services
* Affected systems and sensitive data
* Indicators of Compromise (IPs, domains, ports)
* Supporting evidence (screenshots, packet captures)

**Exercise 8:**

* Compile a **professional forensic report** based on your findings.

---

---

#### **2. Presentation of Findings**

* Present your findings as if briefing **BookWorld executives**.
* Focus on **what happened**, **impact**, and **how to prevent recurrence**.

**Exercise 9:**

* Prepare a slide deck summarizing your investigation, findings, and remediation recommendations.

---

---

### **Conclusion**

In this lab, you conducted a **hands-on forensic investigation** on BookWorld’s network using Wireshark. You:

* Detected suspicious behavior
* Identified attacker activity and database targeting
* Assessed potential data exposure
* Produced actionable forensic evidence and reporting

This lab enhances your ability to **filter, pivot, and analyze traffic**, preparing you for real-world incident response.

---

