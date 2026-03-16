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
- **Encryption:** \( E(x) = (x + k) \mod 26 \)
- **Decryption:** \( D(x) = (x - k) \mod 26 \)

#### **2.2 The Vigenère Cipher**
The Vigenère cipher is a **polyalphabetic substitution cipher** that uses a keyword to determine the shift for each letter.

#### **Solved Example: Vigenère Cipher Decryption**
**Problem:** Decrypt the ciphertext `RIJVS` using the key `KEY`.

**Solution:**
1.  **Repeat the key:** `KEYKE`
2.  **Align ciphertext and key:**
    ```
    Ciphertext: R I J V S
    Key:        K E Y K E
    ```
3.  **Convert letters to numbers (A=0, B=1, ..., Z=25):**
    ```
    Ciphertext: 17 8 9 21 18
    Key:        10 4 24 10 4
    ```
4.  **Decrypt using the formula P = (C - K) mod 26:**
    -   R (17) - K (10) = 7 (H)
    -   I (8) - E (4) = 4 (E)
    -   J (9) - Y (24) = -15 mod 26 = 11 (L)
    -   V (21) - K (10) = 11 (L)
    -   S (18) - E (4) = 14 (O)

**Plaintext:** `HELLO`

#### **Exercises**
1. **Manual Decryption:** Decrypt the following Vigenère ciphertext using the key `KEY`: `RIJVS`.
2. **Cryptanalysis:** Use frequency analysis to attempt to break a Caesar cipher with an unknown shift.
3. **Python Implementation:** Write a Python script that can encrypt and decrypt messages using the Vigenère cipher.

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
    openssl enc -aes-256-cbc -salt -in secret.txt -out encrypted.bin -pass pass:mysecretpassword
    ```
3.  **Decrypt the file:**
    ```bash
    openssl enc -d -aes-256-cbc -in encrypted.bin -out decrypted.txt -pass pass:mysecretpassword
    ```

#### **Exercises**
1. **OpenSSL Encryption:** Use OpenSSL to encrypt a file using AES-256-CBC.
2. **The ECB Vulnerability:** Encrypt a bitmap image (.bmp) using AES-ECB and AES-CBC. Observe why ECB is insecure for structured data.
3. **Python AES:** Implement a script using the `cryptography` library to encrypt a string using AES-GCM.

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
2.  **Compare the calculated checksum with the provided checksum.** If they match, the file's integrity is verified.

#### **Exercises**
1. **File Integrity:** Download a file and verify its SHA-256 checksum against the provided value.
2. **HMAC Generation:** Use OpenSSL to generate an HMAC-SHA256 for a message.
3. **Password Security:** Write a Python script that hashes a password using `bcrypt` with a salt.

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
1. **RSA Key Generation:** Generate a 2048-bit RSA key pair using OpenSSL.
2. **Manual RSA:** Given \( p=3, q=11 \), calculate \( n, \phi(n) \), and find a valid \( e \) and \( d \).
3. **Python RSA:** Use the `cryptography` library to encrypt a message with a public key and decrypt it with a private key using OAEP padding.

---

### **6. Level 5: Digital Signatures and PKI (Expert)**

#### **6.1 Digital Signatures**
A digital signature provides **Authentication** and **Non-repudiation**. The sender signs the hash of a message with their **Private Key**.

#### **Solved Example: Digital Signatures (Signing and Verifying)**
**Problem:** Sign a message `hello.txt` using a previously generated RSA private key and then verify the signature.

**Solution:**
1.  **Sign the message:**
    ```bash
    openssl dgst -sha256 -sign private.pem -out signature.bin hello.txt
    ```
2.  **Verify the signature:**
    ```bash
    openssl dgst -sha256 -verify public.pem -signature signature.bin hello.txt
    ```

#### **Exercises**
1. **Signing and Verifying:** Sign a text file using your RSA private key and verify it using the public key.
2. **Self-Signed Certificate:** Create a self-signed X.509 certificate for a web server.
3. **Trust Chain Analysis:** Inspect the certificate chain of `google.com` using your browser or OpenSSL.

---

### **7. Level 6: Real-world Protocols and Advanced Topics (Expert)**

#### **7.1 TLS (Transport Layer Security)**
The protocol behind HTTPS. It combines symmetric encryption, asymmetric encryption, and hashing.

#### **Solved Example: Wireshark TLS Handshake Analysis**
**Problem:** Identify the key messages in a TLS handshake using Wireshark.

**Solution:**
1.  **Open Wireshark** and start capturing on your active interface.
2.  **Browse to an HTTPS website** (e.g., `https://www.example.com`).
3.  **Filter for `tls`** and look for `Client Hello`, `Server Hello`, and `Certificate` messages.

#### **Exercises**
1. **Wireshark Analysis:** Capture a TLS handshake in Wireshark and identify the "Client Hello" and "Server Hello" messages.
2. **GPG Encryption:** Use GnuPG to encrypt a file for a specific recipient's public key.

---

### **8. Level 7: Broken Crypto & Cryptanalysis (Expert)**

#### **8.1 Padding Oracle Attacks**
A padding oracle attack is an attack which uses the padding of a cryptographic message to decrypt the message.

#### **Solved Example: Understanding Padding Oracle**
**Problem:** Explain how a padding oracle can be used to decrypt a block of ciphertext.

**Solution:**
If a server reveals whether a decrypted ciphertext has valid padding, an attacker can systematically modify the ciphertext and observe the server's response. By doing this, the attacker can deduce the plaintext byte by byte without knowing the key.

#### **8.2 Hash Length Extension Attacks**
This attack allows an attacker to use `Hash(message1)` to calculate `Hash(message1 || message2)` without knowing `message1`.

#### **Exercises**
1. **Padding Oracle Challenge:** Research the "Padding Oracle" attack and explain how it can be used to decrypt CBC-mode ciphertext.
2. **Length Extension Challenge:** Use a tool like `hashpump` to perform a length extension attack on a simulated vulnerable application.

---

### **9. Level 8: Future of Cryptography (Expert)**

#### **9.1 Homomorphic Encryption**
Allows computations to be performed on encrypted data without first decrypting it.

#### **9.2 Zero-Knowledge Proofs (ZKP)**
Allows one party to prove to another that they know a value, without conveying any information apart from the fact that they know the value.

#### **Exercises**
1. **ZKP Research:** Research the "Ali Baba Cave" analogy and explain the concept of ZKP in your own words.
2. **Homomorphic Encryption Exploration:** Research the difference between Partially Homomorphic Encryption (PHE) and Fully Homomorphic Encryption (FHE).

---

### **10. Mastery Challenge: The Cryptographic Gauntlet**

**Scenario:** You are a security engineer at a global bank. You must design a secure communication system for high-value transactions.

**Task:**
1. **Key Management:** Design a system to securely store and rotate RSA-4096 keys.
2. **Secure Channel:** Implement a Python script that simulates a TLS-like handshake.
3. **Audit Trail:** Every transaction must be hashed using SHA-3 and digitally signed.
4. **Quantum Readiness:** Propose a plan to migrate the bank's infrastructure to Post-Quantum Cryptography.

---

### **Conclusion**
Cryptography is a rapidly evolving field. By completing this lab, you have progressed from the ancient Caesar cipher to the cutting-edge world of Post-Quantum Cryptography and Zero-Knowledge Proofs. Continue to practice, stay updated on new vulnerabilities, and always remember: **Never roll your own crypto!**
