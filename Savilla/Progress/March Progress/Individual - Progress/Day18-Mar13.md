# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Mar 13, 2026 </ins> | **Training Day:** <ins>18</ins>/180 (or <ins>18</ins>/90 for 3-month plan)

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
- [x] Binary Exploitation / Pwn
- [ ] Cryptography
- [ ] Reverse Engineering
- [ ] Forensics
- [ ] OSINT
- [ ] Other: ___________

**Primary Specialty:** <ins>180</ins> minutes
**Secondary Specialty:** <ins> </ins> minutes
**Other Categories:** _____ minutes

### 5. Reflection (Qualitative)

**What went well today?**
<ins>This was my first time learning how to use GDB to inspect a compiled binary and find memory addresses of functions. The Picker IV challenge is a binary exploitation problem where the program asks you to enter a memory address and then jumps to it. I learned that even without PIE you still need to find the exact address of the win function first. By using GDB or objdump on the binary I was able to locate the address of the win function and simply enter it into the program to redirect execution and get the flag.</ins>

**What challenged you?**
<ins>At first I was not sure how to find the address of the win function since this was a compiled C binary and not a Python script like the previous Picker challenges. Learning to use GDB and commands like disassemble or using objdump to look up function addresses was new to me but once I found the address all I had to do was enter it.</ins>

**Key learning:**
<ins>How to use GDB and objdump to inspect binary files and find function addresses, how programs use function pointers to jump to memory addresses, and how simply supplying a known function address can redirect program execution to a win function.</ins>

**Tomorrow's focus:**
<ins>More binary exploitation challenges and getting more practice with GDB for analyzing binaries.</ins>
