# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Mar 14, 2026 </ins> | **Training Day:** <ins>19</ins>/180 (or <ins>19</ins>/90 for 3-month plan)

### 1.<u> Time Investment</u>

- [x] Training time today: <ins>3.5</ins> hours
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
| Easy            | ___ × 5 pts     | __<ins>5</ins>__         |
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

**Secondary Specialty:** <ins>30</ins> minutes

**Other Categories:** _____ minutes

### 5. Reflection (Qualitative)

**What went well today?**
<ins>This was my first hands on experience with a classic buffer overflow attack. I learned that when a C program uses an input buffer that is too small and does not check how much data is being written into it, you can overflow beyond the buffer and overwrite nearby variables in memory. In the Local Target challenge the goal was to make a variable called num equal to 65 because that is the condition that triggers the flag to print. Since the input buffer was only 16 bytes long I crafted a payload that filled those 16 bytes and then added the character A at the end since A has an ASCII value of 65 which then overwrote num and printed the flag.</ins>

**What challenged you?**
<ins>The tricky part was figuring out exactly how many characters I needed to type before the overflow would reach and overwrite the num variable. It took a bit of trial and error to get the right length but once I understood how memory is laid out in the stack and that variables sit next to each other it all made sense.</ins>

**Key learning:**
<ins>Buffer overflow basics, how adjacent variables in memory can be overwritten by exceeding a buffer's size, ASCII values and how they map to characters, and how to craft a simple overflow payload manually without any special tools.</ins>

**Tomorrow's focus:**
<ins>More buffer overflow challenges and learning how to overflow the stack to overwrite return addresses and redirect program execution.</ins>
