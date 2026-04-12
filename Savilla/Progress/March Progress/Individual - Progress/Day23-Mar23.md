# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Mar 23, 2026 </ins> | **Training Day:** <ins>23</ins>/180 (or <ins>23</ins>/90 for 3-month plan)

### 1.<u> Time Investment</u>

- [x] Training time today: <ins>3</ins> hours
- [x] Goal met? (<ins>Yes</ins>/No)
- [x] Consistency streak: __<ins>1</ins>__ days

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

**Primary Specialty:** <ins>180</ins> minutes
**Secondary Specialty:** <ins></ins> minutes
**Other Categories:** _____ minutes

### 5. Reflection (Qualitative)

**What went well today?**
<ins>This was my first time learning how to overwrite a return address using a buffer overflow to redirect program execution to a function that was never meant to be called. In the Buffer Overflow 1 challenge I learned that when a 32 bit program returns from a function it pops a 4 byte value off the stack and jumps to it. By overflowing the input buffer with the right number of padding bytes followed by the address of the win function I was able to hijack the return address and make the program jump to win instead of going back to main. I also learned how to use pwntools to script the entire exploit including finding the win function address automatically from the binary.</ins>

**What challenged you?**
<ins>The trickiest part was figuring out exactly how many bytes of padding were needed before the return address gets overwritten. I learned to use the cyclic and cyclic_find functions in pwntools to generate a unique pattern, feed it to the program in a debugger, and then find exactly where in that pattern the program crashed to calculate the offset which turned out to be 44 bytes.</ins>

**Key learning:**
<ins>How return addresses work on the stack in 32 bit programs, how to calculate the overflow offset using cyclic patterns in pwntools and pwndbg, how to look up function addresses from a binary using the ELF object in pwntools, and how to construct and send a payload of padding plus an address to redirect execution.</ins>

**Tomorrow's focus:**
<ins>More buffer overflow challenges and learning about calling conventions and how to pass arguments to functions through stack based exploits.</ins>
