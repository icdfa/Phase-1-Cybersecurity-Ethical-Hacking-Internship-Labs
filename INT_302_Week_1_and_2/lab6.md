

## **INT302: Kali Linux Tools and System Security – Lab 6: Advanced Packet Analysis Techniques**

### **Lab Overview**
In this lab, participants will delve deeper into packet analysis using Wireshark. You will learn how to dissect various protocols, create custom filters for targeted analysis, and identify vulnerabilities within network traffic. This hands-on lab will enhance your understanding of network security and equip you with the skills to perform thorough traffic analysis.

---

### **Lab Objectives**
By the end of this lab, you will be able to:
1. Dissect various network protocols and understand their structure.
2. Create custom display filters to isolate specific packets of interest.
3. Analyze traffic for signs of vulnerabilities and malicious activities.
4. Use advanced features in Wireshark for effective network troubleshooting and security assessment.

---

### **Tools Used**
- **Wireshark**: A graphical network protocol analyzer.
- **tshark**: The terminal-based version of Wireshark.

---

### **Prerequisites**
- Completion of Lab 5: Wireshark.
- Basic understanding of networking concepts and protocols.

---

### **Lab Steps**

#### **Step 1: Dissecting Protocols**

1. **TCP Analysis**:
   - Capture some TCP traffic (e.g., browsing a website) using Wireshark.
   - Select a TCP packet and expand the details in the Packet Details Pane.
   - Identify key components such as TCP flags (SYN, ACK, FIN) and sequence numbers.

**Exercise 1**:  
- Describe the purpose of the SYN and ACK flags in the TCP handshake. How do these flags indicate the status of a connection? __________

2. **HTTP Analysis**:

```bash
http
```

   - Examine the headers of an HTTP request and response.

**Key Headers to Focus On**:
- Request Method (GET, POST, etc.)
- Status Code (200, 404, etc.)
- User-Agent

**Exercise 2**:  
- Choose an HTTP packet and summarize its request method, status code, and any notable headers. What can you infer about the transaction? __________

3. **DNS Analysis**:

```bash
dns
```

   - Examine the DNS response packets to see the resolved IP addresses for the queried domains.

**Exercise 3**:  
- Identify a DNS query and its corresponding response. What information does the response provide, and how is it structured? __________

---

#### **Step 2: Creating Custom Filters**

1. **Filter Basics**:
   - Learn about basic filtering syntax in Wireshark.
   - Combine multiple filters using logical operators (`and`, `or`, `not`).

**Examples**:
- Filter for HTTP traffic from a specific IP: `http and ip.src == <source IP>`
- Filter for DNS queries excluding specific domains: `dns and !(dns.qry.name == "<excluded domain>")`

**Exercise 4**:  
- Create a custom filter that captures only TCP traffic from your machine to a specific target IP. Document the filter syntax and the packets captured. __________

2. **Using Filter Expressions**:
   - Utilize the Wireshark display filter expression dialog to construct complex filters.
   - Practice filtering packets based on multiple criteria, such as source/destination IP, protocol type, and port numbers.

**Exercise 5**:  
- Write a filter that captures traffic on a specific port (e.g., HTTP port 80) and analyze the results. What packets were captured? __________

---

#### **Step 3: Identifying Vulnerabilities**

1. **Recognizing Anomalies**:
   - Look for signs of potential vulnerabilities, such as unusual traffic patterns, unencrypted sensitive information, or malicious payloads.

**Common Indicators**:
- Repeated SYN packets (possible SYN flood attack).
- HTTP packets containing sensitive information (e.g., passwords, credit card numbers).

**Exercise 6**:  
- Analyze your capture for any anomalies or indicators of potential vulnerabilities. Document your findings and suggest possible remediation steps. __________

2. **Security Protocols**:
   - Examine traffic from secure protocols (HTTPS) and identify how encryption affects packet analysis.
- Use the

```bash
ssl
```


**Exercise 7**:  
- Capture HTTPS traffic and identify the initial handshake packets. What information is exchanged during this handshake, and how does it contribute to security? __________

---

#### **Step 4: Practical Applications and Reporting**

1. **Conduct a Security Assessment**:
   - Using the knowledge gained from this lab, conduct a mini security assessment on your network traffic.
   - Look for signs of compromised traffic, open ports, or unauthorized access attempts.

**Exercise 8**:  
- Prepare a brief report summarizing your findings during the assessment. Include potential risks and recommended actions. __________

2. **Creating a Capture Report**:
   - Document your analysis steps, findings, and any relevant screenshots or packet details.
   - Prepare a presentation summarizing your lab experience and learnings.

**Exercise 9**:  
- Create a capture report that includes your objectives, methods, key findings, and any recommendations for improving network security. __________

---

### **Conclusion**
In this lab, you have explored advanced packet analysis techniques using Wireshark. You learned to dissect protocols, create custom filters, and identify vulnerabilities in network traffic. These skills are essential for performing thorough traffic analysis and enhancing your capabilities as a cybersecurity professional.

---

### **Next Steps**
In the next lab, we will explore practical use cases for Wireshark in real-world scenarios, including incident response and threat hunting techniques.

