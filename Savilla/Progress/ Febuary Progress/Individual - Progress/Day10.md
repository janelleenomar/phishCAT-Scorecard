# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Feb 20, 2026 </ins> | **Training Day:** <ins>8</ins>/180 (or <ins>8</ins>/90 for 3-month plan)

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
- [x] Web Exploitation
- [ ] Binary Exploitation / Pwn
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
<ins>I was able to solve the SSTI2 challenge on picoCTF by bypassing the login using a NoSQL injection payload and retrieving the flag from the server's response token.</ins>

**What challenged you?**
<ins>I was stuck when my first injection payload returned an error saying "email.startsWith is not a function." I did not immediately know why it failed and had to figure out that the dollar sign in the payload was being blocked during JSON parsing.</ins>

**Key learning:**
<ins>I learned how NoSQL injection works against MongoDB login forms. By reading the source code, I found the flag was stored in a token field. I then used Burp Suite to intercept the login request and sent a payload using escaped quotes to bypass the input sanitization. Once the server accepted it and returned the token, I decoded the Base64 string using CyberChef to get the flag.</ins>

**Tomorrow's focus:**
<ins>More CTF challenges and learning more about NoSQL injection techniques and how to bypass input sanitization.</ins>
