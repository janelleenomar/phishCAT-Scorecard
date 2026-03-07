# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** February 21, 2026 | **Training Day:** 15/90

### 1. Time Investment

- [x] Training time today: 4 hours & 0 minutes
- [x] Goal met? Yes
- [x] Consistency streak: 13 days

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

- [x] Created writeup for at least 1 challenge (+10 pts)
- [x] Learned new technique/tool (+10 pts)
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

**Primary Specialty:** 240 minutes

**Secondary Specialty:** _____ minutes

---

### 5. Reflection (Qualitative)

**What went well today?**
Challenge 8 is complete! After being "half of half way there" yesterday and spent a lot of hours because I forgot what to do, I successfully wrote a script to scan the hex strings for repeating 16-byte blocks. Finding the one ciphertext that had a duplicate block was the "aha!" moment that proved it was encrypted with ECB.

**What challenged you?**
The main challenge was handling the raw hex data correctly and ensuring the block slicing was precise. It took a few tries to make sure I wasn't off-by-one when splitting the 16-character strings, but once the logic clicked, the pattern became obvious. Also the part when I had to re do it again over and over because I forgot what I did yesterday.

---

**Key learning:**
I learned why ECB is insecure: it is deterministic. Because it lacks an Initialization Vector (IV), the same plaintext block always produces the same ciphertext block. This makes it vulnerable to simple pattern recognition even if you can't actually "decrypt" the message.

---

**Tomorrow's focus:**
REEEEEEEEEEESSSSSSSSSSSSSSTTTTTTTTTTTTTTTTTTTTT

---
