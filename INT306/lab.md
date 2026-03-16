# **INT306: Cryptography – The Ultimate Lab Guide**
## **From Beginner to Expert: A Comprehensive Journey into Secure Communication**

---

### **Table of Contents**
1. [Introduction and Lab Setup](#1-introduction-and-lab-setup)
2. [Level 1: Classical Cryptography (Beginner)](#2-level-1-classical-cryptography-beginner)
3. [Level 2: Symmetric Key Cryptography (Intermediate)](#3-level-2-symmetric-key-cryptography-intermediate)
4. [Level 3: Hashing and Message Integrity (Intermediate)](#4-level-3-hashing-and-message-integrity-intermediate)
5. [Level 4: Asymmetric Key Cryptography (Advanced)](#5-level-4-asymmetric-key-cryptography-advanced)
6. [Level 5: Digital Signatures and PKI (Expert)](#6-level-5-digital-signatures-and-pki-expert)
7. [Level 6: Real-world Protocols and Advanced Topics (Expert)](#7-level-6-real-world-protocols-and-advanced-topics-expert)
8. [Level 7: Broken Crypto & Cryptanalysis (Expert)](#8-level-7-broken-crypto--cryptanalysis-expert)
9. [Level 8: Future of Cryptography (Expert)](#9-level-8-future-of-cryptography-expert)
10. [Mastery Challenge: The Cryptographic Gauntlet](#10-mastery-challenge-the-cryptographic-gauntlet)

---

### **1. Introduction and Lab Setup**

#### **Learning Outcomes**
- Understand the core pillars of cryptography: **Confidentiality, Integrity, Availability, and Non-repudiation**.
- Set up a professional cryptographic environment using **OpenSSL** and **Python**.

#### **Lab Environment**
For this lab, it is recommended to use **Kali Linux** or a standard Ubuntu environment. Ensure the following tools are installed:
- **OpenSSL**: The industry-standard toolkit for TLS and general-purpose cryptography.
- **Python 3**: With the `cryptography` and `pycryptodome` libraries.
- **GnuPG**: For PGP-related exercises.

**Installation Command (Ubuntu/Kali):**
```bash
sudo apt update && sudo apt install openssl gnupg2 python3-pip -y
pip3 install cryptography pycryptodome
```

---

### **2. Level 1: Classical Cryptography (Beginner)**

#### **2.1 The Caesar Cipher**
The Caesar cipher is a **monoalphabetic substitution cipher** where each letter is shifted by a fixed number.

**Mathematical Representation:**
- **Encryption:** `E(x) = (x + k) mod 26`
- **Decryption:** `D(x) = (x - k) mod 26`

#### **Solved Example: Caesar Cipher Decryption**
**Problem:** Decrypt the ciphertext `KHOOR` with a shift of `k = 3`.

**Solution:**
1.  **Convert letters to numbers (A=0, B=1, ..., Z=25):**
    - K=10, H=7, O=14, O=14, R=17
2.  **Apply decryption formula `D(x) = (x - 3) mod 26`:**
    - (10 - 3) mod 26 = 7 (H)
    - (7 - 3) mod 26 = 4 (E)
    - (14 - 3) mod 26 = 11 (L)
    - (14 - 3) mod 26 = 11 (L)
    - (17 - 3) mod 26 = 14 (O)
3.  **Result:** `HELLO`

#### **Exercises**
1.  **Manual Decryption:** Decrypt the ciphertext `WTAAD` using a shift of `k = 15`.
2.  **Brute Force:** You intercept the ciphertext `XAB`. Try all 25 possible shifts to find the English word.

#### **2.2 The Vigenère Cipher**
The Vigenère cipher is a **polyalphabetic substitution cipher** that uses a keyword to determine the shift for each letter.

#### **Solved Example: Vigenère Cipher Decryption**
**Problem:** Decrypt the ciphertext `RIJVS` using the key `KEY`.

**Solution:**
1.  **Repeat the key to match ciphertext length:** `KEYKE`
2.  **Align ciphertext and key:**
    ```
    Ciphertext: R I J V S
    Key:        K E Y K E
    ```
3.  **Convert letters to numbers (A=0, B=1, ..., Z=25):**
    - Ciphertext: 17, 8, 9, 21, 18
    - Key: 10, 4, 24, 10, 4
4.  **Decrypt using `P = (C - K) mod 26`:**
    - (17 - 10) mod 26 = 7 (H)
    - (8 - 4) mod 26 = 4 (E)
    - (9 - 24) mod 26 = -15 mod 26 = 11 (L)
    - (21 - 10) mod 26 = 11 (L)
    - (18 - 4) mod 26 = 14 (O)
5.  **Result:** `HELLO`

#### **Exercises**
1.  **Manual Decryption:** Decrypt the ciphertext `LXFOPVEFRNHR` using the key `LEMON`.
2.  **Python Implementation:** Write a Python script that takes a ciphertext and a key as input and returns the decrypted Vigenère plaintext.

---

### **3. Level 2: Symmetric Key Cryptography (Intermediate)**

#### **3.1 Block Ciphers vs. Stream Ciphers**
- **Block Ciphers:** Encrypt data in fixed-size blocks (e.g., AES uses 128-bit blocks).
- **Stream Ciphers:** Encrypt data one bit or byte at a time (e.g., ChaCha20).

#### **3.2 Advanced Encryption Standard (AES)**
AES is the global standard for symmetric encryption. It supports key lengths of 128, 192, and 256 bits.

#### **Solved Example: OpenSSL AES Encryption**
**Problem:** Encrypt a file named `secret.txt` with the content "This is a secret message." using AES-256-CBC and then decrypt it.

**Solution:**
1.  **Create the plaintext file:**
    ```bash
    echo "This is a secret message." > secret.txt
    ```
2.  **Encrypt the file:**
    ```bash
    openssl enc -aes-256-cbc -salt -in secret.txt -out encrypted.bin -k mypassword
    ```
3.  **Decrypt the file:**
    ```bash
    openssl enc -d -aes-256-cbc -in encrypted.bin -out decrypted.txt -k mypassword
    ```
4.  **Verify:** `cat decrypted.txt`

#### **Exercises**
1.  **OpenSSL Encryption:** Use OpenSSL to encrypt a file using `AES-128-CBC`. What happens if you use the wrong password during decryption?
2.  **The ECB Vulnerability:** Download a `.bmp` image. Encrypt it using `AES-256-ECB` and `AES-256-CBC`. Compare the two encrypted images. Why can you still see the pattern in the ECB version?
3.  **Python AES-GCM:** Use the `cryptography` library to encrypt the string "Authenticated Data" using AES-GCM. Ensure you include an Initialization Vector (IV) and an Authentication Tag.

---

### **4. Level 3: Hashing and Message Integrity (Intermediate)**

#### **4.1 Cryptographic Hash Functions**
A hash function takes an input and produces a fixed-size string (digest). It must be **one-way** and **collision-resistant**.

#### **Solved Example: File Integrity Verification**
**Problem:** Verify the integrity of a downloaded file `document.pdf` with a known SHA-256 checksum.

**Solution:**
1.  **Calculate the SHA-256 checksum:**
    ```bash
    sha256sum document.pdf
    ```
2.  **Compare the output** with the checksum provided on the download page. If they match, the file is untampered.

#### **Exercises**
1.  **Hash Collision Research:** Research the MD5 collision attack. Find two different files that produce the same MD5 hash.
2.  **HMAC Generation:** Use OpenSSL to generate an HMAC-SHA256 for the message "Transaction: $100" using the secret key "bank-secret".
    ```bash
    echo -n "Transaction: $100" | openssl dgst -sha256 -hmac "bank-secret"
    ```
3.  **Password Security:** Write a Python script that uses `bcrypt` to hash a user's password. Include a salt and verify the password later.

---

### **5. Level 4: Asymmetric Key Cryptography (Advanced)**

#### **5.1 RSA (Rivest-Shamir-Adleman)**
RSA relies on the mathematical difficulty of factoring large prime numbers. It uses a **Public Key** for encryption and a **Private Key** for decryption.

#### **Solved Example: RSA Key Generation**
**Problem:** Generate a 2048-bit RSA private key and extract the corresponding public key using OpenSSL.

**Solution:**
1.  **Generate the RSA private key:**
    ```bash
    openssl genrsa -out private.pem 2048
    ```
2.  **Extract the public key:**
    ```bash
    openssl rsa -in private.pem -pubout -out public.pem
    ```

#### **Exercises**
1.  **Manual RSA Calculation:** Given `p = 3` and `q = 11`:
    - Calculate `n = p * q`.
    - Calculate `phi(n) = (p-1) * (q-1)`.
    - Choose `e = 3`. Find `d` such that `(e * d) mod phi(n) = 1`.
    - Encrypt the message `M = 5` using `C = M^e mod n`.
    - Decrypt `C` using `M = C^d mod n`.
2.  **Python RSA Encryption:** Use the `cryptography` library to:
    - Generate an RSA key pair.
    - Encrypt the message "Top Secret" using the public key with OAEP padding.
    - Decrypt it using the private key.

---

### **6. Level 5: Digital Signatures and PKI (Expert)**

#### **6.1 Digital Signatures**
A digital signature provides **Authentication** and **Non-repudiation**. The sender signs the hash of a message with their **Private Key**.

#### **Solved Example: Digital Signatures (Signing and Verifying)**
**Problem:** Sign a message `hello.txt` using a previously generated RSA private key and then verify the signature.

**Solution:**
1.  **Create the message:** `echo "Hello World" > hello.txt`
2.  **Sign the message:**
    ```bash
    openssl dgst -sha256 -sign private.pem -out signature.bin hello.txt
    ```
3.  **Verify the signature:**
    ```bash
    openssl dgst -sha256 -verify public.pem -signature signature.bin hello.txt
    ```

#### **Exercises**
1.  **Tamper Detection:** Sign a file, then modify one character in the file. Try to verify the signature again. What is the result?
2.  **Self-Signed Certificate:** Create a self-signed X.509 certificate for the domain `mysite.local` valid for 365 days.
    ```bash
    openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes -subj "/CN=mysite.local"
    ```
3.  **Trust Chain Analysis:** Use `openssl s_client -connect google.com:443 -showcerts` to view the certificate chain. Identify the Root CA and the Intermediate CA.

---

### **7. Level 6: Real-world Protocols and Advanced Topics (Expert)**

#### **7.1 TLS (Transport Layer Security)**
The protocol behind HTTPS. It combines symmetric encryption, asymmetric encryption, and hashing.

#### **Solved Example: Wireshark TLS Handshake Analysis**
**Problem:** Identify the key messages in a TLS handshake using Wireshark.

**Solution:**
1.  **Start Wireshark** capture on your network interface.
2.  **Run:** `curl https://www.google.com`
3.  **Filter by `tls`** in Wireshark.
4.  **Find:** `Client Hello`, `Server Hello`, `Certificate`, and `Finished` messages.

#### **Exercises**
1.  **Cipher Suite Inspection:** Use `nmap --script ssl-enum-ciphers -p 443 google.com` to list the supported cipher suites. Which ones are considered "weak"?
2.  **GPG File Encryption:** Generate a GPG key pair. Encrypt a file for yourself and then decrypt it.
    ```bash
    gpg --full-generate-key
    gpg --encrypt --recipient "Your Name" secret.txt
    gpg --decrypt secret.txt.gpg
    ```

---

### **8. Level 7: Broken Crypto & Cryptanalysis (Expert)**

#### **8.1 Padding Oracle Attacks**
A padding oracle attack is an attack which uses the padding of a cryptographic message to decrypt the message.

#### **Solved Example: Understanding Padding Oracle**
**Problem:** Explain how a padding oracle can be used to decrypt a block of ciphertext.

**Solution:**
If a server reveals whether a decrypted ciphertext has valid PKCS#7 padding, an attacker can modify the last byte of the previous ciphertext block. By iterating through all 256 values, the attacker finds the one that results in valid padding (usually `0x01`). This reveals the last byte of the plaintext.

#### **Exercises**
1.  **Padding Oracle Simulation:** Research the "Padding Oracle" attack. Use a tool like `padbuster` against a simulated vulnerable web application to decrypt a session cookie.
2.  **Hash Length Extension:** Use `hashpump` to perform a length extension attack. Given `Hash(secret + "user=admin")`, generate a valid hash for `secret + "user=admin&append=true"` without knowing the `secret`.

---

### **9. Level 8: Future of Cryptography (Expert)**

#### **9.1 Homomorphic Encryption**
Allows computations to be performed on encrypted data without first decrypting it.

#### **9.2 Zero-Knowledge Proofs (ZKP)**
Allows one party to prove to another that they know a value, without conveying any information apart from the fact that they know the value.

#### **Exercises**
1.  **ZKP Research:** Explain the "Ali Baba Cave" analogy for Zero-Knowledge Proofs. How does it prove knowledge without revealing the secret?
2.  **Post-Quantum Cryptography (PQC):** Research the NIST PQC competition. Name three algorithms that are currently being standardized to replace RSA and ECC.

---

### **10. Mastery Challenge: The Cryptographic Gauntlet**

**Scenario:** You are a security engineer at a global bank. You must design a secure communication system for high-value transactions.

**Task:**
1.  **Key Management:** Design a system to securely store and rotate RSA-4096 keys.
2.  **Secure Channel:** Implement a Python script that simulates a TLS-like handshake:
    - Exchange public keys.
    - Establish a shared AES-256 session key using Diffie-Hellman.
    - Encrypt a "Transaction" message using the session key.
3.  **Audit Trail:** Every transaction must be hashed using SHA-3 and digitally signed.
4.  **Quantum Readiness:** Propose a plan to migrate the bank's infrastructure to Post-Quantum Cryptography.

---

### **Conclusion**
Cryptography is a rapidly evolving field. By completing this lab, you have progressed from the ancient Caesar cipher to the cutting-edge world of Post-Quantum Cryptography and Zero-Knowledge Proofs. Continue to practice, stay updated on new vulnerabilities, and always remember: **Never roll your own crypto!**
