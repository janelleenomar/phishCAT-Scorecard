# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Mar 18, 2026 </ins> | **Training Day:** <ins>21</ins>/180 (or <ins>21</ins>/90 for 3-month plan)

### 1.<u> Time Investment</u>

- [x] Training time today: <ins>2</ins> hours
- [x] Goal met? (<ins>Yes</ins>/No)
- [x] Consistency streak: __<ins>2</ins>__ days

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

**Primary Specialty:** <ins>120</ins> minutes
**Secondary Specialty:** <ins></ins> minutes
**Other Categories:** _____ minutes

### 5. Reflection (Qualitative)

**What went well today?**
<ins>This was my first time learning about environment variable injection as an exploitation technique. I learned that some programs rely on environment variables to determine what they do and if those variables are not properly sanitized a user can inject extra commands into them. In the VNE challenge there was a binary that ran ls with root permissions using a directory path stored in an environment variable called SECRET_DIR. By setting that variable to include not just a directory but also a command to read the flag file I was able to trick the binary into printing the flag even though I did not have root access myself.</ins>

**What challenged you?**
<ins>At first, I just set the environment variable to point to the root directory and could list its contents but could not read any files directly. The key insight was realizing I could append an additional shell command into the variable itself so that when the binary ran ls with my input it would also execute my injected command and print the flag file.</ins>

**Key learning:**
<ins>Environment variables and how to set them using the export command, how programs that use environment variables without sanitizing them are vulnerable to injection, and how to chain shell commands inside an environment variable to read protected files.</ins>

**Tomorrow's focus:**
<ins>More binary exploitation and Linux privilege escalation challenges, and exploring other ways environment variables and shell features can be abused.</ins>
