### **INT303: Networking Fundamentals – Lab 1**

#### **Lab 1: Understanding Network Layers and TCP/IP Model using OWASP Broken Web Application IP**

---

#### **Objective:**
In this lab, you will explore the OSI and TCP/IP models using the IP address of the OWASP Broken Web Application virtual machine. This practical exercise will help you understand how data is transmitted across networks, the key protocols involved, and how to use essential network commands for troubleshooting and analysis.

---

#### **Learning Outcomes:**
By the end of this lab, students will:
- Understand the OSI and TCP/IP models and their functions.
- Use essential network tools to explore and analyze network traffic.
- Apply knowledge of TCP/IP layers in real-world scenarios using OWASP Broken Web Application IP.

---

#### **Materials Needed:**
- Linux-based system (Kali, Ubuntu, etc.)
- OWASP Broken Web Application VM (running and reachable on your network)
- Terminal access with networking tools
- IP address of the OWASP Broken Web Application (e.g., 192.168.X.X)

---

#### **Lab Exercises:**

---

### **Exercise 1: Understanding OSI and TCP/IP Models**

1. **Task:** Review the OSI and TCP/IP models and their layers.
   - OSI Layers: Physical, Data Link, Network, Transport, Session, Presentation, Application
   - TCP/IP Layers: Link, Internet, Transport, Application
   
2. **Question:**
   - List the OSI model layers and describe the function of each.
   - Match each OSI layer with its corresponding TCP/IP layer.

---

### **Exercise 2: Pinging the OWASP Broken Web Application**

3. **Task:** Use the `ping` command to check the reachability of the OWASP Broken Web Application using its IP address.

```bash
# Replace <OWASP_IP> with the actual IP address
ping <OWASP_IP>

# Example:
ping 192.168.56.101

# Send only 4 packets
ping -c 4 192.168.56.101
```
   
4. **Question:**
   - What happens when you ping the OWASP application? Describe the process.
   - Which OSI layer does the `ping` command operate in? Explain.

---

### **Exercise 3: Tracing the Path to the OWASP Application**

5. **Task:** Use the `traceroute` command to trace the route packets take to reach the OWASP Broken Web Application.

```bash
# Trace the route to OWASP VM
traceroute <OWASP_IP>

# Example:
traceroute 192.168.56.101
```
   
6. **Question:**
   - How many hops did it take to reach the OWASP VM?
   - Describe the significance of each hop and what role traceroute plays in network troubleshooting.

---

### **Exercise 4: Viewing Active Connections to OWASP VM**

7. **Task:** Use `netstat` to view active network connections between your system and the OWASP application.

```bash
# View active connections to OWASP VM
netstat -an | grep <OWASP_IP>

# Alternative: use ss command (modern replacement for netstat)
ss -an | grep <OWASP_IP>
```
   
8. **Question:**
   - What connections do you see? Identify the source and destination IP addresses.
   - Explain how the Transport Layer (TCP/UDP) is involved in this communication.

---

### **Exercise 5: TCP vs. UDP**

9. **Task:** Investigate the difference between TCP and UDP by scanning the OWASP Broken Web Application.

```bash
# Run a TCP scan using nmap
nmap -sT <OWASP_IP>

# Example:
nmap -sT 192.168.56.101

# Run a UDP scan (requires root privileges)
sudo nmap -sU <OWASP_IP>

# Example:
sudo nmap -sU 192.168.56.101
```

10. **Question:**
   - What are the key differences between TCP and UDP in terms of reliability and speed?
   - Based on the scan results, list which services on the OWASP application are using TCP and which are using UDP.

---

### **Exercise 6: Discovering MAC Addresses with ARP**

11. **Task:** Use the `arp` command to view the MAC address of the OWASP Broken Web Application.

```bash
# View ARP cache and find OWASP VM's MAC address
arp -a | grep <OWASP_IP>

# Alternative: view entire ARP table
arp -a

# Modern alternative using ip command
ip neigh show
```
   
12. **Question:**
   - What is the MAC address associated with the OWASP VM’s IP?
   - Explain the significance of ARP in the Data Link Layer and how it contributes to successful communication.

---

### **Exercise 7: Capturing Network Traffic with Wireshark**

13. **Task:** Use Wireshark or `tshark` to capture network packets between your machine and the OWASP Broken Web Application.

```bash
# Launch Wireshark GUI
wireshark

# Or use tshark for command-line capture
sudo tshark -i <interface> host <OWASP_IP>

# Example: capture on eth0 interface
sudo tshark -i eth0 host 192.168.56.101

# Save capture to file
sudo tshark -i eth0 -w capture.pcap host 192.168.56.101
```
   
14. **Question:**
   - Analyze the captured traffic. What protocols are in use?
   - Can you identify the handshake process or other significant events in the captured packets?

---

### **Submission Requirements:**
- Submit a detailed report including answers to the questions and the commands you used.
- Include screenshots where appropriate, particularly for commands like `ping`, `traceroute`, `netstat`, and packet captures from Wireshark.
- Discuss any issues or troubleshooting steps taken during the lab.

---

#### **Reflection:**
At the end of this lab, students will have hands-on experience with network layer interaction using real-world tools and commands, along with a better understanding of how the TCP/IP model facilitates communication.
