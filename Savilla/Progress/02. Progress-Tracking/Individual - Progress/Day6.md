# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Feb 17, 2026 </ins> | **Training Day:** <ins>6</ins>/180 (or <ins>6</ins>/90 for 3-month plan)

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
- [x] Web Exploitation
- [ ] Binary Exploitation / Pwn
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
<ins>I was able to solve the Pachinko challenge on picoCTF 2025 by figuring out how the NAND circuit API worked and using Burp Suite Intruder to fuzz the node values and get the flag.</ins>

**What challenged you?**
<ins>I was stuck at the start because the NAND simulator looked complex and I thought I needed to understand the actual circuit logic to solve it. It took me a while to realize I could just brute-force the node IDs instead.</ins>

**Key learning:**
<ins>I learned that even a complicated-looking interface can have a simple vulnerability underneath. By intercepting the POST request with Burp Suite, I saw that the circuit was just JSON with plain numbers. Using Intruder in Sniper mode with a payload of 0 to 100, I found the correct node combination by looking for the response with a different status code and longer length, which revealed the flag.</ins>

**Tomorrow's focus:**
<ins>More CTF challenges and practicing with Burp Suite fuzzing techniques.</ins>
