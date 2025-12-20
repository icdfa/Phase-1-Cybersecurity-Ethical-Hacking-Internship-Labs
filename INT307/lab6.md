

# INT307 Web Application Security Lab 6: Insecure Direct Object References (IDOR) in DVWA

## Overview

In this lab, you will explore Insecure Direct Object References (IDOR) vulnerabilities within the Damn Vulnerable Web Application (DVWA). You will learn how these vulnerabilities can be exploited to access unauthorized data or perform unauthorized actions.

### Objectives

1. Understand what IDOR vulnerabilities are and how they can be exploited.
2. Identify IDOR vulnerabilities in DVWA.
3. Discuss mitigation strategies to prevent IDOR attacks.

### Prerequisites

- Ensure you have DVWA installed and running.
- Familiarize yourself with BurpSuite for effective testing.

---

## Exercise Instructions

### **Exercise 1: Understanding IDOR**

**Objective:** Gain an understanding of what IDOR is and how it can be exploited.

1. **Read About IDOR**: Research and understand the concept of Insecure Direct Object References (IDOR).
   - Key points to consider:
     - Definition of IDOR
     - How IDOR vulnerabilities arise
     - Real-world examples of IDOR attacks

2. **Reflection**: Write a brief summary of your findings on IDOR.

---

### **Exercise 2: Identify IDOR Vulnerabilities in DVWA**

**Objective:** Find and exploit IDOR vulnerabilities within DVWA.

1. **Access the User Information Page**:
   - Navigate to the following URL in your DVWA instance:
     - [User Info Page](http://localhost/DVWA/vulnerabilities/idor/)

2. **Check Existing User Information**:
   - Note the user ID displayed on the page (e.g., `user=1`).

3. **Manipulate the User ID**:
- Change the user ID in the URL to access different users. For example, if the URL is

```bash
http://localhost/DVWA/vulnerabilities/idor/?user=1
```


4. **Observe the Results**:
   - What information do you see when you change the user ID? Were you able to access information that should not be available to you?

5. **Reflection**:
   - Discuss the implications of IDOR vulnerabilities in this scenario.

---

### **Exercise 3: Exploit IDOR to Access Unauthorized Data**

**Objective:** Exploit the IDOR vulnerability to gain access to unauthorized user data.

1. **Attempt to Access Different User Profiles**:
   - Using the same user information page, try different user IDs in the URL to access profiles that should not be available to your logged-in user.

2. **Analyze the Response**:
   - Document any unauthorized information you were able to access through the IDOR vulnerability.

3. **Reflection**:
   - What kind of sensitive data were you able to access? Discuss the potential risks involved in this type of vulnerability.

---

### **Exercise 4: Preventing IDOR Vulnerabilities**

**Objective:** Discuss methods to mitigate IDOR vulnerabilities in web applications.

1. **Identify Mitigation Strategies**:
   - Research and list effective strategies for preventing IDOR vulnerabilities, including:
     - Access control measures
     - Using indirect object references
     - Implementing authorization checks
     - Logging and monitoring access attempts

2. **Reflection**:
   - How can these strategies be implemented in DVWA or other web applications to prevent IDOR attacks?

---

## Conclusion

In this lab, you have learned about Insecure Direct Object References (IDOR) vulnerabilities and how they can be exploited in web applications. Understanding IDOR is crucial for developing secure applications and protecting sensitive data from unauthorized access.

### Report Submission

After completing the lab exercises, submit a report summarizing your findings, including:
- The vulnerabilities identified and exploited.
- Any unauthorized data accessed.
- Recommendations for securing applications against IDOR vulnerabilities.

