# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Feb 17, 2026 </ins> | **Training Day:** <ins>9</ins>/180 (or <ins>9</ins>/90 for 3-month plan)

### 1.<u> Time Investment</u>

- [x] Training time today: <ins>3</ins> hours
- [x] Goal met? (<ins>Yes</ins>/No)
- [x] Consistency streak: __<ins>4</ins>__ days

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
- [x] Web Exploitation
- [ ] Binary Exploitation / Pwn
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
<ins>I was able to solve the More SQLi challenge on picoCTF by using a SQL injection payload to bypass the login page and retrieve the flag from the server's response using Burp Suite.</ins>

**What challenged you?**
<ins>I was stuck at the beginning trying to figure out how the login form was handling my input. It was only after I noticed the raw SQL query showing up in the response that I understood the app was vulnerable and knew what kind of payload to use.</ins>

**Key learning:**
<ins>I learned how SQL injection works in a login form. By entering test credentials first, the server revealed the raw SQL query it was running, which confirmed the vulnerability. I then used the payload ' OR 1=1; -- // in both the username and password fields to make the condition always true and bypass the login. I used Burp Suite Repeater to send the modified request and found the flag inside the server's response body.</ins>

**Tomorrow's focus:**
<ins>More CTF challenges and practicing different SQL injection techniques including extracting data from databases.</ins>
