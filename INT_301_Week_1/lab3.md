# **Lab 3: Advanced Network Analysis and Troubleshooting**

## **Enhanced Objectives**
In this lab, you will:
- Master advanced network configuration and diagnostic commands.
- Perform comprehensive network analysis and traffic monitoring.
- Troubleshoot complex network issues using multiple tools.
- Understand network protocols and their security implications.
- Implement network security controls and monitoring.

## **Background / Scenario**
As a security professional, you need deep understanding of network operations beyond basic connectivity checks. This lab covers advanced network analysis, protocol examination, and troubleshooting techniques essential for penetration testing, incident response, and network defense.

## **Required Resources**
- Kali Linux virtual machine (VM).
- Internet access.
- Additional virtual machines or network segments (recommended).

---

## **Instructions**

### **Part 1: Comprehensive Network Discovery**

#### **Step 1: Advanced Interface Analysis**
```bash
# Display all network interfaces with detailed information
ip addr show
ip link show
ip -s link show eth0

# Show network statistics
ss -tuln
netstat -i
cat /proc/net/dev
```

**Exercise 1.1:** What is the difference between `ss` and `netstat`? Which provides more detailed information?

#### **Step 2: Network Configuration Management**
```bash
# Create a virtual interface for testing
sudo ip link add veth0 type veth peer name veth1
sudo ip addr add 10.0.1.1/24 dev veth0
sudo ip addr add 10.0.1.2/24 dev veth1
sudo ip link set veth0 up
sudo ip link set veth1 up

# Verify the configuration
ip addr show veth0
ip addr show veth1
```

**Exercise 1.2:** Test connectivity between the virtual interfaces using `ping`.

#### **Step 3: Advanced Routing Analysis**
```bash
# Display detailed routing information
ip route show table all
ip rule show

# Add a custom routing table
echo "200 custom" | sudo tee -a /etc/iproute2/rt_tables
sudo ip route add 192.168.100.0/24 dev eth0 table custom
sudo ip rule add from 192.168.1.100 table custom
```

### **Part 2: Advanced Connectivity Testing**

#### **Step 1: Comprehensive Ping Techniques**
```bash
# Ping with specific interface
ping -I eth0 google.com

# Ping with specific TTL
ping -t 10 google.com

# Flood ping for stress testing
ping -f -c 1000 localhost

# IPv6 testing
ping6 -c 4 ipv6.google.com
```

**Exercise 2.1:** What happens when you use flood ping, and why is it useful for network testing?

#### **Step 2: Advanced Traceroute Methods**
```bash
# Traceroute with different protocols
traceroute -T google.com
traceroute -U google.com
traceroute -I google.com

# Traceroute with specific port
traceroute -T -p 443 google.com

# MTR - combination of ping and traceroute
sudo apt install mtr
mtr google.com
```

#### **Step 3: Path Analysis and MTU Discovery**
```bash
# Find maximum MTU to a host
ping -M do -s 1500 -c 1 google.com
ping -M do -s 1472 -c 1 google.com

# Tracepath for MTU discovery
tracepath google.com
```

### **Part 3: Network Service Analysis**

#### **Step 1: Port and Service Scanning**
```bash
# Comprehensive port scanning with netcat
nc -zv google.com 80
nc -zv google.com 22

# Multiple port scanning
nc -zv google.com 20-80

# Service version detection
nc -v google.com 80
```

#### **Step 2: Banner Grabbing and Service Identification**
```bash
# HTTP banner grabbing
echo "HEAD / HTTP/1.0\r\n\r\n" | nc google.com 80

# SSH version detection
nc google.com 22

# SMTP banner
nc gmail-smtp-in.l.google.com 25
```

**Exercise 3.1:** What information can you gather from service banners that might be useful for security assessment?

### **Part 4: Advanced Traffic Analysis**

#### **Step 1: Comprehensive Packet Capture**
```bash
# Capture on specific interface with verbose output
sudo tcpdump -i eth0 -vvv

# Capture and display in HEX and ASCII
sudo tcpdump -i eth0 -XX

# Capture specific protocol
sudo tcpdump -i eth0 tcp
sudo tcpdump -i eth0 udp
sudo tcpdump -i eth0 icmp

# Capture to file for later analysis
sudo tcpdump -i eth0 -w capture.pcap
```

#### **Step 2: Advanced tcpdump Filters**
```bash
# Capture specific host
sudo tcpdump -i eth0 host 8.8.8.8

# Capture specific port
sudo tcpdump -i eth0 port 80

# Capture traffic between specific hosts
sudo tcpdump -i eth0 host 192.168.1.10 and host 192.168.1.20

# Capture all HTTP traffic
sudo tcpdump -i eth0 -A tcp port 80
```

**Exercise 4.1:** Create a tcpdump filter to capture only DNS queries and responses.

#### **Step 3: Real-time Traffic Analysis**
```bash
# Monitor bandwidth usage by interface
iftop -i eth0

# Monitor connections in real-time
nethogs

# Comprehensive network monitoring
sudo apt install bmon
bmon
```

### **Part 5: DNS and Name Resolution**

#### **Step 1: DNS Analysis Tools**
```bash
# Basic DNS lookup
nslookup google.com
dig google.com

# Reverse DNS lookup
dig -x 8.8.8.8

# Query specific DNS server
dig @8.8.8.8 google.com

# Comprehensive DNS information
dig google.com ANY
```

#### **Step 2: DNS Troubleshooting**
```bash
# Trace DNS resolution path
dig +trace google.com

# Check DNS response times
dig google.com | grep "Query time"

# Test DNS over TCP
dig +tcp google.com
```

**Exercise 5.1:** Compare the response times between your local DNS resolver and Google's public DNS (8.8.8.8).

### **Part 6: Network Security Analysis**

#### **Step 1: Firewall and Security Assessment**
```bash
# Check iptables rules
sudo iptables -L -v -n

# Check for listening services
sudo netstat -tulpn
sudo ss -tulpn

# Monitor connection attempts
sudo tcpdump -i eth0 'tcp[tcpflags] & (tcp-syn) != 0'
```

#### **Step 2: ARP Analysis and Spoofing Detection**
```bash
# View ARP table
arp -a
ip neighbor show

# Monitor ARP traffic
sudo tcpdump -i eth0 -n arp

# Detect ARP spoofing
sudo arpwatch -i eth0
```

### **Part 7: Performance and Load Testing**

#### **Step 1: Bandwidth Testing**
```bash
# Install network testing tools
sudo apt install iperf3 speedtest-cli

# Test download speed
speedtest-cli

# Set up iperf3 server (on another machine)
iperf3 -s

# Test bandwidth to server
iperf3 -c server_ip
```

#### **Step 2: Network Stress Testing**
```bash
# Generate network load
sudo apt install stress-ng
stress-ng --udp 4 --udp-port 5000 --timeout 60s

# Monitor during stress test
iftop -i eth0
```

### **Part 8: Wireless Network Analysis**

#### **Step 1: Wireless Interface Management**
```bash
# Check wireless capabilities
sudo iw list

# Scan for wireless networks
sudo iw dev wlan0 scan | grep SSID

# Monitor mode setup
sudo ip link set wlan0 down
sudo iw dev wlan0 set type monitor
sudo ip link set wlan0 up
```

## **Challenge Exercises**

**Challenge 1: Network Mapping**
- Create a complete map of your local network
- Identify all active hosts and their open ports
- Document services running on each host
- Time limit: 30 minutes

**Challenge 2: Traffic Analysis**
- Capture 5 minutes of network traffic
- Identify the top 5 protocols in use
- Find any plaintext credentials transmitted
- Generate a traffic analysis report

**Challenge 3: DNS Investigation**
- Map the DNS infrastructure of a large organization
- Identify all authoritative name servers
- Check for DNS security misconfigurations
- Document your findings

**Challenge 4: Network Troubleshooting Scenario**
```bash
# Simulate a network issue
sudo iptables -A OUTPUT -p tcp --dport 80 -j DROP

# Troubleshoot and identify the problem
# Document your troubleshooting methodology
```

## **Advanced Tools Installation**

```bash
# Install comprehensive networking toolkit
sudo apt install \
    wireshark \
    tshark \
    nmap \
    hping3 \
    dnsutils \
    net-tools \
    tcpdump \
    iperf3 \
    iftop \
    nethogs \
    mtr \
    arp-scan \
    ettercap-text-only \
    dsniff
```

## **Troubleshooting Common Network Issues**

1. **Interface Won't Come Up**
   ```bash
   sudo ip link set eth0 up
   sudo dhclient eth0
   journalctl -u NetworkManager
   ```

2. **DNS Resolution Problems**
   ```bash
   systemctl status systemd-resolved
   cat /etc/resolv.conf
   dig @1.1.1.1 google.com
   ```

3. **Routing Issues**
   ```bash
   ip route get 8.8.8.8
   traceroute 8.8.8.8
   ping -R 8.8.8.8
   ```

## **Conclusion**
You have now mastered advanced network analysis and troubleshooting techniques essential for security professionals. These skills enable you to conduct thorough network assessments, identify security issues, and maintain robust network infrastructure.

## **Additional Resources**
- **Wireshark Documentation**: https://www.wireshark.org/docs/
- **tcpdump Manual**: https://www.tcpdump.org/manpages/tcpdump.1.html
- **Nmap Network Scanning**: https://nmap.org/book/
- **Linux Network Administrator's Guide**: https://tldp.org/LDP/nag2/index.html
