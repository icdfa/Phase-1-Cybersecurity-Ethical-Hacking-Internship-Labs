
### **INT306: Cryptography – Lab 1: Exploring the Caesar Cipher**

---

#### **Objectives**

By the end of this lab, students will be able to:
- Understand the fundamental concepts of substitution ciphers
- Implement the Caesar cipher encryption and decryption algorithms
- Analyze the security weaknesses of classical ciphers
- Apply cryptanalysis techniques to break Caesar cipher encrypted messages
- Recognize the historical significance and limitations of the Caesar cipher

---

#### **Overview**
The **Caesar cipher** is a simple yet powerful encryption technique classified as a substitution cipher. In this method, each letter in the plaintext is replaced by another letter a fixed number of positions down the alphabet. This lab will explore the workings of the Caesar cipher, its applications, and various exercises to solidify your understanding.

---

### **Understanding the Caesar Cipher**
The Caesar cipher operates by shifting the letters of the alphabet. For example, with a shift of 2:

**Example Shift Table (Shift of 2):**
```
Plain:  A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
Cipher: C D E F G H I J K L M N O P Q R S T U V W X Y Z A B
```

**Algorithm:**
- **Encryption:** For each plaintext letter \( p \), substitute the ciphertext letter \( C \):
  \[
  C = (p + k) \mod 26
  \]
- **Decryption:** For each ciphertext letter \( C \), retrieve the original plaintext letter \( P \):
  \[
  P = (C - k) \mod 26
  \]

---

### **Caesar Cipher Examples**

#### **Example 1: Encryption**
**Encrypt the plaintext “HELLO” using a shift of 3.**

**Solution:**
```
Plain:  H E L L O
Shift:  K H O O R
Cipher: K H O O R
```

---

#### **Example 2: Decryption**
**Decrypt the ciphertext “WTAAD” using a shift of 4.**

**Solution:**
```
Cipher: W T A A D
Shift:  S P W W Z
Plain:  S P W W Z
```

---

### **Exercises**

#### **Exercise 1: Basic Decryption**
A plaintext was encrypted with a Caesar cipher using a shift of 4. The resulting ciphertext is:  
**Ciphertext:** “LIPPS”  
**Task:** Determine the original plaintext.

---

#### **Exercise 2: Brute Force Attack**
Attempt to crack the following Caesar ciphertext using brute force:  
**Ciphertext:** “ZEBRAS”  
**Task:** Try every possible shift (1-25) and identify the original plaintext.

---

#### **Exercise 3: Pattern Recognition**
You have the following encrypted message:  
**Ciphertext:** “CGRRC YQ YZGE”  
**Task:** Can you determine the plaintext?  
**Hint:** Look for patterns, especially the repeated letters.

---

#### **Exercise 4: Frequency Analysis**
The following ciphertext has been created without spaces:  
**Ciphertext:** “hxgfhgshvczhx”  
**Task:** Conduct a frequency analysis of the letters. Based on your findings, attempt to decrypt the message by hypothesizing the most common letters.

---

#### **Exercise 5: Creative Sentence**
Create a meaningful sentence of your own, encrypt it using a Caesar cipher with a shift of 5, and present the ciphertext to your peers. Challenge them to decode it!

---

#### **Exercise 6: Historical Context**
Research the historical use of the Caesar cipher in military communication. Write a brief paragraph on its significance during Julius Caesar's time and how it relates to modern encryption techniques.

---

#### **Exercise 7: Modern Application**
Choose a contemporary use case for substitution ciphers (such as in gaming or secure communications). Write a short essay discussing its relevance today and compare it to the Caesar cipher.

---

### **Conclusion**
Through this lab, students will gain practical insights into the Caesar cipher, practice decryption and encryption techniques, and explore the broader implications of substitution ciphers in both historical and modern contexts. This foundational understanding will prepare students for more complex cryptographic concepts.

