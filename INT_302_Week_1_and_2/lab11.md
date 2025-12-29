

## **INT302: Kali Linux Tools and System Security – Lab 11: Anonymity Testing with Tor and Proxychains**

---

## **Lab Overview**

This lab focuses on **anonymity testing and verification** using **Tor** and **Proxychains**. Students will configure Tor-based proxy routing, verify IP address masking, observe Tor circuit behavior, and evaluate the effectiveness and limitations of anonymity mechanisms used during security assessments and penetration testing activities.

Rather than simple usage, this lab emphasizes **proof of anonymity**, **traffic routing validation**, and **operational limitations**.

---

## **Lab Objectives**

By the end of this lab, you will be able to:

1. Explain how Tor provides anonymity through onion routing.
2. Configure Proxychains to route traffic through the Tor network.
3. Verify anonymity by comparing real IP addresses with Tor exit node IPs.
4. Analyze Tor circuit persistence and IP rotation behavior.
5. Identify limitations and risks of using Tor and Proxychains during security testing.

---

## **Tools Used**

* **Tor** – Provides anonymity via onion routing and Tor exit nodes.
* **Proxychains-ng** – Forces applications to route traffic through Tor (SOCKS5).
* **Curl** – Used for IP and traffic verification.
* **Firefox (optional)** – For browser-based IP verification.

---

## **Prerequisites**

* Basic knowledge of IP addressing and TCP/IP networking
* Familiarity with Linux terminal usage
* Kali Linux environment with internet access

---

## **Lab Steps**

---

## **Step 1: Installing Required Tools**

1. **Update System Packages**

```bash
sudo apt update
```

2. **Install Tor**

```bash
sudo apt install tor -y
```

3. **Install Proxychains**

```bash
sudo apt install proxychains -y
```

---

## **Step 2: Configuring and Starting Tor**

1. **Start the Tor Service**

```bash
sudo service tor start
```

2. **Verify Tor Status**

```bash
systemctl status tor
```

**Exercise 1**

* Record the Tor service status output.
* Is the Tor service running successfully?

---

---

## **Step 3: Configuring Proxychains for Anonymity**

1. **Edit Proxychains Configuration**

```bash
sudo nano /etc/proxychains.conf
```

2. **Apply the Following Settings**
   Ensure the configuration includes:

```ini
strict_chain
proxy_dns
tcp_read_time_out 15000
tcp_connect_time_out 8000

[ProxyList]
socks5 127.0.0.1 9050
```

> **Note:**
> `strict_chain` ensures traffic must pass through Tor.
> `proxy_dns` prevents DNS leaks.

**Exercise 2**

* Explain the difference between `strict_chain`, `dynamic_chain`, and `random_chain`.

---

---

## **Step 4: Baseline IP Address Identification (Non‑Anonymous)**

1. **Check Your Real IP Address**

```bash
curl https://httpbin.org/ip
```

2. **Record the IP Address**

```
"origin": _____________________
```

**Exercise 3**

* Is this IP associated with your ISP or local network?

---

---

## **Step 5: Anonymity Verification Using Proxychains**

1. **Test Anonymous Connection**

```bash
proxychains curl https://httpbin.org/ip
```

2. **Observe the Output**
   Example:

```json
{
  "origin": "185.183.159.40"
}
```

**Exercise 4**

* Compare this IP with your real IP from Step 4.
* Is the IP different?
* What does this confirm about your anonymity?

---

---

## **Step 6: Tor Circuit Persistence and IP Behavior**

1. **Repeat the Command Multiple Times**

```bash
proxychains curl https://httpbin.org/ip
```

2. **Observe Whether the IP Changes**

**Exercise 5**

* Did the IP address remain the same or change?
* What does this indicate about Tor circuit reuse?

---

---

## **Step 7: Forcing a New Tor Identity (Optional Advanced Test)**

1. **Restart Tor**

```bash
sudo service tor restart
```

2. **Re-test IP Address**

```bash
proxychains curl https://httpbin.org/ip
```

**Exercise 6**

* Did the Tor exit IP change after restarting Tor?
* Why is IP rotation not guaranteed on every request?

---

---

## **Step 8: Browser-Based Anonymity Testing (Optional)**

1. **Launch Firefox Through Proxychains**

```bash
proxychains firefox
```

2. **Visit an IP Check Website**

* [https://www.whatismyip.com/](https://www.whatismyip.com/)

**Exercise 7**

* Does the browser show the same Tor exit IP as the curl test?
* Why is consistency important in anonymity testing?

---

---

## **Step 9: Anonymity vs. Functionality Trade‑Off**

1. **Optional Tool Test**

```bash
proxychains nmap -sT -Pn <target-ip>
```

**Exercise 8**

* What limitations did you experience when routing scans through Tor?
* Why is Tor unsuitable for certain types of active scanning?

---

---

## **Step 10: Risk and Limitation Analysis**

**Exercise 9**
Answer the following:

* What are the risks of Tor exit nodes?
* How can DNS leaks compromise anonymity?
* Why should Tor not be used for authenticated personal accounts?

---

---

## **Conclusion**

In this lab, you performed **practical anonymity testing** using Tor and Proxychains. You verified IP masking, analyzed Tor circuit behavior, evaluated IP persistence, and identified real‑world limitations of anonymous routing. These skills are essential for ethical hackers, digital forensic analysts, and privacy‑focused security professionals.

---

## **Deliverables**

Students must submit:

* Screenshots of IP comparison results
* Answers to all exercises
* A brief summary explaining whether anonymity was successfully achieved and why

---

## **Next Lab**

The next lab will focus on **web traffic interception and anonymity risks** using tools such as **Burp Suite** and **OWASP ZAP**.

---

