# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** <ins>Mar 19, 2026 </ins> | **Training Day:** <ins>22</ins>/180 (or <ins>22</ins>/90 for 3-month plan)

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
<ins>This was by far the most advanced binary exploitation challenge I have encountered so far. The Echo Valley challenge combined several techniques I had been learning about all at once including format string vulnerabilities, PIE bypassing, and overwriting return addresses on the stack. I learned that when a program has all major protections enabled like Full RELRO, stack canaries, NX, and PIE you cannot simply overwrite the GOT table or hardcode addresses. Instead I had to first use the format string bug to leak the return address of main from the stack, then calculate where the print_flag function was located using the fixed offset between them, and finally use the format string write primitive to overwrite the return address on the stack to redirect execution to print_flag.</ins>

**What challenged you?**
<ins>This challenge took a lot more effort than the previous ones. The hardest parts were understanding that the format string vulnerability could be used not just to read but also to write to arbitrary memory addresses, figuring out which stack positions held the addresses I needed to leak, and then constructing a working write payload using pwntools. The combination of PIE, Full RELRO, and stack canaries meant every shortcut I had learned before was blocked and I had to chain multiple techniques together.</ins>

**Key learning:**
<ins>Advanced format string exploitation including using it to both leak memory addresses and overwrite the return address on the stack, how to bypass PIE by leaking a runtime address and computing offsets, what Full RELRO means and why it blocks GOT overwrites, and how to use pwntools functions like fmtstr_payload to construct write payloads.</ins>

**Tomorrow's focus:**
<ins>More advanced binary exploitation and getting more comfortable with pwntools for scripting multi step exploits.</ins>
