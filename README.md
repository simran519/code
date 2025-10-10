[README.md](https://github.com/user-attachments/files/22847714/README.md)

## Practical 1: Substitution and Transformation Ciphers

### **AIM**
DKFNDDKGNDV

### 🅐 Caesar (Shift) Cipher

**Algorithm:** Shifts each letter by a fixed number of positions in the alphabet.

```python
def encrypt(text, shift):
    result = ""
    for char in text:
        if char.isupper():
            result += chr((ord(char) + shift - 65) % 26 + 65)
        elif char.islower():
            result += chr((ord(char) + shift - 97) % 26 + 97)
        else:
            result += char
    return result

def decrypt(text, shift):
    return encrypt(text, -shift)

# Example Usage
plain_text = "Hello World"
shift = 3
encrypt_text = encrypt(plain_text, shift)
decrypt_text = decrypt(encrypt_text, shift)

print("Plain text:", plain_text)
print("Encrypted:", encrypt_text)
print("Decrypted:", decrypt_text)
```

### 🅑 Vernam (One-Time Pad) Cipher

**Algorithm:** XOR operation between plaintext and key of equal length.

```python
def vernam_encrypt(plaintext, key):
    if len(plaintext) != len(key):
        raise ValueError("Key and plaintext must be same length")
    
    ciphertext = ""
    for i in range(len(plaintext)):
        # XOR operation
        cipher_char = chr(ord(plaintext[i]) ^ ord(key[i]))
        ciphertext += cipher_char
    return ciphertext

def vernam_decrypt(ciphertext, key):
    return vernam_encrypt(ciphertext, key)  # XOR is symmetric

# Example Usage
plaintext = "HELLO"
key = "XMCKL"
cipher = vernam_encrypt(plaintext, key)
decrypted = vernam_decrypt(cipher, key)

print("Plaintext:", plain_text)
print("Key:", key)
print("Encrypted:", cipher)
print("Decrypted:", decrypted)
```

### 🅒 Columnar Transposition Cipher

**Algorithm:** Arranges plaintext in a grid and reads columns based on keyword order.

```python
def encrypt(plaintext, keyword):
    # Remove spaces and convert to uppercase
    plaintext = plaintext.replace(" ", "").upper()
    
    # Create grid
    cols = len(keyword)
    rows = len(plaintext) // cols
    if len(plaintext) % cols:
        rows += 1
    
    # Fill grid with plaintext
    grid = [[''] * cols for _ in range(rows)]
    index = 0
    for i in range(rows):
        for j in range(cols):
            if index < len(plaintext):
                grid[i][j] = plaintext[index]
                index += 1
            else:
                grid[i][j] = 'X'  # Padding
    
    # Get column order based on keyword
    col_order = sorted(range(len(keyword)), key=lambda k: keyword[k])
    
    # Read columns in order
    ciphertext = ""
    for col in col_order:
        for row in range(rows):
            ciphertext += grid[row][col]
    
    return ciphertext

def decrypt(ciphertext, keyword):
    cols = len(keyword)
    rows = len(ciphertext) // cols
    
    # Get column order
    col_order = sorted(range(len(keyword)), key=lambda k: keyword[k])
    
    # Fill grid column by column
    grid = [[''] * cols for _ in range(rows)]
    index = 0
    for col in col_order:
        for row in range(rows):
            grid[row][col] = ciphertext[index]
            index += 1
    
    # Read row by row
    plaintext = ""
    for i in range(rows):
        for j in range(cols):
            plaintext += grid[i][j]
    
    return plaintext.rstrip('X')  # Remove padding

# Example Usage
plain_text = "BNN College"
key = "SECRET"
encrypted = encrypt(plain_text, key)
decrypted = decrypt(encrypted, key)

print("Plain text:", plain_text)
print("Keyword:", key)
print("Encrypted:", encrypted)
print("Decrypted:", decrypted)
```

### 🅓 Rail Fence Cipher

**Algorithm:** Writes plaintext in zigzag pattern across multiple rails.

```python
def railfence_encrypt(plaintext, rails=2):
    plaintext = plaintext.replace(" ", "").lower()
    
    if rails == 2:
        row_1 = ""
        row_2 = ""
        
        for i, char in enumerate(plaintext):
            if i % 2 == 0:
                row_1 += char
            else:
                row_2 += char
        
        return row_1 + row_2
    
def railfence_decrypt(ciphertext, rails=2):
    if rails == 2:
        mid = len(ciphertext) // 2
        row_1 = ciphertext[:mid]
        row_2 = ciphertext[mid:]
        
        plaintext = ""
        for i in range(len(row_1)):
            plaintext += row_1[i]
            if i < len(row_2):
                plaintext += row_2[i]
        
        return plaintext

# Example Usage
plain_text = "Janhavi Singh"
encrypted = railfence_encrypt(plain_text)
decrypted = railfence_decrypt(encrypted)

print("Plain text:", plain_text)
print("Encrypted:", encrypted)
print("Decrypted:", decrypted)
```

---

## Practical 2: RSA Encryption and Decryption

### **AIM**
Implement the RSA algorithm for public-key encryption and decryption, and explore its properties and security considerations.

### 🅐 Monoalphabetic Substitution Cipher

```python
import string

def monoalphabetic_cipher():
    ALPHABET = string.ascii_uppercase
    KEY = "QWERTYUIOPASDFGHJKLZXCVBNM"
    
    def encrypt(plaintext):
        plaintext = plaintext.upper()
        ciphertext = ""
        for char in plaintext:
            if char in ALPHABET:
                index = ALPHABET.index(char)
                ciphertext += KEY[index]
            else:
                ciphertext += char
        return ciphertext
    
    def decrypt(ciphertext):
        plaintext = ""
        for char in ciphertext:
            if char in KEY:
                index = KEY.index(char)
                plaintext += ALPHABET[index]
            else:
                plaintext += char
        return plaintext
    
    return encrypt, decrypt

# Example Usage
encrypt, decrypt = monoalphabetic_cipher()
message = "HELLO WORLD"
encrypted = encrypt(message)
decrypted = decrypt(encrypted)

print("Original:", message)
print("Encrypted:", encrypted)
print("Decrypted:", decrypted)
```

### 🅑 RSA Algorithm (Manual Implementation)

```python
import math

def gcd(a, b):
    while b:
        a, b = b, a % b
    return a

def mod_inverse(e, phi):
    for d in range(1, phi):
        if (e * d) % phi == 1:
            return d
    return None

def rsa_manual():
    # Step 1: Choose two prime numbers
    p = 3
    q = 7
    
    # Step 2: Calculate n = p * q
    n = p * q
    
    # Step 3: Calculate Euler's totient function
    phi = (p - 1) * (q - 1)
    
    # Step 4: Choose e such that gcd(e, phi) = 1
    e = 2
    while gcd(e, phi) != 1:
        e += 1
    
    # Step 5: Calculate d (private key)
    d = mod_inverse(e, phi)
    
    print(f"p = {p}, q = {q}")
    print(f"n = {n}")
    print(f"phi = {phi}")
    print(f"e = {e}")
    print(f"d = {d}")
    
    # Encryption and Decryption
    message = 12
    ciphertext = pow(message, e, n)
    plaintext = pow(ciphertext, d, n)
    
    print(f"Original message: {message}")
    print(f"Encrypted: {ciphertext}")
    print(f"Decrypted: {plaintext}")

rsa_manual()
```

### 🅒 RSA using Python RSA Library

```python
import rsa

def rsa_library_example():
    # Generate key pair
    publickey, privatekey = rsa.newkeys(512)
    
    # Message to encrypt
    message = "Welcome to BNN College"
    
    # Encrypt message
    encMessage = rsa.encrypt(message.encode(), publickey)
    
    # Decrypt message
    decMessage = rsa.decrypt(encMessage, privatekey).decode()
    
    print("Original Message:", message)
    print("Encrypted Message:", encMessage)
    print("Decrypted Message:", decMessage)

rsa_library_example()
```

---

## Practical 3: Message Authentication Codes (MAC)

### **AIM**
Implement algorithms to generate and verify MACs for data integrity and authenticity.

### 🅐 MD5 Algorithm

```python
import hashlib

def md5_demo():
    # Example 1
    result = hashlib.md5(b'BNN COLLEGE')
    print("MD5 of 'BNN COLLEGE':", result.hexdigest())
    print("MD5 digest:", result.digest())
    
    # Example 2 - Different case
    result1 = hashlib.md5(b'bnn college')
    print("MD5 of 'bnn college':", result1.hexdigest())
    
    # Show different hashes for different cases
    print("Same content, different case produces different hash!")

md5_demo()
```

### 🅑 SHA Algorithm

```python
import hashlib

def sha_demo():
    # User input
    str_input = input("Enter the value to encode: ")
    
    # SHA-1 Hash
    result = hashlib.sha1(str_input.encode())
    print("SHA-1 Hash:", result.hexdigest())
    
    # SHA-256 Hash
    result256 = hashlib.sha256(str_input.encode())
    print("SHA-256 Hash:", result256.hexdigest())

sha_demo()
```

---

## Practical 4: Digital Signature with RSA and Hashing

### **AIM**
Using RSA with SHA-256 to sign and verify message integrity.

```python
import rsa
import hashlib

def digital_signature_demo():
    # Generate RSA key pair
    public_key, private_key = rsa.newkeys(1024)
    
    # Message to sign
    message = b"This is a secret message"
    
    # Create hash of the message
    message_hash = hashlib.sha256(message).digest()
    print("Message:", message.decode())
    print("Message Hash:", message_hash.hex())
    
    # Sign the message
    signature = rsa.sign(message, private_key, 'SHA-256')
    print("Digital Signature:", signature.hex())
    
    # Verify the signature
    try:
        rsa.verify(message, signature, public_key)
        print("✅ Signature verification: SUCCESS")
    except rsa.VerificationError:
        print("❌ Signature verification: FAILED")
    
    # Test with tampered message
    tampered_message = b"This is a tampered message"
    try:
        rsa.verify(tampered_message, signature, public_key)
        print("✅ Tampered message verification: SUCCESS")
    except rsa.VerificationError:
        print("❌ Tampered message verification: FAILED (Expected)")

digital_signature_demo()
```

---

## Practical 5: Diffie-Hellman Key Exchange

### **AIM**
Key Exchange using Diffie-Hellman algorithm.

```python
def diffie_hellman_demo():
    # Public parameters (known to both parties)
    P = 23  # Prime modulus
    G = 9   # Generator
    
    print(f"Public Parameters:")
    print(f"P (prime) = {P}")
    print(f"G (generator) = {G}")
    
    # Alice's secret key
    a = 4
    print(f"\nAlice's private key: {a}")
    
    # Bob's secret key  
    b = 6
    print(f"Bob's private key: {b}")
    
    # Alice computes A = G^a mod P
    A = pow(G, a, P)
    print(f"\nAlice computes A = G^a mod P = {G}^{a} mod {P} = {A}")
    
    # Bob computes B = G^b mod P
    B = pow(G, b, P)
    print(f"Bob computes B = G^b mod P = {G}^{b} mod {P} = {B}")
    
    # Alice computes shared secret: ka = B^a mod P
    ka = pow(B, a, P)
    print(f"\nAlice computes shared secret: ka = B^a mod P = {B}^{a} mod {P} = {ka}")
    
    # Bob computes shared secret: kb = A^b mod P
    kb = pow(A, b, P)
    print(f"Bob computes shared secret: kb = A^b mod P = {A}^{b} mod {P} = {kb}")
    
    print(f"\n🔐 Shared Secret Keys:")
    print(f"Alice's computed key: {ka}")
    print(f"Bob's computed key: {kb}")
    
    if ka == kb:
        print("✅ Key exchange successful! Both parties have the same shared secret.")
    else:
        print("❌ Key exchange failed!")

diffie_hellman_demo()
```

---


---

## Practical 5: Diffie-Hellman Key Exchange

### **AIM**
Key Exchange using Diffie-Hellman algorithm.

```python
def diffie_hellman_demo():
    # Public parameters (known to both parties)
    P = 23  # Prime modulus
    G = 9   # Generator
    
    print(f"Public Parameters:")
    print(f"P (prime) = {P}")
    print(f"G (generator) = {G}")
    
    # Alice's secret key
    a = 4
    print(f"\nAlice's private key: {a}")
    
    # Bob's secret key  
    b = 6
    print(f"Bob's private key: {b}")
    
    # Alice computes A = G^a mod P
    A = pow(G, a, P)
    print(f"\nAlice computes A = G^a mod P = {G}^{a} mod {P} = {A}")
    
    # Bob computes B = G^b mod P
    B = pow(G, b, P)
    print(f"Bob computes B = G^b mod P = {G}^{b} mod {P} = {B}")
    
    # Alice computes shared secret: ka = B^a mod P
    ka = pow(B, a, P)
    print(f"\nAlice computes shared secret: ka = B^a mod P = {B}^{a} mod {P} = {ka}")
    
    # Bob computes shared secret: kb = A^b mod P
    kb = pow(A, b, P)
    print(f"Bob computes shared secret: kb = A^b mod P = {A}^{b} mod {P} = {kb}")
    
    print(f"\n🔐 Shared Secret Keys:")
    print(f"Alice's computed key: {ka}")
    print(f"Bob's computed key: {kb}")
    
    if ka == kb:
        print("✅ Key exchange successful! Both parties have the same shared secret.")
    else:
        print("❌ Key exchange failed!")

diffie_hellman_demo()
```

---
---

## Practical 5: Diffie-Hellman Key Exchange

### **AIM**
Key Exchange using Diffie-Hellman algorithm.

```python
def diffie_hellman_demo():
    # Public parameters (known to both parties)
    P = 23  # Prime modulus
    G = 9   # Generator
    
    print(f"Public Parameters:")
    print(f"P (prime) = {P}")
    print(f"G (generator) = {G}")
    
    # Alice's secret key
    a = 4
    print(f"\nAlice's private key: {a}")
    
    # Bob's secret key  
    b = 6
    print(f"Bob's private key: {b}")
    
    # Alice computes A = G^a mod P
    A = pow(G, a, P)
    print(f"\nAlice computes A = G^a mod P = {G}^{a} mod {P} = {A}")
    
    # Bob computes B = G^b mod P
    B = pow(G, b, P)
    print(f"Bob computes B = G^b mod P = {G}^{b} mod {P} = {B}")
    
    # Alice computes shared secret: ka = B^a mod P
    ka = pow(B, a, P)
    print(f"\nAlice computes shared secret: ka = B^a mod P = {B}^{a} mod {P} = {ka}")
    
    # Bob computes shared secret: kb = A^b mod P
    kb = pow(A, b, P)
    print(f"Bob computes shared secret: kb = A^b mod P = {A}^{b} mod {P} = {kb}")
    
    print(f"\n🔐 Shared Secret Keys:")
    print(f"Alice's computed key: {ka}")
    print(f"Bob's computed key: {kb}")
    
    if ka == kb:
        print("✅ Key exchange successful! Both parties have the same shared secret.")
    else:
        print("❌ Key exchange failed!")

diffie_hellman_demo()
```

---
---

## Practical 5: Diffie-Hellman Key Exchange

### **AIM**
Key Exchange using Diffie-Hellman algorithm.

```python
def diffie_hellman_demo():
    # Public parameters (known to both parties)
    P = 23  # Prime modulus
    G = 9   # Generator
    
    print(f"Public Parameters:")
    print(f"P (prime) = {P}")
    print(f"G (generator) = {G}")
    
    # Alice's secret key
    a = 4
    print(f"\nAlice's private key: {a}")
    
    # Bob's secret key  
    b = 6
    print(f"Bob's private key: {b}")
    
    # Alice computes A = G^a mod P
    A = pow(G, a, P)
    print(f"\nAlice computes A = G^a mod P = {G}^{a} mod {P} = {A}")
    
    # Bob computes B = G^b mod P
    B = pow(G, b, P)
    print(f"Bob computes B = G^b mod P = {G}^{b} mod {P} = {B}")
    
    # Alice computes shared secret: ka = B^a mod P
    ka = pow(B, a, P)
    print(f"\nAlice computes shared secret: ka = B^a mod P = {B}^{a} mod {P} = {ka}")
    
    # Bob computes shared secret: kb = A^b mod P
    kb = pow(A, b, P)
    print(f"Bob computes shared secret: kb = A^b mod P = {A}^{b} mod {P} = {kb}")
    
    print(f"\n🔐 Shared Secret Keys:")
    print(f"Alice's computed key: {ka}")
    print(f"Bob's computed key: {kb}")
    
    if ka == kb:
        print("✅ Key exchange successful! Both parties have the same shared secret.")
    else:
        print("❌ Key exchange failed!")

diffie_hellman_demo()
```

---
