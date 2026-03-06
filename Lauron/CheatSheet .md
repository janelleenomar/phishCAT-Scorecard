# 🔐 General Cryptography & Data Master Cheat Sheet

---

## 🚀 Best Languages for Crypto Operations

| Language | Strengths | Best For... |
| :--- | :--- | :--- |
| **Python** | Huge libraries (`PyCryptodome`), easy syntax, rapid prototyping. | **CTFs, Scripting, & Research.** |
| **C / C++** | Blazing fast performance, low-level memory control. | **Core Crypto Libraries** (like OpenSSL). |
| **Java** | Strong built-in security providers (`JCA/JCE`), strictly typed. | **Enterprise Apps & Android Security.** |
| **Rust** | Memory safety by default, prevents common buffer overflow bugs. | **Modern, Secure System Tools.** |

---

## 🌐 Learning & Practice Hub

| Category | Website / Resource | Purpose |
| :--- | :--- | :--- |
| **Practice** | **Cryptopals** | The gold standard for learning crypto by breaking it. |
| **Practice** | **picoCTF** | Beginner-friendly challenges covering many security domains. |
| **Practice** | **CryptoHack** | A fun, modern platform for learning cryptography through puzzles. |
| **Learning** | **Practical Cryptography** | Great for understanding classical ciphers and frequency analysis. |
| **Learning** | **Trail of Bits (Guides)** | Professional-grade deep dives into modern crypto security. |
| **Learning** | **Coursera (Stanford)** | Dan Boneh's Crypto course for heavy-duty mathematical theory. |

---

## 💻 Essential Data Manipulation (Python)

| Functionality | Usage | Example | Description |
| :--- | :--- | :--- | :--- |
| **Base64 Decode** | `base64.b64decode([str])` | `base64.b64decode("ZmxhZw==")` | Converts a Base64 string into raw bytes. |
| **Base64 Encode** | `base64.b64encode([bytes])` | `base64.b64encode(b"flag")` | Converts raw bytes into a Base64 string. |
| **Hex to Bytes** | `bytes.fromhex([str])` | `bytes.fromhex("48656c")` | Converts a Hexadecimal string into a bytes object. |
| **Bytes to Hex** | `[bytes].hex()` | `raw_data.hex()` | Converts bytes back into a readable Hex string. |
| **Fixed XOR** | `xor_bytes(b1, b2)` | `bytes([a ^ b for a, b in zip(b1, b2)])` | Performs a bitwise XOR between two equal-length buffers. |
| **Repeating XOR**| `(key * n)[:len(data)]` | `(b"KEY" * 10)[:len(p)]` | Applies a short key repeatedly across a longer data set. |
| **Hamming Dist** | `bin(b1 ^ b2).count('1')` | `sum(bin(x ^ y).count('1')...)` | Calculates the bitwise difference between two strings. |
| **Freq Scoring** | `score_text([bytes])` | `sum(freq.get(c, 0)...)` | Ranks data based on English character frequency. |

---

## 🔍 Pattern Recognition & Signatures

| If you see... | It is likely... | Action to take... |
| :--- | :--- | :--- |
| `SGVsbG8=` | **Base64** | Use `base64.b64decode` to see the hidden data. |
| `0x48656c6c6f` | **Hexadecimal** | Use `bytes.fromhex` to convert to raw data. |
| `89 50 4E 47` | **PNG Image** | "Magic Bytes" identifying a file as a PNG. |
| `PK` / `50 4B` | **ZIP / Office** | Indicates a compressed archive or docx/xlsx file. |

---

## 🛠️ Universal Procedures

### 1. The "Identify & Convert" Flow
* **Step 1**: Identify the encoding (Is it Hex? Base64? Binary?).
* **Step 2**: Convert to **Raw Bytes**. Python logic works best on bytes, not strings.
* **Step 3**: Apply the operation (XOR, Decrypt, or SQL Query).
* **Step 4**: Convert back to a human-readable format (String or Hex).

### 2. XOR Logic Fundamentals
* **The Rule**: If $A \oplus B = C$, then $A \oplus C = B$ and $B \oplus C = A$.
* **Application**: This is why the same XOR function can both encrypt and decrypt data.

---

## 🧮 Mathematical Reference

### Hamming Distance Logic
To calculate the bitwise difference between two bytes ($A$ and $B$):
1. Compute $X = A \oplus B$.
2. Count the number of set bits (**1**s) in $X$.
* **Example**: `0x01` (0001) and `0x03` (0011) have a Hamming Distance of **1**.

### RSA Logic (The Big Picture)
* **Public Key ($e, N$):** Used to lock (encrypt) the data.
* **Private Key ($d, N$):** Used to unlock (decrypt) the data.
* **The Math:** Security depends on the fact that $N$ is almost impossible to factor if it's large enough.

---

## 🛠️ External Tool Arsenal
* **CyberChef**: Use the "Magic" operation for auto-detecting encodings.
* **HxD**: Essential for inspecting file headers to verify "Magic Bytes."
* **RsaCtfTool**: Automates common attacks against weak RSA public keys.
* **Hashcat**: The industry standard for cracking password hashes.
