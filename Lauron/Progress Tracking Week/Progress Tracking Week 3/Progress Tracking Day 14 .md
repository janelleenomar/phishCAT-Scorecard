# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** February 20, 2026 | **Training Day:** 14/90

### 1. Time Investment

- [x] Training time today: 2 hours & 0 minutes
- [x] Goal met? Yes
- [x] Consistency streak: 12 days

**Points:**

- 2+ hours = 10 points
- 1-2 hours = 5 points
- <1 hour = 2 points
- Missed day = 0 points (streak resets)

**Total Points Today: 10**

---

### 2. Challenge Completion

| Difficulty      | Challenges Solved | Points Earned |
| --------------- | ----------------- | ------------- |
| Easy            | 0 × 5 pts         | 0             |
| Medium          | 1 × 15 pts        | 15            |
| Hard            | 0 × 30 pts        | 0             |
| Expert          | 0 × 50 pts        | 0             |
| **Daily Total** |                   | **15** |

---

### 3. Quality Indicators

- [x] Created writeup for at least 1 challenge (+10 pts) -> *Challenge 7: AES-128 ECB*
- [x] Learned new technique/tool (+10 pts) -> *Block cipher decryption*
- [ ] Reviewed 3+ writeups from others (+5 pts)
- [ ] Updated cheat sheet (+5 pts)
- [ ] Practiced timed challenge (+5 pts)

**Quality Points Total: 20**

---

### 4. Category Focus Today

Which categories did you practice?

- [ ] Web Exploitation
- [ ] Binary Exploitation / Pwn
- [x] Cryptography: 120 minutes
- [ ] Reverse Engineering
- [ ] Forensics
- [ ] OSINT
- [ ] Other: ___________

**Primary Specialty:** 120 minutes

**Secondary Specialty:** _____ minutes

---

### 5. Reflection (Qualitative)

**What went well today?**
I finally cracked Challenge 7! After days of troubleshooting the AES-128 ECB implementation, seeing the decrypted text was a huge relief. It confirmed that my data handling and library usage are finally aligned.

**What challenged you?**
Moving on to Challenge 8 (Detect AES in ECB mode) was a tough jump. I’m currently only "half of half way there." Identifying the patterns in the hex strings is proving much more complex than just running a decryption function, and I'm still trying to wrap my head around the statistical approach needed to detect the repetition.

---

**Key learning:**
I learned how to successfully implement AES decryption using standard libraries. For Challenge 8, I've started researching how ECB mode lacks a randomizing vector, which means identical blocks of plaintext result in identical blocks of ciphertext—this is the "tell" I need to exploit.

---

**Tomorrow's focus:**
February 21—Deepening the analysis for **Challenge 8**. I need to write a script that can count recurring 16-byte blocks to spot the ECB signature among the provided hex strings.

---
