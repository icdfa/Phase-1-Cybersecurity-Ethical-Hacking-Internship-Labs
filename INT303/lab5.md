### **INT303: Networking Fundamentals – Lab 5**

---

#### **Lab 5: IP Address Analysis and Network Report**

---

#### **Objective:**
This lab aims to deepen your understanding of IP addressing, network scalability, and subnetting. You will analyze real-world websites, classify IP addresses, calculate device capacities, determine subnet masks, and perform advanced IP operations. Additionally, you will compile a detailed report showcasing your findings and understanding of IP networking.

---

#### **Learning Outcomes:**
Upon completing this lab, you will:
- Master IP address classification.
- Calculate the number of devices supported by each class of IP address.
- Identify and work with subnet masks.
- Gain experience with both basic and advanced IP tools.
- Develop a comprehensive network report.
- Learn hands-on exercises with advanced concepts like subnetting, network summarization, and IP analysis.

---

#### **Instructions:**

### **Step 1: Select 10 Websites**
1. Choose **10 popular websites** (e.g., `apple.com`, `twitter.com`, etc.) to analyze.

2. **Bonus Exercise:** Include a variety of domains, such as

```bash
.com
```


---

### **Step 2: Ping the Websites**
2. Use the **ping** command in your terminal to retrieve the IP addresses of each website.

   - **Example Command:**
     ```
     ping apple.com
     ```

3. **Bonus Exercise:** Identify if the website resolves to multiple IP addresses (i.e., if it uses a content delivery network or load balancing). Record multiple IPs where applicable and compare the geographical locations of each.

---

### **Step 3: Document the IP Addresses**
3. Create a table to record the IP addresses for each website you ping.

---

### **Step 4: Classify the IP Addresses**
4. Determine the **class** (A, B, or C) of each IP address based on its first octet.

   - **Bonus Exercise:**
     - Research the reserved IP ranges (e.g., private IP ranges like 10.0.0.0/8) and see if any of your IP addresses fall into these special ranges.
     - Discuss the importance of these reserved IPs in network configurations.

---

### **Step 5: Calculate the Number of Devices Each IP Can Support**
5. For each IP class, calculate how many devices the network can accommodate. This will give you an understanding of network size and scalability.

   - **Device Capacity Formula:**
- **Class A:**

```bash
2^24
```

- **Class B:**

```bash
2^16
```

- **Class C:**

```bash
2^8
```


   - **Bonus Exercise:**
     - Calculate the actual number of usable hosts by performing subnetting on these networks. For instance, consider subdividing a Class B network into smaller subnets and calculate the device capacity for each subnet.
- Consider subnet masks like

```bash
/26
```


---

### **Step 6: Determine the Subnet Mask**
6. Identify the **default subnet mask** for each IP address based on its class.

   - **Bonus Exercise:**
     - Explore scenarios where custom subnetting is required (e.g., for network segmentation). How does altering the subnet mask affect the device capacity and overall network organization?
     - Try experimenting with subnet masks like `/25`, `/27`, and explain the difference in the number of networks and hosts.

---

### **Step 7: Advanced IP Tools (Bonus Exercises)**

- **Traceroute (Network Path Analysis):**
   Use `traceroute` (Linux/Mac) or `tracert` (Windows) to discover the network path between your system and one of the websites.
   ```
   traceroute apple.com
   ```
   - **Analyze the hops** between your system and the destination. Identify the location and IP address of each hop.
   - **Bonus:** Explain the significance of each hop, and analyze if any of them belong to private networks or are hosted on cloud infrastructure.

- **GeoIP Location:**
   Use online tools like **IPinfo.io** or **GeoIP** to check the geographical location of the IP addresses.
   - Identify if the IP addresses belong to data centers, ISPs, or any specific regions.
   - **Bonus:** Compare the latency (ping time) with the geographic distance.

---

### **Step 8: Compile a Professional Report**
Create a report that includes the following sections:

1. **Introduction:**
   - Outline the purpose of the lab, your objectives, and the significance of IP address analysis and subnetting.

2. **Website List and IP Addresses:**
   - Present the list of websites and their corresponding IP addresses.

3. **IP Address Classification:**
   - Classify each IP address and explain the method used for classification (Class A, B, or C). Discuss the characteristics of each class and their practical applications.

4. **Number of Devices Supported:**
   - Present your device capacity calculations for each IP address. Include a detailed explanation of how the number of devices is determined based on the IP class and subnetting.

5. **Subnet Masks:**
   - List the subnet masks for each IP address and discuss any custom subnetting scenarios.

6. **Advanced Tools and Analysis (Optional):**
   - Present your findings from the traceroute, GeoIP analysis, and any other advanced IP tools you explored. Discuss how these tools can be applied in network troubleshooting, performance optimization, or security audits.

7. **Conclusion:**
   - Summarize your findings and reflect on the importance of IP address management, subnetting, and network scalability in real-world networking.

---

### **Reflection:**
This lab provides a comprehensive understanding of IP address analysis, subnetting, and the usage of advanced network tools. By working with real-world data, you'll gain practical skills applicable to network configuration, security auditing, and system administration. Compiling the information into a professional report will further enhance your technical documentation skills.

---

#### **Additional Exercises for Further Practice:**
- **Subnetting Challenge:** For each IP address you pinged, create multiple subnets and calculate the network address, first usable IP, last usable IP, and broadcast address.
- **IP Address Conflict Detection:** Simulate a scenario where IP address conflicts occur within a network and outline troubleshooting steps.
- **Ping Flood Analysis:** Use tools like

```bash
hping3
```


---
