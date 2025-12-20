

### **INT303: Networking Fundamentals – Lab 4**

#### **Lab 4: Simulating Network Routing and VLAN Configuration in Linux**

---

#### **Objective:**
In this lab, students will simulate network routing and VLAN configuration using Linux-based tools. They will use the OWASP Broken Web Application VM's IP address to test connectivity and routing principles.

---

#### **Learning Outcomes:**
By the end of this lab, students will:
- Understand how to set up routing and VLANs on Linux.
- Be able to simulate network device behavior using Linux tools.
- Gain hands-on experience in network troubleshooting.
- Learn how to configure `iptables`, `ip route`, and network namespaces to manage traffic.

---

#### **Materials Needed:**
- Linux machine or VM (e.g., Ubuntu, Kali).
- OWASP Broken Web Application VM (reachable on the network).
- IP address of the OWASP Broken Web Application VM (e.g., 192.168.X.X).
- Terminal access.

---

#### **Lab Exercises:**

---

### **Exercise 1: Setting Up Static Routing in Linux**

1. **Task:** Set up static routes in Linux to simulate routing behavior. Ensure the Linux machine can route traffic to the OWASP Broken Web Application VM.

   - **Steps:**
     1. Use `ip route` to add a static route to reach the OWASP Broken Web Application VM.
     2. Ensure that your machine routes traffic correctly through the simulated network.

   - **Commands:**
     -

```bash
sudo ip route add <destination_network> via <gateway_IP> dev <interface>
```

       Example: `sudo ip route add 192.168.4.0/24 via 192.168.1.1 dev eth0`
     -

```bash
ip route show
```


   - **Verification Command:**
     -

```bash
ping <OWASP_IP>
```


2. **Question:**
   - How does static routing work on a Linux system?
   - What challenges could arise when setting up routes manually?

---

### **Exercise 2: VLAN Configuration Using Network Namespaces**

3. **Task:** Create virtual LANs (VLANs) using Linux network namespaces to segment traffic. Assign the OWASP Broken Web Application VM to a separate namespace and test connectivity between namespaces.

   - **Steps:**
     1. Create two network namespaces to simulate VLANs.
     2. Assign virtual network interfaces to each namespace.
     3. Route traffic between the namespaces.
     4. Test communication between namespaces and the OWASP Broken Web Application VM.

   - **Commands:**
     -

```bash
sudo ip netns add vlan1
```

     -

```bash
sudo ip netns add vlan2
```

     -

```bash
sudo ip link add veth1 type veth peer name veth2
```

     -

```bash
sudo ip link set veth1 netns vlan1
```

     -

```bash
sudo ip link set veth2 netns vlan2
```

     -

```bash
sudo ip netns exec vlan1 ip link set lo up
```

     -

```bash
sudo ip netns exec vlan1 ip addr add 192.168.10.1/24 dev veth1
```

     -

```bash
sudo ip netns exec vlan1 ping <OWASP_IP>
```


4. **Question:**
   - How do network namespaces simulate VLANs in Linux?
   - What are the benefits of using namespaces in network isolation?

---

### **Exercise 3: IP Address Assignment and Subnetting in Linux**

5. **Task:** Subnet your network and assign IP addresses to each namespace and the OWASP VM. Ensure the correct routing between subnets using static routes.

   - **Steps:**
     1. Subnet the given network (e.g., 192.168.0.0/24).
     2. Assign IP addresses to network namespaces and devices.
     3. Configure static routes to enable communication between the subnets.

   - **Commands:**
     -

```bash
ip addr add <subnet_IP> dev <interface>
```

     -

```bash
ip route add <subnet>
```


6. **Question:**
   - How does subnetting work in Linux environments?
   - What challenges arise when configuring subnets manually?

---

### **Exercise 4: Testing Connectivity Using Ping and Traceroute**

7. **Task:** Use `ping` and `traceroute` to test connectivity between the Linux machine, network namespaces, and the OWASP Broken Web Application VM. Analyze the routing path.

   - **Commands:**
     -

```bash
ping <OWASP_IP>
```

     -

```bash
traceroute <OWASP_IP>
```


8. **Question:**
   - What can `traceroute` reveal about network issues?
   - How does packet routing affect network performance?

---

### **Exercise 5: Configuring `iptables` for Routing and Firewall Rules**

9. **Task:** Use `iptables` to simulate a router by controlling the flow of traffic between different networks and the OWASP VM. Block certain traffic while allowing other traffic.

   - **Steps:**
     1. Enable IP forwarding on the Linux machine.
     2. Set up `iptables` rules to allow or block specific traffic between namespaces and the OWASP VM.
     3. Test the firewall by pinging the OWASP VM and other devices.

   - **Commands:**
     -

```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

     -

```bash
sudo iptables -A FORWARD -s 192.168.10.0/24 -d 192.168.20.0/24 -j ACCEPT
```

     -

```bash
sudo iptables -A FORWARD -s 192.168.10.0/24 -d <OWASP_IP> -j DROP
```


10. **Question:**
    - How can `iptables` be used to simulate routing and firewall functionality?
    - What are common mistakes when configuring `iptables` rules?

---

### **Exercise 6: Monitoring Traffic Using `tcpdump`**

11. **Task:** Use `tcpdump` to monitor traffic between your Linux namespaces and the OWASP VM. Capture and analyze packets to understand traffic flow.

   - **Commands:**
     -

```bash
sudo tcpdump -i <interface>
```

     -

```bash
sudo tcpdump -i veth1
```

     -

```bash
sudo tcpdump -i eth0 src <OWASP_IP>
```


12. **Question:**
    - How can `tcpdump` be used to diagnose network issues?
    - What types of traffic do you observe during the simulation?

---

### **Submission Requirements:**
- Submit a report including:
  - Screenshots of the static routing, namespace creation, and `iptables` configurations.
  - A brief explanation of each step and the results from `ping`, `traceroute`, and `tcpdump` commands.
  - Troubleshooting steps for any encountered issues.

---

#### **Reflection:**
This lab demonstrates how Linux-based tools can effectively simulate routing and VLAN behavior. Students gain critical insights into routing, network segmentation, and traffic control without needing physical network hardware.

---
