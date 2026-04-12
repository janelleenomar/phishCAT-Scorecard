# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Mar 12, 2026 </ins> | **Training Day:** <ins>17</ins>/180 (or <ins>17</ins>/90 for 3-month plan)

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
**Secondary Specialty:** <ins> </ins> minutes
**Other Categories:** _____ minutes

### 5. Reflection (Qualitative)

**What went well today?**
<ins>This was my first time learning about PATH hijacking as an exploitation technique. I learned that when a program runs another command like md5sum without specifying its full path, the operating system searches through folders listed in the PATH variable to find it. By creating a fake md5sum script of my own and putting my folder at the front of the PATH I was able to trick the flaghasher binary into running my script instead of the real one, which then printed out the contents of the flag file. For the second part of the challenge I also learned how to escape a restricted shell called rbash which limits what commands you can run, and then applied the same PATH hijacking trick to get the flag.</ins>

**What challenged you?**
<ins>The hardest part was figuring out that the program was calling an external command rather than doing the hashing itself. Once I realized that md5sum was being called externally the PATH hijacking approach made sense. The second challenge added another layer because rbash blocked certain commands but spawning a new shell got around that restriction.</ins>

**Key learning:**
<ins>PATH hijacking, how Linux searches for commands using the PATH variable, creating fake executable scripts to intercept program behavior, and how to escape a restricted bash shell to regain full shell access.</ins>

**Tomorrow's focus:**
<ins>More binary exploitation and shell-based challenges, and learning more about Linux privilege escalation techniques.</ins>
