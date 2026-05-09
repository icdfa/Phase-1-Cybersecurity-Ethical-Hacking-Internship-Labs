# **INT308 Session Management and Web Security CTF Challenge: Session Hijacking Test on OWASP Juice Shop**

### **Course Title**: INT308 - Session Management and Web Security  
### **Challenge Title**: Testing for Session Hijacking on OWASP Juice Shop  
### **Submission Format**: PDF Report (Max 5MB)  
### **Weight**: 35%  

---

### **Objective**
The objective of this CTF challenge is to enhance your practical skills in identifying and exploiting session hijacking vulnerabilities. You will use a deliberately vulnerable web application, OWASP Juice Shop, to attempt to detect and exploit potential session hijacking issues.

---

### **Challenge Overview**

**1. Understanding Session Hijacking**
   - **Research**: Start by reviewing concepts of session hijacking, focusing on how attackers exploit weaknesses in web session management. Understand the tools and methods commonly used to detect session-related vulnerabilities.

**2. Test Setup**
   - **Access**: Deploy or access an instance of OWASP Juice Shop (e.g., via Docker, Heroku, or a local installation).
   - **Observation**: Use browser Developer Tools, Burp Suite, or OWASP ZAP to observe session cookies and their management in your browser.

**3. Session Hijacking Attempt**
   - **Simulate an Attack**: Utilize the knowledge gained to simulate a session hijacking attack on your own session within the Juice Shop environment. Use tools like Wireshark to monitor session traffic, intercept cookies, or test session expiration scenarios.
   - **Key Focus Areas**:
     - **Session ID Predictability**: Investigate if the session ID can be easily guessed or regenerated.
     - **Session Fixation**: Test whether you can set a user's session ID before login and hijack the session.
     - **Session Expiration**: Confirm if the session terminates correctly after logout or inactivity.
     - **Transport Security**: Evaluate if session tokens are transmitted securely (via HTTPS).

**4. Defense Mechanisms**
   - **Identify Vulnerabilities**: After testing, propose practical countermeasures to prevent session hijacking attacks. This may include enhancing session management, adjusting cookie attributes, or implementing encryption.

---

### **Submission Requirements**

You are expected to submit a well-documented report in PDF format (maximum 5MB) containing the following sections:

1. **Introduction**
   - Provide an overview of session hijacking, its potential impact on security, and the significance of protecting against such vulnerabilities.

2. **Methodology**
   - Describe the approach taken to test for session hijacking vulnerabilities on the OWASP Juice Shop platform.
   - List any tools used during testing (e.g., Wireshark, Burp Suite, Developer Tools) and the environment setup.

3. **Findings**
   - Document any vulnerabilities or weaknesses identified during the session hijacking test.
   - Include relevant screenshots to illustrate key steps and findings.

4. **Countermeasures**
   - Recommend how session management on the platform can be improved to mitigate the risks of session hijacking.

5. **Conclusion**
   - Summarize the importance of securing web sessions and the lessons learned during this challenge.

---

### **Important Notes**

- **Ethics & Authorization**: This challenge is for educational purposes only. You are permitted to perform these tests only on your own instance of OWASP Juice Shop. Attacking public instances or other users’ sessions without their consent violates ethical hacking principles.
  
- **Professionalism**: Ensure your report is professional and well-structured, following the provided format. Points will be awarded for thoroughness, clarity, and adherence to ethical guidelines.

- **Tools**: You may use open-source tools like OWASP ZAP, Burp Suite, Wireshark, or browser Developer Tools. Avoid actions that could harm or disrupt normal operations of any shared environments.

---

### **Submission Guidelines**

- Submit your report via the course assignment portal. Title your PDF with your full name and student ID (e.g., JohnDoe_12345_SessionHijackingCTF.pdf).
- Ensure your file does not exceed 5MB and contains all relevant screenshots and documentation.

---

### **Grading Criteria**

| CRITERIA                       | WEIGHTING |
|--------------------------------|-----------|
| Introduction & Background      | 05%       |
| Methodology                    | 05%       |
| Findings                       | 10%       |
| Recommendations                | 10%       |
| Conclusion & Presentation      | 05%       |

---

This CTF challenge is designed to develop your practical skills in identifying session hijacking vulnerabilities and deepen your understanding of web security measures. We look forward to your insights and contributions!

**Good luck, and may the best hacker win!**
