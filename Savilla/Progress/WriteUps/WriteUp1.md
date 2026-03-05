## Challenge Write-Up — Crack the Gate 1

---

## 📌 Challenge Overview

| Field                 | Information                                 |
| :-------------------- | :------------------------------------------ |
| **Competition**       | picoCTF                                     |
| **Category**          | Web Exploitation                         |
| **Difficulty**        | Easy                                        |
| **Objective**         | Bypass the gate check and retrieve the flag |

---

## Initial Analysis

The challenge provided an exposed hidden code in the source code. Since this falls underWeb Exploit, the goal was likely:

* Inspect the program logic
* find hidden flags or codes
* Intercept the data

---

## 🔎 Step 1 — Identify the File Type

Opened the site in the browser and inspected the page source.
Found a suspicious comment that looked like gibberish (likely ROT13).
Decoded the comment — it revealed a developer backdoor header: X-Dev-Access: yes.

---

## Step 2 — Extract Readable Strings

Found HTML comment:

<!-- ABGR: Wnpx - grzcbenel olcnff: hfr urnqre "K-Qri-Npprff: lrf" -->
<!-- Remove before pushing to production! -->

## Step 3 - Decode ROT13 (example)
echo 'ABGR: Wnpx - grzcbenel olcnff: hfr urnqre "K-Qri-Npprff: lrf"' \
  | tr 'A-Za-z' 'N-ZA-Mn-za-m'
# -> NOTE: Jack - temporary bypass: use header "X-Dev-Access: yes"

### Step 4 - Using Burp Suite:

By turning on intercept mode and sending the requests to the repeater, you can access the header requests.
Edi the header requests and add 'X-Dev-Access: Yes'
---

### Step 5 - Forwarding the Request:

After sending the request, a response is replied and you can see the flag.

```text
Access Granted!
picoCTF{brut4_f0rc4_cbb8faa7}
```

Success.
![CanYouSee Challenge Description](CracktheGate1.png)
---

## 🏁 Flag

```text
picoCTF{brut4_f0rc4_cbb8faa7}```

---

## 🔬 Technical Insight

This challenge demonstrates a very common beginner mistake:

### ❌ Hardcoding sensitive values inside your files

Even though the source code isn’t visible, the compiled program still contains:

* Plain text strings that can be manipulated

These can be extracted using:

* find in source code

---

## 🎯 Key Lesson

This Web Exploit often follows this pattern:

1. Inspect the code
2. Find hidden codes
3. Use the network in dev tools
4. Use Burp Suite to intercept

---

## 🧩 Final Reflection

“Crack the Gate 1” reinforces a foundational web exploit principle:


If sensitive information exists in plaintext inside a program, it can almost always be extracted.

---
