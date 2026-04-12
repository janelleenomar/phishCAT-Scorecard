# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Mar 8, 2026 </ins> | **Training Day:** <ins>15</ins>/180 (or <ins>15</ins>/90 for 3-month plan)

### 1.<u> Time Investment</u>

- [x] Training time today: <ins>3.5</ins> hours
- [x] Goal met? (<ins>Yes</ins>/No)
- [x] Consistency streak: __<ins>0</ins>__ days

**Points:**

- 2+ hours = 10 points
- 1-2 hours = 5 points
- <1 hour = 2 points
- Missed day = 0 points (streak resets)

### 2. Challenge Completion

| Difficulty      | Challenges Solved | Points Earned |
| --------------- | ----------------- | ------------- |
| Easy            | <ins>4</ins> × 5 pts     | __<ins>20</ins>__         |
| Medium          | _____ × 15 pts    | _____         |
| Hard            | _____ × 30 pts    | _____         |
| Expert          | _____ × 50 pts    | _____         |
| **Daily Total** |                   | **<ins>20</ins>**     |

### 3. Quality Indicators

- [x] Created writeup for at least 1 challenge (+10 pts)
- [x] Reviewed 3+ writeups from others (+5 pts)
- [x] Learned new technique/tool (+10 pts)
- [x] Updated cheat sheet (+5 pts)
- [x] Practiced timed challenge (+5 pts)

**Quality Points Total:** <ins>35</ins>

### 4. Category Focus Today

Which categories did you practice?

- [ ] Web Exploitation
- [x] Binary Exploitation / Pwn
- [ ] Cryptography
- [x] Reverse Engineering
- [ ] Forensics
- [ ] OSINT
- [ ] Other: ___________

**Primary Specialty:** <ins>180</ins> minutes

**Secondary Specialty:** <ins>30</ins> minutes

**Other Categories:** _____ minutes

5. Reflection (Qualitative)
What went well today?
<ins>This was another binary exploitation challenge but this time it went deeper into format string vulnerabilities. I learned that when a C program uses printf incorrectly by passing user input directly as the format argument, an attacker can use special format specifiers like %p or %x to read raw values sitting in the stack memory. By sending a long chain of these specifiers I was able to dump hex values from the stack which contained parts of the hidden flag. I then used CyberChef to convert those hex values into readable text and rearranged them in the correct order to get the full flag.</ins>
What challenged you?
<ins>The trickiest part was understanding that the hex values were stored in reverse order due to something called endianness. The data I got back from the stack looked scrambled at first but after learning that I needed to reverse each value and reorder them I was able to piece together the flag correctly.</ins>
Key learning:
<ins>Format string vulnerabilities using %p and %x, how to leak stack memory through printf, understanding endianness and why bytes appear reversed, and using CyberChef to convert and rearrange hex values into the final flag.</ins>
Tomorrow's focus:
<ins>More binary exploitation challenges and getting more comfortable reading and manipulating raw memory output from vulnerable programs.</ins>
