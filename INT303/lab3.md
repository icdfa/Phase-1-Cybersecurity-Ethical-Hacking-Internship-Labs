### **INT303: Networking Fundamentals – Lab 3**

#### **Lab 3: TCP/IP Protocol Stack and Packet Inspection Using OWASP Broken Web Application IP**

---

#### **Objective:**
In this lab, students will delve into the Transmission Control Protocol/Internet Protocol (TCP/IP) stack, dissecting and inspecting the various layers involved in packet transmission. Students will focus on understanding how data travels across a network, analyzing packets, and troubleshooting issues related to the TCP/IP model.

---

#### **Learning Outcomes:**
By the end of this lab, students will:
- Understand the fundamentals of the TCP/IP model.
- Be able to analyze packets at different layers (Application, Transport, Network, and Link).
- Gain hands-on experience in dissecting TCP/IP traffic using packet inspection tools.
- Learn how to apply practical troubleshooting techniques based on TCP/IP behavior.

---

#### **Materials Needed:**
- Linux-based system (Kali, Ubuntu, etc.)
- OWASP Broken Web Application VM (running and reachable on your network)
- IP address of the OWASP Broken Web Application (e.g., 192.168.X.X)
- Wireshark or tshark for packet capture and analysis

---

#### **Lab Exercises:**

---

### **Exercise 1: Understanding the TCP/IP Model**

1. **Task:** Briefly review the layers of the TCP/IP model (Application, Transport, Network, and Link layers). Understand the purpose and function of each layer in data transmission.

2. **Question:**
   - Explain the differences between the TCP/IP and OSI models.
   - Which layers of the TCP/IP model correspond to specific OSI layers?

---

### **Exercise 2: Capturing and Analyzing TCP Packets**

3. **Task:** Initiate a connection to the OWASP Broken Web Application VM via HTTP or SSH. Capture TCP packets related to this connection using

```bash
tcpdump
```

   - Command:

```bash
tcpdump -i <interface> tcp and host <OWASP_IP>
```


```bash
tcpdump -i eth0 tcp and host 192.168.56.101
```

   
4. **Question:**
   - What happens during the TCP handshake (SYN, SYN-ACK, ACK)?
   - Identify and describe the flags used in TCP communication (SYN, ACK, FIN, etc.).
   - How does the TCP connection maintain reliability during transmission?

---

### **Exercise 3: Investigating IP Packets (Network Layer)**

5. **Task:** Capture and analyze the IP packets from your connection to the OWASP Broken Web Application.
   - Command: Use Wireshark or

```bash
tcpdump
ip.addr == <OWASP_IP>
```

   
6. **Question:**
   - What fields can you see in the IP packet header (e.g., Source IP, Destination IP, TTL, etc.)?
   - What is the significance of each of these fields?
   - How does IP routing work in this scenario? Are there any hops between your system and the OWASP VM?

---

### **Exercise 4: Application Layer Analysis (HTTP/SSH Traffic)**

7. **Task:** If you're using HTTP, filter the packets to capture only HTTP traffic using Wireshark or

```bash
tcpdump
```


```bash
tcpdump -i <interface> port 80 and host <OWASP_IP>
```


```bash
tcpdump -i <interface> port 22 and host <OWASP_IP>
```

   
8. **Question:**
   - Analyze the HTTP packets. What information is available in the HTTP request and response?
   - For SSH traffic, what is the significance of encrypted packets? Can you analyze the payload?
   - How does the application layer play a role in data exchange between your system and the OWASP VM?

---

### **Exercise 5: Error Handling in TCP/IP Transmission**

9. **Task:** Simulate packet loss or network issues by introducing a delay or stopping the network connection momentarily. Capture how TCP/IP handles this issue.
   - Command: Temporarily disable your network interface using

```bash
ifconfig <interface> down
```

   
10. **Question:**
    - What happens when packets are dropped or delayed?
    - How does TCP ensure data reliability in the presence of errors?
    - How do retransmissions and sequence numbers work in TCP to maintain a proper data flow?

---

### **Exercise 6: ICMP and Ping Inspection (Network Layer)**

11. **Task:** Send a series of

```bash
ping
```

    - Command:

```bash
ping <OWASP_IP>
tcpdump
icmp
```

    
12. **Question:**
    - What are the key fields in an ICMP packet (e.g., Type, Code, Checksum)?
    - How does ICMP assist in diagnosing network connectivity issues?
    - What is the significance of TTL in both ICMP packets and general IP packets?

---

### **Exercise 7: Analyzing UDP Packets (Transport Layer)**

13. **Task:** If available, generate some UDP traffic to the OWASP VM by using a simple application or UDP-based service. Capture and analyze the UDP packets.
    - Command:

```bash
tcpdump -i <interface> udp and host <OWASP_IP>
```

    
14. **Question:**
    - Compare UDP with TCP. What are the major differences in packet structure and behavior?
    - Why does UDP not ensure reliability, and in what scenarios would you prefer UDP over TCP?
    - How does UDP manage data transmission without the need for acknowledgments or retransmissions?

---

### **Exercise 8: OS Detection via Nmap (Network and Transport Layers)**

15. **Task:** Use

```bash
nmap
```

    - Command:

```bash
nmap -O <OWASP_IP>
```

   
16. **Question:**
- How does

```bash
nmap
```

    - What packet characteristics (TTL, window size, etc.) help in identifying the OS?
    - Explain why OS detection can be an important step in network analysis and vulnerability assessment.

---

### **Exercise 9: Analyzing ARP Traffic (Link Layer)**

17. **Task:** Use

```bash
arp-scan
```

    - Command:

```bash
arp-scan -I <interface> <OWASP_IP>
```

   
18. **Question:**
    - What information can you gather from ARP packets (e.g., MAC addresses)?
    - How does the ARP protocol function at the link layer?
    - What role does ARP play in the communication between your system and the OWASP VM?

---

### **Exercise 10: Troubleshooting Network Connectivity Using TCP/IP Knowledge**

19. **Task:** Simulate a common network issue (e.g., incorrect subnet mask, gateway misconfiguration) and troubleshoot the issue using your understanding of the TCP/IP stack.
   
20. **Question:**
    - What is the issue you simulated, and how did it affect network communication?
    - How did you diagnose and resolve the issue using packet inspection and knowledge of the TCP/IP layers?
    - What tools and techniques would you recommend for real-world network troubleshooting?

---

### **Submission Requirements:**
- Submit a report that includes packet captures, command outputs, and explanations for each exercise.
- Include screenshots and highlight key details in the packet captures.
- Provide in-depth analysis of TCP/IP behavior observed during the lab.

---

#### **Reflection:**
Through this lab, students will gain practical experience in dissecting and troubleshooting network traffic using the TCP/IP stack. Understanding how data flows across the network at various layers will help in mastering network fundamentals and preparing for real-world challenges in network administration and cybersecurity.

---

Would you like to proceed with Lab 4 or make any changes to this one?