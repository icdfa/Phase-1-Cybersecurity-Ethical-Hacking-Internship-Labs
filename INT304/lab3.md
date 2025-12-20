Here’s Lab 3 for **INT304: Network Security and Protocols**:

---

## **INT304: Network Security and Protocols – Lab 3: Network Security Protocols and Configuration**

### **Objectives**
- Understand various network security protocols and their implementations.
- Gain hands-on experience configuring network devices with security protocols.
- Learn to analyze and verify the security configurations.

### **Lab Activities**

1. **Overview of Network Security Protocols**
   - Begin with a lecture or reading on key network security protocols such as:
     - **SSL/TLS**: Securing data in transit.
     - **IPsec**: Protecting IP packets.
     - **SSH**: Secure shell for secure remote access.
     - **VPN**: Virtual Private Network for secure connections.
     - **802.1X**: Port-based network access control.
   - Discuss the importance of each protocol in securing communications.

2. **Configuring SSL/TLS on a Web Server**
   - Set up a local web server (e.g., Apache or Nginx) on a Linux VM.
   - Obtain a self-signed SSL certificate or use a tool like Let's Encrypt for a free SSL certificate.
   - Configure the web server to support HTTPS:
     - Enable SSL/TLS.
     - Redirect HTTP traffic to HTTPS.
     - Test the configuration by accessing the web server through a web browser.

3. **Implementing IPsec VPN**
   - Set up a VPN server using software such as OpenVPN or StrongSwan.
   - Create client configurations and test connections to the VPN server.
   - Ensure secure communication between clients and the server:
     - Monitor traffic to confirm that data is encrypted.
     - Use tools like Wireshark to capture and analyze packets.

4. **Configuring SSH for Secure Remote Access**
   - Install and configure an SSH server on a Linux machine.
   - Adjust settings to enhance security:
     - Change the default port (22) to a non-standard port.
     - Disable root login.
     - Implement public key authentication instead of password-based authentication.
   - Test SSH connections from a client machine, ensuring secure access.

5. **Using 802.1X for Network Access Control**
   - Simulate a network with a switch that supports 802.1X.
   - Configure a RADIUS server to handle authentication requests.
   - Connect client devices to the network and verify that only authenticated devices can access resources.
   - Discuss potential challenges and troubleshooting methods.

6. **Verification and Testing**
   - After configuring the protocols, perform the following tests:
- Verify HTTPS using tools like

```bash
curl
```

     - Check IPsec VPN connections using ping and traceroute.
     - Validate SSH access and configuration settings.
     - Test network access with and without 802.1X authentication.

### **Deliverables**
- Submit a report (4-6 pages) that includes:
  - Configuration details for each protocol implemented.
  - Screenshots demonstrating successful connections and security verifications.
  - A summary of challenges faced during the lab and how they were resolved.

### **Deadline**
- The report should be submitted by the specified due date, which will be communicated in class.

---