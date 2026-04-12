# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Mar 17, 2026 </ins> | **Training Day:** <ins>20</ins>/180 (or <ins>20</ins>/90 for 3-month plan)

### 1.<u> Time Investment</u>

- [x] Training time today: <ins>2</ins> hours
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
| Easy            | ___ × 5 pts     | __<ins>5</ins>__         |
| Medium          | <ins>1</ins> × 15 pts    | <ins>15</ins>         |
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
- [ ] Reverse Engineering
- [ ] Forensics
- [ ] OSINT
- [ ] Other: ___________

**Primary Specialty:** <ins>120</ins> minutes
**Secondary Specialty:** <ins>0</ins> minutes
**Other Categories:** _____ minutes

### 5. Reflection (Qualitative)

**What went well today?**
<ins>This was my first time learning about integer overflow as an exploitation technique. I learned that in C programs integers have a maximum value they can hold which for a 32 bit signed integer is 2,147,483,647. If you add two large positive numbers together and the result exceeds that maximum the value wraps around and becomes negative. The two-sum challenge used this concept where the program checks if the sum of two numbers is still positive and if it overflows to a negative number it triggers the flag. By entering two very large positive numbers I was able to cause an integer overflow and get the flag.</ins>

**What challenged you?**
<ins>At first the condition n1 > n1 + n2 seemed mathematically impossible for positive numbers. The hint about integer overflow helped me realize this was not a math problem but a programming vulnerability. Once I understood the maximum value of a 32 bit integer and how overflow wraps the result to a negative number it all made sense.</ins>

**Key learning:**
<ins>Integer overflow, how 32 bit signed integers have a maximum value of 2,147,483,647, how exceeding that value causes the result to wrap around to a negative number, and how this can be used to bypass conditions in a program.</ins>

**Tomorrow's focus:**
<ins>More binary exploitation challenges and exploring other types of integer vulnerabilities and how they can be abused in programs.</ins>
