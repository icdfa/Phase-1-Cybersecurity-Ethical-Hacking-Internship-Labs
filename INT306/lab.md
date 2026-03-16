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
3.  **Python Caesar Cipher (Making Things):**
    -   **Problem:** Implement a Python function to encrypt and decrypt messages using the Caesar cipher.
    -   **Solved Example:**
        ```python
        def caesar_cipher(text, shift, mode=\'encrypt\'):
            result = \"\"
            for char in text:
                if char.isalpha():
                    start = ord(\'A\') if char.isupper() else ord(\'a\')
                    if mode == \'encrypt\':
                        shifted_char = chr((ord(char) - start + shift) % 26 + start)
                    elif mode == \'decrypt\':
                        shifted_char = chr((ord(char) - start - shift) % 26 + start)
                    result += shifted_char
                else:
                    result += char
            return result

        # Example Usage:
        plaintext = \"HELLO\"
        key = 3

        encrypted_text = caesar_cipher(plaintext, key, mode=\'encrypt\')
        print(f\"Encrypted: {encrypted_text}\") # KHOOR

        decrypted_text = caesar_cipher(encrypted_text, key, mode=\'decrypt\')
        print(f\"Decrypted: {decrypted_text}\") # HELLO
        ```
    -   **Task:** Implement the `caesar_cipher` function in Python. Test it with the plaintext `CRYPTOGRAPHY` and a shift of `7`. Then decrypt the resulting ciphertext.

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
4.  **Secure File Encryption Tool (Making Things):**
    -   **Problem:** Build a command-line tool in Python that can encrypt and decrypt files using AES-256-GCM. The tool should derive a key from a user-provided password.
    -   **Solved Example:**
        ```python
        import os
        from cryptography.hazmat.primitives.ciphers.aead import AESGCM
        from cryptography.hazmat.primitives.kdf.pbkdf2 import PBKDF2HMAC
        from cryptography.hazmat.primitives import hashes
        from cryptography.hazmat.backends import default_backend

        def derive_key(password: bytes, salt: bytes) -> bytes:
            kdf = PBKDF2HMAC(
                algorithm=hashes.SHA256(),
                length=32,
                salt=salt,
                iterations=100000,
                backend=default_backend()
            )
            return kdf.derive(password)

        def encrypt_file(file_path: str, password: str):
            salt = os.urandom(16)
            key = derive_key(password.encode(), salt)
            aesgcm = AESGCM(key)
            nonce = os.urandom(12)

            with open(file_path, 'rb') as f:
                plaintext = f.read()

            ciphertext = aesgcm.encrypt(nonce, plaintext, None)

            with open(file_path + '.enc', 'wb') as f:
                f.write(salt + nonce + ciphertext)
            print(f"Encrypted {file_path} to {file_path}.enc")

        def decrypt_file(file_path: str, password: str):
            with open(file_path, 'rb') as f:
                data = f.read()
            
            salt = data[:16]
            nonce = data[16:28]
            ciphertext = data[28:]

            key = derive_key(password.encode(), salt)
            aesgcm = AESGCM(key)

            try:
                plaintext = aesgcm.decrypt(nonce, ciphertext, None)
                with open(file_path.replace('.enc', '.dec'), 'wb') as f:
                    f.write(plaintext)
                print(f"Decrypted {file_path} to {file_path.replace('.enc', '.dec')}")
            except Exception as e:
                print(f"Decryption failed: {e}")

        # Example Usage:
        # with open('my_secret_file.txt', 'w') as f: f.write('This is a top secret file.')
        # encrypt_file('my_secret_file.txt', 'my-strong-password')
        # decrypt_file('my_secret_file.txt.enc', 'my-strong-password')
        ```
    -   **Task:** Implement the secure file encryption tool in Python. Create a text file, encrypt it using your tool, and then decrypt it to verify that the contents are restored correctly. Then, try to decrypt the file with the wrong password and observe the result.

---

### **4. Level 3: Hashing and Message Integrity (Intermediate)**

#### **4.1 Cryptographic Hash Functions**
A hash function takes an input and produces a fixed-size string (digest). It must be **one-way** and **collision-resistant**.

#### **Solved Example: Compute Hash Values**
**Problem:** Compute the MD5 and SHA-256 hash values for the string "Cryptography Lab".

**Solution:**
1.  **Using Python:**
    ```python
    import hashlib

    data = "Cryptography Lab".encode('utf-8')

    md5_hash = hashlib.md5(data).hexdigest()
    sha256_hash = hashlib.sha256(data).hexdigest()

    print(f"MD5 Hash: {md5_hash}")
    print(f"SHA-256 Hash: {sha256_hash}")
    ```
    **Output:**
    ```
    MD5 Hash: 5eb63bbbe01eeed093cb22bb8f5ac6
    SHA-256 Hash: b0b84c2e9c5f1ec3e379ef4be8e12df02e9da8b4043ec8ff074e1c2c4205a05b
    ```
2.  **Using `echo` and `openssl` (Linux/macOS):**
    ```bash
    echo -n "Cryptography Lab" | openssl md5
    echo -n "Cryptography Lab" | openssl sha256
    ```

#### **Exercises**
1.  **Compute Hash Values:** Using Python or OpenSSL, compute the hash values for the following strings:
    - "Hello World"
    - "Secure Hashing"
    - "INT306 Cryptography"
    Record the MD5 and SHA-256 hash values for each. Discuss the differences in the output length and characteristics.
2.  **File Integrity Verification:** Download a file (e.g., a Linux ISO) and find its official SHA-256 checksum. Verify the integrity of your downloaded file using `sha256sum`.
3.  **Hash Function Properties (Avalanche Effect):**
    - Create a file named `original.txt` with the content: `The quick brown fox jumps over the lazy dog.`
    - Compute its SHA-256 hash.
    - Create a new file named `modified.txt` with a single character changed: `The quick brown fox jumps over the lazy cog.`
    - Compute the SHA-256 hash of `modified.txt`.
    - Compare the two hashes. Discuss how drastically the hash changes due to a minor input alteration, illustrating the **avalanche effect**.
4.  **HMAC Generation:** Use OpenSSL to generate an HMAC-SHA256 for the message "Financial Transaction: $500" using the secret key "super-secret-key-123".
5.  **Password Security (bcrypt):** Write a Python script that:
    - Takes a password as input.
    - Hashes the password using `bcrypt` with a randomly generated salt.
    - Stores the hash.
    - Later, takes another password input and verifies it against the stored hash.
    Discuss why `bcrypt` is preferred over simple SHA-256 for password hashing.
6.  **Rainbow Table Concept:** Research and describe how a rainbow table works to crack password hashes. Explain why salting passwords effectively mitigates rainbow table attacks.
7.  **Collision Demonstration (Making Things):**
    -   **Problem:** Demonstrate an MD5 hash collision using known collision pairs. Explain why this makes MD5 unsuitable for integrity checks where collision resistance is critical.
    -   **Solved Example:**
        1.  **Known MD5 Collision Files:** For educational purposes, we can use pre-generated files that are known to collide. (In a real scenario, generating these is computationally intensive).
            - Download `md5_collision_1.bin` and `md5_collision_2.bin` (these would be provided as lab resources).
        2.  **Compute MD5 Hashes:**
            ```bash
            md5sum md5_collision_1.bin
            md5sum md5_collision_2.bin
            ```
        3.  **Observe:** Both files will produce the exact same MD5 hash, despite having different content.
        4.  **Discussion:** This demonstrates that MD5 is not collision-resistant, meaning an attacker could substitute a malicious file for a legitimate one if only MD5 hashes are used for verification.
    -   **Task:** Obtain two files that are known to produce an MD5 collision (e.g., from a reputable source like the [MD5 Collision Project](https://www.win.tue.nl/~bdeweger/Collisions/)). Verify their hashes and explain the implications for digital signatures and file integrity.
8.  **Rainbow Table Creation (Making Things):**
    -   **Problem:** Create a simple rainbow table for a small set of common passwords (e.g., `password`, `123456`, `qwerty`) using MD5 hashes. Then, demonstrate how to use this table to find the original password for a given hash.
    -   **Solved Example:**
        1.  **Common Passwords and their MD5 Hashes:**
            - `password`: `5f4dcc3b5aa765d61d8327deb882cf99`
            - `123456`: `e10adc3949ba59abbe56e057f20f883e`
            - `qwerty`: `d8578edf8458ce06fbc5bb76a587711`
        2.  **Python Script to Generate Table:**
            ```python
            import hashlib

            passwords = ["password", "123456", "qwerty"]
            rainbow_table = {}

            print("Generating Rainbow Table...")
            for pwd in passwords:
                md5_hash = hashlib.md5(pwd.encode("utf-8")).hexdigest()
                rainbow_table[md5_hash] = pwd
                print(f"  Password: {pwd}, MD5: {md5_hash}")

            print("\nRainbow Table Generated.")

            # Example of using the table to crack a hash
            target_hash = "e10adc3949ba59abbe56e057f20f883e" # Hash for 123456
            if target_hash in rainbow_table:
                print(f"\nCracked! Hash {target_hash} corresponds to password: {rainbow_table[target_hash]}")
            else:
                print(f"\nHash {target_hash} not found in table.")
            ```
    -   **Task:** Implement the Python script to generate a rainbow table for at least 5 common passwords. Then, given an MD5 hash (e.g., `d8578edf8458ce06fbc5bb76a587711`), use your table to find the original password. Discuss the limitations of this simple rainbow table and how salting would prevent this attack.
9.  **Real-World Application (Research & Report):**
    -   **Problem:** Choose an application that heavily utilizes hash functions (e.g., blockchain/cryptocurrency, digital forensics, version control systems like Git, or secure boot processes). Write a one-page report detailing how hash functions are used in that application.
    -   **Solved Example Outline:**
        1.  **Application Chosen:** Blockchain/Cryptocurrency (e.g., Bitcoin)
        2.  **How Hashes are Used:**
            -   **Block Header Hashing:** Each block header is hashed using SHA-256 (double SHA-256). This hash serves as the block's unique identifier and is crucial for linking blocks in the chain.
            -   **Proof-of-Work:** Miners compete to find a hash below a certain target, demonstrating computational effort and securing the network.
            -   **Merkle Trees:** Transaction hashes are organized into a Merkle tree, where the root hash is included in the block header, allowing efficient verification of transactions.
            -   **Wallet Addresses:** Public keys are hashed to generate wallet addresses, providing a layer of abstraction and privacy.
        3.  **Potential Vulnerabilities/Implications:**
            -   **51% Attack:** If an attacker controls more than 50% of the network's hashing power, they could potentially reverse transactions or prevent new ones.
            -   **Hash Collisions (Theoretical):** While highly improbable for SHA-256, a collision could theoretically allow an attacker to forge transactions.
            -   **Quantum Computing:** Future quantum computers could break the underlying cryptographic primitives (like ECDSA for signatures), though PQC is being researched.
    -   **Task:** Select an application (e.g., Git, Digital Forensics, Secure Boot, Certificate Transparency) and prepare a one-page report (approx. 300-500 words) explaining the role of hash functions, including specific algorithms used, their benefits, and any associated vulnerabilities or real-world implications.
10. **Implementing a Hash Table (Making Things):**
    -   **Problem:** Implement a simple hash table (also known as a hash map or dictionary) in Python that stores key-value pairs. Demonstrate its basic operations (insert, search, delete).
    -   **Solved Example:**
        ```python
        class HashTable:
            def __init__(self, size):
                self.size = size
                self.table = [[] for _ in range(self.size)]

            def _hash(self, key):
                return hash(key) % self.size

            def insert(self, key, value):
                key_hash = self._hash(key)
                key_value = [key, value]

                if self.table[key_hash] is None:
                    self.table[key_hash] = [key_value]
                else:
                    for pair in self.table[key_hash]:
                        if pair[0] == key:
                            pair[1] = value # Update existing key
                            return
                    self.table[key_hash].append(key_value) # Add new key

            def search(self, key):
                key_hash = self._hash(key)
                if self.table[key_hash] is not None:
                    for pair in self.table[key_hash]:
                        if pair[0] == key:
                            return pair[1]
                return None

            def delete(self, key):
                key_hash = self._hash(key)
                if self.table[key_hash] is not None:
                    for i, pair in enumerate(self.table[key_hash]):
                        if pair[0] == key:
                            del self.table[key_hash][i]
                            print(f"Deleted: {key}")
                            return
                print(f"Key {key} not found.")

            def display(self):
                for i, bucket in enumerate(self.table):
                    print(f"Bucket {i}: {bucket}")

        # Demonstrate usage
        ht = HashTable(10)
        ht.insert("apple", 10)
        ht.insert("banana", 20)
        ht.insert("cherry", 30)
        ht.insert("apple", 15) # Update apple

        print("\n--- Hash Table Contents ---")
        ht.display()

        print("\n--- Search Operations ---")
        print(f"Search 'banana': {ht.search('banana')}")
        print(f"Search 'grape': {ht.search('grape')}")

        print("\n--- Delete Operations ---")
        ht.delete("banana")
        ht.delete("grape")

        print("\n--- Hash Table Contents After Deletion ---")
        ht.display()
        ```
    -   **Task:** Implement the `HashTable` class in Python. Test its `insert`, `search`, and `delete` operations with at least 5 different key-value pairs. Discuss how hash functions (specifically the `_hash` method) contribute to the efficiency of hash tables and the concept of collision resolution (e.g., chaining as used in the example).

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
3.  **Diffie-Hellman Key Exchange Simulation (Making Things):**
    -   **Problem:** Implement a Python script to simulate the Diffie-Hellman key exchange protocol between two parties (Alice and Bob) to establish a shared secret.
    -   **Solved Example:**
        ```python
        from cryptography.hazmat.primitives import hashes
        from cryptography.hazmat.primitives.asymmetric import dh
        from cryptography.hazmat.primitives.kdf.hkdf import HKDF
        from cryptography.hazmat.backends import default_backend

        # 1. Agree on common parameters (p, g)
        # In a real scenario, these would be well-known safe primes.
        # For demonstration, we generate small parameters.
        parameters = dh.generate_parameters(generator=2, key_size=512, backend=default_backend())

        # 2. Alice generates her private key and public key
        alice_private_key = parameters.generate_private_key()
        alice_public_key = alice_private_key.public_key()

        # 3. Bob generates his private key and public key
        bob_private_key = parameters.generate_private_key()
        bob_public_key = bob_private_key.public_key()

        print("--- Diffie-Hellman Key Exchange Simulation ---")
        print(f"Alice\'s Public Key: {alice_public_key.public_bytes(encoding=serialization.Encoding.PEM, format=serialization.PublicFormat.SubjectPublicKeyInfo).decode().strip().splitlines()[1]}")
        print(f"Bob\'s Public Key: {bob_public_key.public_bytes(encoding=serialization.Encoding.PEM, format=serialization.PublicFormat.SubjectPublicKeyInfo).decode().strip().splitlines()[1]}")

        # 4. Alice computes the shared secret
        alice_shared_key = alice_private_key.exchange(bob_public_key)

        # 5. Bob computes the shared secret
        bob_shared_key = bob_private_key.exchange(alice_public_key)

        # 6. Derive a symmetric key from the shared secret using HKDF
        derived_key_alice = HKDF(algorithm=hashes.SHA256(), length=32, salt=None, info=b\'handshake data\', backend=default_backend()).derive(alice_shared_key)
        derived_key_bob = HKDF(algorithm=hashes.SHA256(), length=32, salt=None, info=b\'handshake data\', backend=default_backend()).derive(bob_shared_key)

        print(f"\nAlice\'s Derived Shared Key: {derived_key_alice.hex()}")
        print(f"Bob\'s Derived Shared Key: {derived_key_bob.hex()}")

        if derived_key_alice == derived_key_bob:
            print("\nShared keys match! Secure communication can now proceed.")
        else:
            print("\nError: Shared keys do not match.")
        ```
    -   **Task:** Implement the Python Diffie-Hellman key exchange simulation. Run the script and observe that Alice and Bob successfully derive the same shared secret. Explain the role of the public parameters (`p`, `g`) and why the private keys (`a`, `b`) are never exchanged.

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
