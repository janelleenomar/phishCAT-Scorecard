# 📊 Weekly Progress Summary

**Week:** 2 of 4
**Dates:** 03/08/2026 to 03/15/2026

---

# Weekly Metrics

| Metric                 | Target | Actual | Status |
| ---------------------- | ------ | ------ | ------ |
| Training Hours         | 15–20  | 10     | ✗      |
| Challenges Solved      | 15–25  | 6      | ✗      |
| Live CTF Participated  | 1–2    | 0      | ✗      |
| CTF Challenges Solved  | 2–5    | 0      | ✗      |
| Writeups Created       | 3–5    | 4      | ✓      |
| New Techniques Learned | 2–3    | 4      | ✓      |

---

# Weekly Points Breakdown

| Source                | Points  |
| -------------------- | ------- |
| Training Hours       | 9.5      |
| Challenges Completed | 95      |
| Quality Bonuses      | 80      |
| Live CTF Performance | 0       |
| Writeups & Learning  | 60      |
| **Weekly Total** | **244.5** |

---

# Category Distribution (Hours This Week)

```
Web Exploitation:    10 hours [==========] 100%
AI Safety/Injection:  0 hours [          ] 0%
Binary Exploitation:  0 hours [          ] 0%
Cryptography:         0 hours [          ] 0%
Reverse Engineering:  0 hours [          ] 0%
Forensics:            0.0 hours [          ] 0%
OSINT:                0.0 hours [          ] 0%
Linux Fundamentals:   0.0 hours [          ] 0%
```

---

# Skill Level Assessment (Self-Rated 1–10)

| Specialty                        | Last Week | This Week | Change |
| ------------------------------- | --------- | --------- | ------ |
| Primary #1 (SQL Injection)      | 1         | 4         | +3     |
| Primary #2 (Client-Side Recon)  | 2         | 4         | +2     |
| Secondary (SSTI)                | 1         | 3         | +2     |

---

# Weekly Achievements

* [x] **Database Breakthrough:** Mastered authentication bypass and WHERE clause manipulation in SQL.
* [x] **WAF Specialist:** Successfully used XML hex encoding and Hackverter to bypass a Web Application Firewall.
* [x] **Code Detective:** Found hardcoded credentials in JS source files and manipulated session cookies.
* [x] **Template Explorer:** Successfully executed first Server-Side Template Injection (SSTI) payload.

---

# Weekly Challenges & Lessons

**Biggest challenge this week**

Bypassing the WAF in the XML SQLi lab. Standard payloads were being dropped immediately, and it took significant trial and error with different encoding formats to find one that the firewall didn't inspect but the XML parser could read.

---

**How you overcame it (or plan to)**

I utilized the **Hackverter** extension in Burp Suite. By converting the SQL payload into XML hex entities, I essentially "camouflaged" the attack, allowing it to pass through the WAF safely.

---

**Most valuable lesson learned**

Client-side security is never sufficient. Whether it's a password check in `secure.js` or a session cookie that can be decoded and edited, any security logic that happens in the user's browser can and will be bypassed. Always validate on the server!

---

**Adjustment for next week**

Focus on **Automation**. I spent a lot of time manually testing SQL comments and encoding formats. Next week, I want to start using Burp Intruder more effectively to speed up the fuzzing process for hidden parameters and directories.
