# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Mar 11, 2026 </ins> | **Training Day:** <ins>16</ins>/180 (or <ins>16</ins>/90 for 3-month plan)

### 1.<u> Time Investment</u>

- [x] Training time today: <ins>2</ins> hours
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
| Easy            | <ins>1</ins> × 5 pts     | __<ins>5</ins>__         |
| Medium          | <ins>1</ins> × 15 pts    | <ins>15</ins>         |
| Hard            | _____ × 30 pts    | _____         |
| Expert          | _____ × 50 pts    | _____         |
| **Daily Total** |                   | **<ins>20</ins>**     |

### 3. Quality Indicators

- [x] Created writeup for at least 1 challenge (+10 pts)
- [ ] Reviewed 3+ writeups from others (+5 pts)
- [x] Learned new technique/tool (+10 pts)
- [x] Updated cheat sheet (+5 pts)
- [x] Practiced timed challenge (+5 pts)

**Quality Points Total:** <ins>30</ins>

### 4. Category Focus Today

Which categories did you practice?

- [ ] Web Exploitation
- [x] Binary Exploitation / Pwn
- [ ] Cryptography
- [ ] Reverse Engineering
- [ ] Forensics
- [ ] OSINT
- [ ] Other: ___________

**Primary Specialty:** <ins>180</ins> minutes

**Secondary Specialty:** <ins>30</ins> minutes

**Other Categories:** _____ minutes

### 5. Reflection (Qualitative)

**What went well today?**
<ins>This was my first time learning about PIE which stands for Position Independent Executable. I learned that when a program has PIE enabled the operating system loads it at a random memory address every time it runs which makes it harder to attack because you cannot just hardcode the address of a function you want to jump to. However I also learned that even though the base address changes every run the distance or offset between two functions always stays the same. The program helpfully prints the address of main each time it runs so I used that leaked address along with the fixed offset between main and win to calculate exactly where the win function was and jumped to it to get the flag.</ins>

**What challenged you?**
<ins>At first I did not understand why I could not just use a fixed address for the win function. Once I understood that PIE randomizes the base address each run everything clicked. The tricky part was using GDB on the local binary to find the offset between main and win then applying that same offset to the address leaked by the remote server.</ins>

**Key learning:**
<ins>What PIE is and why it makes exploitation harder, how function offsets stay constant even when base addresses are randomized, using GDB to find memory addresses locally, and calculating a runtime address by subtracting the offset from a leaked address.</ins>

**Tomorrow's focus:**
<ins>More binary exploitation challenges and exploring other memory protection techniques like ASLR and stack canaries.</ins>
