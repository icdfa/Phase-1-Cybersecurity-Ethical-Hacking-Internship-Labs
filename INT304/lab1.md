## **INT304: Network Security and Protocols – Lab 1: Applied Network Security Analysis**

### **Objectives**

The primary objectives of this lab are to move beyond theoretical concepts and apply fundamental network security principles to a high-profile, real-world incident. Upon completion of this lab, students will be able to:

1.  **Analyze** a contemporary cyber-attack scenario to identify the root causes of network security failure.
2.  **Correlate** specific network threats and vulnerabilities with the exploited weaknesses in the scenario.
3.  **Evaluate** the role of security protocols (or the absence thereof) in the attack's success.
4.  **Formulate** a research-backed, comprehensive mitigation strategy to prevent recurrence.

---

### **Research Scenario: The Colonial Pipeline Ransomware Attack (2021)**

In May 2021, the Colonial Pipeline, a major fuel pipeline system in the United States, was forced to shut down its operations due to a **ransomware attack** executed by the cybercriminal group DarkSide. The attack significantly disrupted fuel supplies across the Southeastern U.S., highlighting the critical intersection of network security and national infrastructure.

Initial reports indicated that the attackers gained access to Colonial Pipeline's network through a compromised Virtual Private Network (VPN) account that was not protected by multi-factor authentication (MFA). The attack primarily targeted the company's business network, but the operational technology (OT) network was shut down as a precautionary measure, demonstrating the cascading effects of a network security breach.

---

### **Lab Task: Incident Analysis and Mitigation Proposal**

Your task is to act as a cybersecurity incident response analyst. You must conduct independent research on the Colonial Pipeline attack and prepare a detailed report that addresses the following three key areas:

#### **Part 1: Attack Vector and Vulnerability Identification**

Based on your research, identify and describe:

1.  **The Initial Attack Vector:** How did the DarkSide group first gain unauthorized access to Colonial Pipeline's network?
2.  **The Key Vulnerability:** What specific network security vulnerability (e.g., weak authentication, unpatched software, lack of segmentation) was exploited to facilitate the breach?
3.  **The Threat Type:** Categorize the attack based on the network security threats discussed in class (e.g., DoS, MitM, Ransomware, Phishing). Justify your categorization.

#### **Part 2: Protocol Failure and Relevance**

Analyze the role of network security protocols in this incident:

1.  **Authentication Protocol Failure:** Discuss the failure of the authentication mechanism (or lack of a robust one) on the compromised VPN account. How would a protocol like **Multi-Factor Authentication (MFA)** have prevented the initial breach?
2.  **Network Segmentation:** Research and discuss the concept of **network segmentation** (e.g., separating IT and OT networks). How did the lack of effective segmentation contribute to the overall impact of the attack, even if the OT network was not directly compromised?
3.  **Encryption Protocols:** Were protocols like **SSL/TLS** or **IPSec** relevant to the initial breach? Explain why or why not.

#### **Part 3: Mitigation Strategy**

Propose a three-point, research-backed mitigation strategy for Colonial Pipeline to prevent a similar incident in the future. For each point, you must:

1.  **Identify** a specific security control or technology (e.g., a specific protocol, a new policy, a hardware solution).
2.  **Explain** how it directly addresses a vulnerability exploited in the 2021 attack.
3.  **Provide** a brief justification for its inclusion, citing best practices in the industry.

---

### **Deliverables**

Submit a formal report (minimum 1,000 words) in a professional document format that includes:

*   A title page with your name, student ID, course, and date.
*   An executive summary of your findings.
*   Detailed sections addressing all points in **Part 1, Part 2, and Part 3** of the Lab Task.
*   A **References** section citing all sources used for your research.

### **Deadline**

The report should be submitted by the specified due date, which will be communicated by your instructor.
