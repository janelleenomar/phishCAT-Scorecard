# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** February 07, 2026 | **Training Day:** 2/90

### 1. Time Investment

- [x] Training time today: 2 hours 0 minutes
- [x] Goal met? **Yes**
- [x] Consistency streak: **2 days**

**Points:** 10 (2+ hours)

---

### 2. Challenge Completion

| Difficulty      | Challenges Solved | Points Earned |
| --------------- | ----------------- | ------------- |
| Easy            |       1 × 5 pts   |        5      |
| Medium          |       0 × 15 pts  |        0      |
| Hard            |       0 × 30 pts  |        0      |
| Expert          |       0 × 50 pts  |        0      |
| **Daily Total** |                   |     **5** |

---

### 3. Quality Indicators

- [x] Created writeup for at least 1 challenge (+10 pts)
- [ ] Reviewed 3+ writeups from others (+5 pts)
- [x] Learned new technique/tool (+10 pts)
- [x] Updated cheat sheet (+5 pts)
- [ ] Practiced timed challenge (+5 pts)

**Quality Points Total: 25**

---

### 4. Category Focus Today

- [ ] Web Exploitation
- [ ] Binary Exploitation / Pwn
- [x] Cryptography
- [ ] Reverse Engineering
- [ ] Forensics
- [ ] OSINT

**Primary Specialty (Cryptography):** 120 minutes

---

### 5. Reflection (Qualitative)

**What went well today?**
After the struggle of Day 1, moving into **Challenge 2** felt much more controlled. I successfully implemented a bitwise XOR function to combine two hex buffers. Seeing the output match the expected result gave me a huge boost in confidence regarding my Python setup.

**What challenged you?**
The challenge was ensuring the two buffers were exactly the same length before performing the operation. I had to be careful with how Python handles byte objects versus strings to avoid "TypeError" messages when doing the actual math.

---

**Key learning:**
I learned the fundamental rule of a Fixed XOR: the buffers must be equal in length. I also practiced using a `for` loop to iterate through two byte arrays simultaneously to create a new XORed result.



---

**Tomorrow's focus:**
Resting up so I can tackle **Challenge 3** on Feb 9th. I need to start learning about "Single-byte XOR" and how to automate the search for a hidden message using character frequency.
