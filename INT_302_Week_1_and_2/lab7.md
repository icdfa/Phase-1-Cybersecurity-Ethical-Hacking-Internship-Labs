

## **INT302: Kali Linux Tools and System Security – Lab 7: Practical Use Cases for Wireshark in Real-World Scenarios**

### **Lab Overview**
In this lab, participants will explore practical use cases for Wireshark in incident response and threat hunting scenarios. You will learn how to use Wireshark to analyze network traffic during security incidents, identify malicious activities, and gather evidence for forensic investigations.

---

### **Lab Objectives**
By the end of this lab, you will be able to:
1. Use Wireshark to analyze network traffic in the context of an incident.
2. Identify indicators of compromise (IoCs) and malicious activities within network traffic.
3. Implement threat hunting techniques using Wireshark for proactive security measures.
4. Generate detailed reports of your findings to aid in incident response efforts.

---

### **Tools Used**
- **Wireshark**: A graphical network protocol analyzer.
- **tshark**: The terminal-based version of Wireshark.

---

### **Prerequisites**
- Completion of Lab 6: Advanced Packet Analysis Techniques.
- Basic understanding of network security concepts.

---

### **Lab Steps**

#### **Step 1: Incident Response Analysis**

1. **Scenario Setup**:
   - You are part of the incident response team tasked with investigating a suspected data breach in your organization.
   - Capture network traffic during the incident using Wireshark to analyze the packets and identify any suspicious activities.

2. **Initial Traffic Inspection**:
   - Use Wireshark to open the captured traffic file.
   - Apply filters to focus on traffic patterns during the incident. Key filters to consider:
     - `ip.addr == <suspected IP>` to focus on a suspected source.
-

```bash
tcp.port == <port number>
```


**Exercise 1**:  
- Describe the overall network traffic during the incident. Are there any noticeable spikes or anomalies? What potential indicators of compromise did you identify? __________

3. **Extracting Suspicious Packets**:
   - Look for specific indicators of compromise (IoCs) such as:
     - Unusual outbound connections to unknown IP addresses.
     - Repeated failed login attempts or suspicious authentication attempts.
     - Malicious payloads or command-and-control (C2) traffic.

**Exercise 2**:  
- Identify a specific packet that raises suspicion. Provide details about the packet, including source and destination IPs, ports, and protocol. What makes this packet suspicious? __________

---

#### **Step 2: Threat Hunting Techniques**

1. **Proactive Threat Hunting**:
   - Use Wireshark to perform proactive threat hunting within your network environment.
   - Set up capture filters to monitor for specific behaviors or protocols often associated with threats (e.g., suspicious DNS queries or unusual traffic on uncommon ports).

**Capture Filter Example**:  
To capture traffic on port 53 (DNS):  
```bash
tcp port 53 or udp port 53
```

**Exercise 3**:  
- Implement a capture filter to monitor DNS traffic. Analyze the captured packets and summarize any findings related to unusual queries or connections. __________

2. **Analyzing Suspicious DNS Traffic**:
   - Focus on DNS query packets to identify potential domain generation algorithms (DGAs) or connections to known malicious domains.

**Exercise 4**:  
- Identify any DNS packets that may indicate a connection to a suspicious or malicious domain. Provide details about the domain queried and any associated IP addresses. __________

3. **Detecting Anomalous Traffic Patterns**:
   - Examine the captured traffic for unusual patterns, such as:
     - Large data transfers to unknown destinations.
     - Outbound traffic during non-business hours.

**Exercise 5**:  
- Document any anomalous traffic patterns you discovered. What does this suggest about potential malicious activity? __________

---

#### **Step 3: Reporting Findings**

1. **Creating an Incident Report**:
   - Compile your findings into a detailed incident report. Include:
     - Summary of the incident.
     - Timeline of events.
     - Indicators of compromise identified.
     - Recommendations for remediation and prevention.

**Exercise 6**:  
- Prepare an incident report based on your analysis. Include any relevant packet captures, screenshots, and detailed explanations of the findings. __________

2. **Presentation of Findings**:
   - Present your findings to your peers or instructor, focusing on the analysis process and the conclusions drawn from the packet data.
   - Discuss the importance of proactive threat hunting and incident response in maintaining network security.

**Exercise 7**:  
- Create a presentation slide deck summarizing your lab experience, findings, and recommendations for improving incident response capabilities. __________

---

### **Conclusion**
In this lab, you explored practical use cases for Wireshark in real-world scenarios, including incident response and threat hunting. By applying the skills you learned, you enhanced your ability to analyze network traffic and identify malicious activities, contributing to a more robust cybersecurity posture.

---

### **Next Steps**
In the next lab, we will focus on advanced malware analysis techniques, exploring how to dissect and analyze malware behaviors using various tools.

---
