# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Feb 15, 2026 </ins> | **Training Day:** <ins>6</ins>/180 (or <ins>6</ins>/90 for 3-month plan)

### 1.<u> Time Investment</u>

- [x] Training time today: <ins>3</ins> hours
- [x] Goal met? (<ins>Yes</ins>/No)
- [x] Consistency streak: __<ins>2</ins>__ days

**Points:**

- 2+ hours = <ins>10</ins> points
- 1-2 hours = 5 points
- <1 hour = 2 points
- Missed day = 0 points (streak resets)

### 2. Challenge Completion

| Difficulty      | Challenges Solved | Points Earned |
| --------------- | ----------------- | ------------- |
| Easy            | ___ × 5 pts     | __<ins></ins>__         |
| Medium          | <ins>1</ins> × 15 pts    | <ins>15</ins>         |
| Hard            | _____ × 30 pts    | _____         |
| Expert          | _____ × 50 pts    | _____         |
| **Daily Total** |                   | **<ins>15</ins>**     |

### 3. Quality Indicators

- [x] Created writeup for at least 1 challenge (+10 pts)
- [x] Reviewed 3+ writeups from others (+5 pts)
- [x] Learned new technique/tool (+10 pts)
- [ ] Updated cheat sheet (+5 pts)
- [x] Practiced timed challenge (+5 pts)

**Quality Points Total:** <ins>30</ins>
### 4. Category Focus Today
Which categories did you practice?
- [ ] Web Exploitation
- [ ] Binary Exploitation / Pwn
- [x] Cryptography
- [ ] Reverse Engineering
- [ ] Forensics
- [ ] OSINT
- [ ] Other: ___________

**Primary Specialty:** <ins>180</ins> minutes
**Secondary Specialty:** <ins> </ins> minutes
**Other Categories:** _____ minutes

### 5. Reflection (Qualitative)

**What went well today?**
<ins>I was able to solve the When Hearts Collide challenge on TryHackMe by understanding what a hash collision is and using the fastcoll Docker tool to generate two different files with the same MD5 hash, then uploading them to the app to get the flag.</ins>

**What challenged you?**
<ins>I was stuck at the beginning because I was not immediately sure how to generate a hash collision in practice. I knew what MD5 collisions were in theory, but finding and using the right tool to actually create the colliding files took some time to figure out.</ins>

**Key learning:**
<ins>I learned that MD5 is a broken hashing algorithm that can be exploited using collision attacks. By using the brimstone/fastcoll Docker image with an existing image as a prefix file, I was able to generate two new files — twin_a.jpg and twin_b.jpg — that had completely different content but the exact same MD5 hash. Uploading both to the app tricked it into accepting them as a match and revealed the flag.</ins>

**Tomorrow's focus:**
<ins>More CTF challenges and learning more about cryptographic hash functions, why MD5 is no longer safe, and how SHA-256 and SHA-3 are better alternatives.</ins>
