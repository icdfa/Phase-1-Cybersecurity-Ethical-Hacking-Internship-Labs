### **INT303: Networking Fundamentals – Lab 2**

#### **Lab 2: Exploring Network Interfaces and Packet Transmission Using OWASP Broken Web Application IP**

---

#### **Objective:**
In this lab, you will dive deeper into the concept of network interfaces and packet transmission by analyzing the network interface configuration on your system. You will explore how to capture and analyze network packets using various tools and understand the process of packet transmission to and from the OWASP Broken Web Application VM.

---

#### **Learning Outcomes:**
By the end of this lab, students will:
- Understand the role and configuration of network interfaces.
- Use packet capture tools to analyze network traffic and understand how data is transmitted.
- Gain experience in monitoring and troubleshooting network interfaces and traffic.

---

#### **Materials Needed:**
- Linux-based system (Kali, Ubuntu, etc.)
- OWASP Broken Web Application VM (running and reachable on your network)
- IP address of the OWASP Broken Web Application (e.g., 192.168.X.X)
- Wireshark or tshark for packet capture

---

#### **Lab Exercises:**

---

### **Exercise 1: Viewing and Configuring Network Interfaces**

1. **Task:** View your network interfaces using the `ifconfig` or `ip` command.

```bash
# View network interfaces (older method)
ifconfig

# View network interfaces (modern method)
ip addr show

# Show only active interfaces
ip link show

# Show interface statistics
ip -s link
```
   
2. **Question:**
   - What network interfaces are available on your system?
   - Identify the IP address assigned to each interface.
   - Describe the difference between a loopback interface and an external network interface.

---

### **Exercise 2: Capturing Packets on a Specific Interface**

3. **Task:** Use `tcpdump` or `tshark` to capture packets on your primary network interface.

```bash
# Capture packets on specific interface
sudo tcpdump -i <interface>

# Example: capture on eth0
sudo tcpdump -i eth0

# Capture and save to file
sudo tcpdump -i eth0 -w capture.pcap

# Alternative: use tshark
sudo tshark -i <interface>

# Capture only first 100 packets
sudo tcpdump -i eth0 -c 100
```
   
4. **Question:**
   - What kind of packets are being captured?
   - Are there any packets related to communication with the OWASP Broken Web Application VM?
   - Describe the role of this network interface in transmitting and receiving packets.

---

### **Exercise 3: Examining Network Statistics**

5. **Task:** Use the `netstat` or `ss` command to view current network statistics and connections.

```bash
# View network interface statistics
netstat -i

# Modern alternative: socket statistics
ss -s

# Show all network connections
netstat -an

# Show listening ports
ss -tuln

# Show established connections
netstat -tn
```
   
6. **Question:**
   - What is the current status of your network interfaces?
   - What active connections are visible?
   - Explain the significance of these statistics in monitoring network performance.

---

### **Exercise 4: Monitoring Network Traffic with Wireshark**

7. **Task:** Use Wireshark to monitor network traffic on your primary interface and filter traffic going to and from the OWASP Broken Web Application VM.

```bash
# Launch Wireshark
wireshark

# Or use tshark with display filter
sudo tshark -i eth0 -Y "ip.addr == 192.168.56.101"

# Capture and filter for specific IP
sudo tshark -i eth0 -f "host 192.168.56.101"

# Save filtered capture
sudo tshark -i eth0 -Y "ip.addr == 192.168.56.101" -w filtered_capture.pcap
```

**Wireshark Display Filters:**
- `ip.addr == <OWASP_IP>` - Filter for specific IP
- `tcp.port == 80` - Filter for HTTP traffic
- `tcp.port == 443` - Filter for HTTPS traffic
   
8. **Question:**
   - Analyze the packets going to and from the OWASP VM. What types of protocols are in use?
   - Can you identify any key packet details such as source/destination IP addresses, port numbers, and flags?
   - How does the TCP/IP model apply to the data captured?

---

### **Exercise 5: Packet Transmission Analysis**

9. **Task:** Perform a ping or TCP connection request to the OWASP Broken Web Application IP and capture the packet details using `tcpdump` or Wireshark.
   - Command: `ping <OWASP_IP>` or `telnet <OWASP_IP> 80` (to initiate a simple connection)
   - Capture the traffic using `tcpdump -i <interface> host <OWASP_IP>`, or set the appropriate filter in Wireshark.
   
10. **Question:**
   - What do you observe during the packet transmission process?
   - Describe the handshake process or the round-trip of the packets for ping or TCP connection.
   - Which layers of the OSI and TCP/IP models are involved in this transmission?

---

### **Exercise 6: Troubleshooting Network Interface Issues**

11. **Task:** Simulate a network interface failure by disabling and then re-enabling an interface. Observe how this affects network connectivity to the OWASP Broken Web Application VM.
   - Command: `sudo ifconfig <interface> down` and `sudo ifconfig <interface> up` (or use `ip` commands)
   
12. **Question:**
   - What happens when you disable the network interface?
   - How does your system respond when the interface is re-enabled?
   - Explain how network administrators can use this knowledge for troubleshooting connectivity issues.

---

### **Exercise 7: Bandwidth Monitoring**

13. **Task:** Use the `iftop` or `nload` command to monitor the bandwidth usage on your system while interacting with the OWASP Broken Web Application VM.
   - Command: `sudo iftop -i <interface>` or `nload <interface>`
   
14. **Question:**
   - What is the current bandwidth usage while communicating with the OWASP VM?
   - Identify the impact of network traffic on your interface. Is there any traffic congestion?
   - How does this help in monitoring network performance?

---

### **Exercise 8: Advanced Packet Capture Filters**

15. **Task:** Create custom filters in Wireshark or `tcpdump` to capture only specific types of traffic, such as TCP or HTTP traffic, between your system and the OWASP VM.
   - Example Filter for HTTP Traffic: `tcp port 80 and ip.addr == <OWASP_IP>`
   
16. **Question:**
   - What is the significance of filtering specific traffic?
   - How can advanced filters help network engineers diagnose and resolve issues?

---

### **Submission Requirements:**
- Submit a report detailing the output of each exercise.
- Include screenshots for critical steps such as packet captures and bandwidth monitoring.
- Provide explanations for each observed behavior, particularly focusing on the significance of network interfaces and packet transmission.

---

#### **Reflection:**
By the end of this lab, students will have a practical understanding of network interfaces and packet transmission. They will be able to configure and monitor network interfaces, analyze packet transmission, and troubleshoot network connectivity using real-world tools.

---
