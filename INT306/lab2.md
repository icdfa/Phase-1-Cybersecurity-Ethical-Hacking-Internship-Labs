# INT306: Cryptography – Lab 2: Post-Quantum Cryptography (PQC) and Future-Proofing Security

---

## **Author: AMINU IDRIS, AMCPN**

---

## **Overview**

This laboratory session provides a pioneering and hands-on exploration of Post-Quantum Cryptography (PQC), the next frontier in digital security. As quantum computing technology advances, traditional cryptographic algorithms like RSA and ECC face an existential threat from Shor's and Grover's algorithms. This lab introduces students to the quantum-resistant algorithms recently standardized by NIST, including ML-KEM (Kyber), ML-DSA (Dilithium), and SLH-DSA (SPHINCS+). Utilizing the Open Quantum Safe (OQS) project within a Kali Linux environment, students will learn to implement, manage, and evaluate these future-proof cryptographic solutions. This lab is designed to equip students with the advanced skills necessary to navigate the transition to a quantum-safe digital landscape.

---

## **Learning Outcomes**

Upon successful completion of this lab, students will be able to:

1.  **Understand the Quantum Threat:** Articulate how quantum computers threaten current asymmetric cryptography (RSA, ECC) and the role of Shor's and Grover's algorithms.
2.  **Identify NIST PQC Standards:** Recognize and differentiate between the primary NIST-standardized PQC algorithms: ML-KEM (Kyber), ML-DSA (Dilithium), and SLH-DSA (SPHINCS+).
3.  **Implement PQC with OpenSSL:** Utilize the `oqs-provider` for OpenSSL 3.x to generate quantum-resistant keys and perform cryptographic operations.
4.  **Execute PQC Digital Signatures:** Implement and verify digital signatures using ML-DSA (Dilithium) to ensure authenticity in a post-quantum world.
5.  **Perform PQC Key Encapsulation (KEM):** Understand and implement Key Encapsulation Mechanisms using ML-KEM (Kyber) for secure key exchange.
6.  **Analyze Hybrid Cryptography:** Comprehend the importance of hybrid cryptographic schemes that combine classical and quantum-resistant algorithms for transitional security.

---

## **1. The Quantum Threat and the Need for PQC**

### **1.1 Shor's and Grover's Algorithms**

The security of modern cryptography relies on the computational difficulty of certain mathematical problems. Quantum computers, however, can solve these problems exponentially faster:

*   **Shor's Algorithm:** Can efficiently factor large integers (breaking RSA) and solve discrete logarithm problems (breaking ECC and Diffie-Hellman). This renders almost all current public-key cryptography obsolete.
*   **Grover's Algorithm:** Provides a quadratic speedup for searching unstructured databases. This effectively halves the security level of symmetric ciphers (e.g., AES-256 becomes as strong as AES-128).

### **1.2 NIST PQC Standardization**

To mitigate this threat, the National Institute of Standards and Technology (NIST) initiated a global effort to standardize quantum-resistant algorithms. In August 2024, the first three standards were finalized [1]:

| NIST Standard | Original Algorithm | Purpose | Mathematical Basis |
| :--- | :--- | :--- | :--- |
| **FIPS 203 (ML-KEM)** | CRYSTALS-Kyber | Key Encapsulation (KEM) | Module Lattice-Based |
| **FIPS 204 (ML-DSA)** | CRYSTALS-Dilithium | Digital Signatures | Module Lattice-Based |
| **FIPS 205 (SLH-DSA)** | SPHINCS+ | Digital Signatures | Stateless Hash-Based |

---

## **2. Practical Exercises in Kali Linux: Post-Quantum Implementation**

**Note:** These exercises utilize the **Open Quantum Safe (OQS)** project. Students should ensure their Kali Linux environment is updated and has OpenSSL 3.x installed.

### **Exercise 2.1: Setting Up the OQS Environment**

The `oqs-provider` allows OpenSSL to support PQC algorithms. This exercise involves configuring the environment to use these new capabilities.

**Objective:** To enable PQC support in OpenSSL using the OQS provider.

**Task:**

1.  **Verify OpenSSL Version:**
    *   Ensure you are running OpenSSL 3.0 or higher.

    ```bash
    openssl version
    ```

2.  **Explore OQS Capabilities (Conceptual):**
    *   The `oqs-provider` is a module that plugs into OpenSSL. Research how "Providers" in OpenSSL 3.x allow for modular cryptographic extensions [2].
    *   **Question:** Why is the "Provider" architecture in OpenSSL 3.x significant for the transition to Post-Quantum Cryptography?

### **Exercise 2.2: Generating PQC Key Pairs**

In this exercise, you will generate key pairs for the new NIST standards: ML-KEM (for key exchange) and ML-DSA (for signatures).

**Objective:** To generate and examine quantum-resistant key pairs.

**Task:**

1.  **Generate an ML-KEM (Kyber-768) Key Pair:**
    *   Kyber-768 provides security roughly equivalent to AES-192.

    ```bash
    # Note: Algorithm names in OQS may vary slightly (e.g., kyber768)
    openssl genpkey -algorithm kyber768 -out pqc_kem_private.pem
    openssl pkey -in pqc_kem_private.pem -pubout -out pqc_kem_public.pem
    ```

2.  **Generate an ML-DSA (Dilithium3) Key Pair:**
    *   Dilithium3 is the standard for digital signatures.

    ```bash
    openssl genpkey -algorithm dilithium3 -out pqc_sig_private.pem
    openssl pkey -in pqc_sig_private.pem -pubout -out pqc_sig_public.pem
    ```

3.  **Examine Key Characteristics:**
    *   Use `ls -lh` to compare the sizes of PQC keys with traditional RSA/ECC keys.
    *   **Question:** Notice the significantly larger size of PQC keys compared to ECC. Discuss the potential impact of these larger keys on network protocols like TLS and IKEv2.

### **Exercise 2.3: PQC Digital Signatures with ML-DSA**

This exercise demonstrates the use of ML-DSA (Dilithium) to sign and verify a document, ensuring its authenticity in a post-quantum world.

**Objective:** To perform quantum-resistant digital signing and verification.

**Task:**

1.  **Create a Document to Sign:**

    ```bash
    echo "This message is protected by NIST-standardized Post-Quantum Cryptography." > pqc_message.txt
    ```

2.  **Sign the Document using ML-DSA:**
    *   Use the `pqc_sig_private.pem` to sign the message.

    ```bash
    openssl dgst -sign pqc_sig_private.pem -out pqc_message.sig pqc_message.txt
    ```

3.  **Verify the Signature:**
    *   Use the `pqc_sig_public.pem` to verify the signature.

    ```bash
    openssl dgst -verify pqc_sig_public.pem -signature pqc_message.sig pqc_message.txt
    ```

    *   **Expected Output:** `Verified OK`
    *   **Question:** Explain the mathematical problem (Module Learning with Errors - MLWE) that provides the security foundation for ML-DSA. How does it differ from the factoring problem used in RSA?

### **Exercise 2.4: Key Encapsulation (KEM) with ML-KEM**

Key Encapsulation Mechanisms (KEM) are used to securely establish a shared symmetric key between two parties. This exercise simulates a PQC key exchange.

**Objective:** To understand and implement the KEM workflow using ML-KEM (Kyber).

**Task:**

1.  **Simulate Key Encapsulation:**
    *   In a real scenario, the sender uses the recipient's public key to "encapsulate" a secret.

    ```bash
    # This command generates a shared secret and an encapsulated key (ciphertext)
    openssl pkeyutl -derive -pubin -inkey pqc_kem_public.pem -out shared_secret.bin -peerout encapsulated_key.bin
    ```

2.  **Simulate Key Decapsulation:**
    *   The recipient uses their private key to "decapsulate" the secret from the received ciphertext.

    ```bash
    openssl pkeyutl -derive -inkey pqc_kem_private.pem -peerkey encapsulated_key.bin -out recovered_secret.bin
    ```

3.  **Verify the Shared Secret:**
    *   Compare `shared_secret.bin` and `recovered_secret.bin`. They should be identical.

    ```bash
    diff shared_secret.bin recovered_secret.bin
    ```

    *   **Question:** Why is a Key Encapsulation Mechanism (KEM) preferred over traditional Diffie-Hellman (DH) for many post-quantum lattice-based algorithms?

---

## **3. Hybrid Cryptography and Migration Strategies**

### **Exercise 3.1: The Hybrid Approach (Conceptual)**

During the transition period, "Hybrid Cryptography" is recommended. This involves using both a classical algorithm (like X25519) and a PQC algorithm (like Kyber) together. If either is broken, the communication remains secure as long as the other holds.

**Objective:** To understand the importance of hybrid schemes for transitional security.

**Task:**

1.  **Research Hybrid Key Exchange:**
    *   Investigate how Google and Cloudflare are implementing hybrid key exchange (e.g., X25519 + Kyber) in Chrome and their networks [3].
    *   **Question:** What are the primary benefits and drawbacks of using hybrid cryptography instead of switching entirely to PQC immediately?

### **Exercise 3.2: Crypto-Agility and Inventory**

Transitioning to PQC requires "Crypto-Agility"—the ability of a system to easily switch between cryptographic algorithms.

**Objective:** To analyze the requirements for a successful PQC migration.

**Task:**

1.  **Cryptographic Inventory:**
    *   Imagine you are the CISO of a mid-sized organization. List the systems and protocols in your environment that would need to be updated to be quantum-safe (e.g., VPNs, Web Servers, SSH, Internal CAs).
    *   **Question:** Discuss the concept of "Harvest Now, Decrypt Later" (HNDL) attacks. Why does this threat make the transition to PQC urgent even before a cryptographically relevant quantum computer (CRQC) exists?

---

## **Conclusion**

This lab has provided a comprehensive and forward-looking exploration of Post-Quantum Cryptography (PQC). By engaging with the new NIST standards (ML-KEM and ML-DSA) through hands-on exercises in Kali Linux, students have gained a practical understanding of how to secure digital assets against the future threat of quantum computing. The lab covered key generation, digital signatures, and key encapsulation, while also emphasizing the critical importance of hybrid cryptography and crypto-agility during this global transition. Mastering these advanced concepts is essential for any cybersecurity professional aiming to lead in the next era of digital security and ensure the long-term confidentiality and integrity of information.

---

## **References**

[1] NIST. (2024). *NIST Releases First Three Finalized Post-Quantum Cryptography Standards*. Retrieved from https://www.nist.gov/news-events/news/2024/08/nist-releases-first-three-finalized-post-quantum-cryptography-standards
[2] OpenSSL Project. (n.d.). *OpenSSL 3.0 Design Document: Providers*. Retrieved from https://www.openssl.org/docs/man3.0/man7/provider.html
[3] Cloudflare. (2023). *Defending against the quantum threat: Cloudflare's journey to post-quantum cryptography*. Retrieved from https://blog.cloudflare.com/post-quantum-cryptography/
[4] Open Quantum Safe Project. (n.d.). *OQS Provider for OpenSSL 3*. Retrieved from https://github.com/open-quantum-safe/oqs-provider

---

