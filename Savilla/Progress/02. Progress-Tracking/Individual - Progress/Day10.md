# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Feb 22, 2026 </ins> | **Training Day:** <ins>5</ins>/180 (or <ins>5</ins>/90 for 3-month plan)

### 1.<u> Time Investment</u>

- [x] Training time today: <ins>3</ins> hours
- [x] Goal met? (<ins>Yes</ins>/No)
- [x] Consistency streak: __<ins>5</ins>__ days

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
**Secondary Specialty:** <ins></ins> minutes
**Other Categories:** _____ minutes

### 5. Reflection (Qualitative)

**What went well today?**
<ins>I was able to solve the Crack the Gate 2 challenge on picoCTF by bypassing the rate-limiting system using a spoofed X-Forwarded-For header and brute-forcing the login with a provided password list using Burp Suite Intruder.</ins>

**What challenged you?**
<ins>I was stuck at the start trying to understand why the login kept blocking me. It took me a while to realize the rate-limiting was based on the IP address in the X-Forwarded-For header, and that I could simply fake a different IP for every attempt to get around it.</ins>

**Key learning:**
<ins>I learned that rate-limiting based on user-controlled headers like X-Forwarded-For can be completely bypassed. By intercepting the login request in Burp Suite and setting up a Pitchfork attack in Intruder, I paired a list of 20 fake IP addresses with the 20 provided passwords. Each attempt used a different IP, tricking the server into thinking each request came from a new source. One of the attempts succeeded and revealed the flag in the response.</ins>

**Tomorrow's focus:**
<ins>More CTF challenges and learning more about how rate-limiting works and the different ways it can be bypassed.</ins>
