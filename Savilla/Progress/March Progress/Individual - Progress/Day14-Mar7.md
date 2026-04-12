# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Mar 7, 2026 </ins> | **Training Day:** <ins>14</ins>/180 (or <ins>14</ins>/90 for 3-month plan)

### 1.<u> Time Investment</u>

- [x] Training time today: <ins>2</ins> hours
- [x] Goal met? (<ins>Yes</ins>/No)
- [x] Consistency streak: __<ins>2</ins>__ days

**Points:**

- 2+ hours = <ins>10 points</ins>
- 1-2 hours = 5 points
- <1 hour = 2 points
- Missed day = 0 points (streak resets)

### 2. Challenge Completion

| Difficulty      | Challenges Solved | Points Earned |
| --------------- | ----------------- | ------------- |
| Easy            | <ins>6</ins> × 5 pts     | __<ins>30</ins>__         |
| Medium          | _____ × 15 pts    | _____         |
| Hard            | _____ × 30 pts    | _____         |
| Expert          | _____ × 50 pts    | _____         |
| **Daily Total** |                   | **<ins>30</ins>**     |

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
- [ ] Reverse Engineering
- [ ] Forensics
- [ ] OSINT
- [ ] Other: ___________

**Primary Specialty:** __<ins>120</ins>__ minutes

**Secondary Specialty:** _____ minutes

**Other Categories:** _____ minutes

### 5. Reflection (Qualitative)

**What went well today?**
<ins>This was my first time learning about heap exploitation. I learned that memory in a C program is not just stored on the stack but also on something called the heap, which is where dynamically allocated variables live. I learned that if a program does not check how much data a user inputs, you can overflow one variable and overwrite another one sitting next to it in memory. I was able to use this technique on the Heap 0 challenge in picoCTF and successfully get the flag.</ins>

**What challenged you?**
<ins>At first I did not understand why overflowing one variable would affect another. But after reading the writeup and looking at the heap addresses printed by the program I realized the two variables were stored right next to each other in memory. Once I understood that I just had to figure out the right number of characters to type to overflow into the second variable and trigger the flag.</ins>

**Key learning:**
<ins>Heap memory, heap overflow attacks, how malloc allocates variables next to each other, and how to use that to overwrite a nearby variable by inputting more data than the program expects.</ins>

**Tomorrow's focus:**
<ins>More binary exploitation challenges and going deeper into how heap and memory vulnerabilities can be chained together.</ins>
