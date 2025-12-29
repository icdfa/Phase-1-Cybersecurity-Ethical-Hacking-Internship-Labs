
## **INT302: Kali Linux Tools and System Security – Lab 7: IoT Network Forensic Investigation Using Wireshark**

### **Lab Overview**

In this lab, participants will investigate a network breach incident affecting **TechGlobal Solutions**. You will use **Wireshark** to analyze network traffic captured during a suspected attack, identify malicious activities targeting IoT and enterprise systems, and gather evidence to support a forensic investigation.

---

### **Lab Objectives**

By the end of this lab, you will be able to:

1. Analyze network traffic in the context of a real-world IoT/enterprise security incident.
2. Identify indicators of compromise (IoCs) and suspicious communications.
3. Investigate protocol usage, unusual ports, and traffic patterns in IoT environments.
4. Generate a professional forensic report documenting findings, timelines, and remediation recommendations.

---

### **Tools Used**

* **Wireshark**: A graphical network protocol analyzer.
* **tshark**: The terminal-based version of Wireshark.
* **NetworkMiner (optional)**: For artifact extraction.
* **WHOIS / GeoIP tools**: To identify external IP addresses and geographic locations.

---

### **Prerequisites**

* Completion of Lab 6: Advanced Packet Analysis Techniques.
* Basic understanding of network protocols and security concepts.
* Access to the provided PCAP file:
  [TechGlobal Network Breach PCAP](https://drive.google.com/file/d/1IV_V5weV8jBTqzgzLJxEKM0VjCpB1RmU/view)

---

### **Lab Steps**

#### **Step 1: Incident Response Analysis**

1. **Scenario Setup**:

   * You are part of the digital forensics team investigating anomalous network activity targeting customer database servers.
   * The incident occurred on **Tuesday, November 19, 2024, between 14:30–16:45 UTC**.
   * Your goal is to identify suspicious IP addresses, attack vectors, and compromised systems.

2. **Initial Traffic Inspection**:

   * Open the PCAP file in Wireshark.
   * Apply filters to focus on traffic patterns during the incident:

     ```bash
     ip.addr == <suspected IP>
     tcp.port == <target port>
     udp.port == <target port>
     ```

**Exercise 1:**

* Describe the overall network traffic during the incident. Are there noticeable spikes or anomalies? What potential IoCs did you identify? __________

3. **Extracting Suspicious Packets**:

   * Look for IoCs such as:

     * Connections from external IPs to internal databases.
     * Repeated failed logins or authentication attempts.
     * Suspicious payloads or command-and-control communications.

**Exercise 2:**

* Identify a specific packet that raises suspicion. Include source/destination IPs, ports, protocol, and explain why it is suspicious. __________

---

#### **Step 2: Protocol and Service Analysis**

1. **TCP/UDP Traffic Patterns**:

   * Analyze unusual port usage.
   * Identify non-standard services being targeted.

2. **DNS Query Analysis**:

   * Filter DNS traffic:

     ```bash
     udp.port == 53
     ```
   * Check for suspicious or dynamically generated domains (possible DGAs).

**Exercise 3:**

* List any DNS queries indicating potential malicious domains and associated IPs. __________

3. **Identifying Attack Vectors**:

   * Determine the first malicious connection attempt.
   * Map attack sequence: reconnaissance, exploitation, data exfiltration.

**Exercise 4:**

* Which protocol was predominantly used during the attack?
* Identify the initial entry point. __________

---

#### **Step 3: Anomaly Detection and Traffic Mapping**

1. **Conversation Mapping**:

   * Use Wireshark’s **Endpoints** and **Conversations** features.
   * Map attacker IPs to targeted hosts and services.

2. **Data Exfiltration Indicators**:

   * Identify unusually large outbound transfers.
   * Observe outbound traffic patterns outside normal operating hours.

**Exercise 5:**

* Document any anomalous traffic patterns and suggest potential malicious activities. __________

---

#### **Step 4: Reporting Findings**

1. **Forensic Report Preparation**:

   * Include:

     * Executive summary of the incident.
     * Attack timeline.
     * Targeted systems and services.
     * IoCs (malicious IPs, domains, protocols, ports).
     * Supporting evidence (screenshots, packet captures).

2. **Recommendation Section**:

   * Suggest network security improvements to prevent similar incidents.

**Exercise 6:**

* Compile an incident report in a professional format, including all relevant analysis. __________

3. **Presentation of Findings**:

   * Present your investigation results, highlighting analysis methods and key findings.
   * Discuss the importance of proactive threat detection in enterprise and IoT environments.

**Exercise 7:**

* Prepare a slide deck summarizing your investigation, findings, and remediation recommendations. __________

---

### **Conclusion**

In this lab, you performed a forensic investigation using **Wireshark** on a real-world IoT/enterprise network breach scenario. You identified attack vectors, suspicious traffic patterns, and IoCs, and produced a professional report with actionable recommendations.

---
