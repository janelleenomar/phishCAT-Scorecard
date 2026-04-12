# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Mar 25, 2026 </ins> | **Training Day:** <ins>25</ins>/180 (or <ins>25</ins>/90 for 3-month plan)

### 1.<u> Time Investment</u>

- [x] Training time today: <ins>3</ins> hours
- [x] Goal met? (<ins>Yes</ins>/No)
- [x] Consistency streak: __<ins>3</ins>__ days

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
**Secondary Specialty:** <ins></ins> minutes
**Other Categories:** _____ minutes

### 5. Reflection (Qualitative)

**What went well today?**
<ins>This was a step up from Buffer Overflow 1 because this time it was not enough to just redirect execution to the win function. The win function also checked two specific argument values before printing the flag so I had to not only overflow the buffer and overwrite the return address but also place the correct argument values onto the stack in the right positions. I learned how function arguments are laid out on the stack in 32 bit programs and how overflowing past the return address lets you control what those arguments look like. Using GDB with breakpoints I was able to inspect memory at each comparison and confirm that my payload was placing the right values in the right spots before finally getting the flag.</ins>

**What challenged you?**
<ins>The hardest part was understanding that after overwriting the return address I needed to add 4 more bytes as a fake return address for win before placing the two argument values. Figuring out the exact position of each argument on the stack required setting breakpoints inside the win function and using the cyclic pattern technique again to measure the exact offsets. It took a lot of back and forth with GDB but seeing the memory values update correctly after each adjustment was very satisfying.</ins>

**Key learning:**
<ins>How function arguments are placed on the stack in 32 bit programs, how to craft a buffer overflow payload that controls both the return address and the arguments passed to the target function, using GDB breakpoints to inspect memory during execution, and building a full pwntools exploit script to automate the attack against a remote server.</ins>

**Tomorrow's focus:**
<ins>Continuing with more advanced buffer overflow challenges and learning about 64 bit calling conventions where arguments are passed through registers instead of the stack.</ins>
