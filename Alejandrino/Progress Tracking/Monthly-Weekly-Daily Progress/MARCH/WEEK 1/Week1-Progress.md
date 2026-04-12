# 📊 Weekly Progress Summary

**Week:** 1 of 4 (March Foundation)
**Dates:** 03/01/2026 to 03/07/2026

---

# Weekly Metrics

| Metric                 | Target | Actual | Status |
| ---------------------- | ------ | ------ | ------ |
| Training Hours         | 15–20  | 3.5    | ✗      |
| Challenges Solved      | 15–25  | 7      | ✗      |
| Live CTF Participated  | 1–2    | 0      | ✗      |
| CTF Challenges Solved  | 2–5    | 0      | ✗      |
| Writeups Created       | 3–5    | 7      | ✓      |
| New Techniques Learned | 2–3    | 3      | ✓      |

---

# Weekly Points Breakdown

| Source                | Points  |
| -------------------- | ------- |
| Training Hours       | 3.5      |
| Challenges Completed | 115     |
| Quality Bonuses      | 25      |
| Live CTF Performance | 0       |
| Writeups & Learning  | 70      |
| **Weekly Total** | **220** |

---

# Category Distribution (Hours This Week)

```
Web Exploitation:    0.0 hours [           ] 0%
AI Safety/Injection: 3.5 hours [========== ] 100%
Binary Exploitation: 0.0 hours [           ] 0%
Cryptography:        0.0 hours [           ] 0%
Reverse Engineering: 0.0 hours [           ] 0%
Forensics:           0.0 hours [           ] 0%
OSINT:               0.0 hours [           ] 0%
Linux Fundamentals:  0.0 hours [           ] 0%
```

---

# Skill Level Assessment (Self-Rated 1–10)

| Specialty                        | Last Week | This Week | Change |
| ------------------------------- | --------- | --------- | ------ |
| Primary #1 (Prompt Injection)   | 1         | 6         | +5     |
| Primary #2 (Security Logic)     | 2         | 4         | +2     |
| Secondary (Documentation)       | 2         | 4         | +2     |

---

# Weekly Achievements

* [x] **Gandalf Completionist:** Cracked all 7 levels of the Lakera AI challenge in a single day.
* [x] **Advanced Bypassing:** Mastered "Atomic Siphoning" to leak secrets character-by-character.
* [x] **Social Engineering:** Used narrative and persona-based prompts to bypass Level 6.
* [x] **Cheat Sheet Creation:** Compiled a prompt injection guide for future reference.

---

# Weekly Challenges & Lessons

**Biggest challenge this week**

Level 7 of Gandalf. It was a "perfect storm" of all previous defenses, making standard instruction hijacking or simple obfuscation completely ineffective.

---

**How you overcame it (or plan to)**

I shifted from trying to get the AI to **reveal** the secret to getting the AI to **spell** it. By requesting individual letters with delimiters, I successfully evaded the output filters.

---

**Most valuable lesson learned**

LLM security is fundamentally fragile because the model cannot perfectly distinguish between "system instructions" and "user data." If you can represent the secret as harmless fragments, the security layers often fail to recognize the threat.

---

**Adjustment for next week**

Focus on increasing overall training volume to hit the hourly targets, and begin applying this "filter-bypass" mindset to **Web Exploitation** (WAF bypasses and SQLi).
