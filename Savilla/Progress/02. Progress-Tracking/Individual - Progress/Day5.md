# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Feb 14, 2026 </ins> | **Training Day:** <ins>5</ins>/180 (or <ins>5</ins>/90 for 3-month plan)

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
<ins>I was able to solve the Corp Website challenge on TryHackMe by identifying the Next.js framework, finding a known CVE using nuclei, exploiting it to get remote code execution, and then escalating to root through a misconfigured sudo rule to retrieve both flags.</ins>

**What challenged you?**
<ins>I was stuck at the start because manual exploration and directory enumeration with ffuf gave me nothing useful. I had to shift my thinking and focus on the framework itself rather than the app's features, which led me to run nuclei and find the CVE.</ins>

**Key learning:**
<ins>I learned how to chain two vulnerabilities together to fully compromise a machine. First, I used nuclei to identify CVE-2025-55182 on the Next.js app, then used a public exploit to get remote code execution and find the user flag. After getting a reverse shell, I ran sudo -l and discovered that the user daniel could run python3 as root with no password. I used that to spawn a root shell and read the root flag from /root/root.txt.</ins>

**Tomorrow's focus:**
<ins>More CTF challenges and learning more about privilege escalation techniques and how to use nuclei for vulnerability scanning.</ins>
