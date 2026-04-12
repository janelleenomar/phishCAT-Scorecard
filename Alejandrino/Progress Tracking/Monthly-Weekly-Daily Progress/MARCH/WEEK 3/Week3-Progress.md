You sent exactly 4 scorecard logs for this week. It looks like you shifted back into core web fundamentals and reconnaissance, focusing heavily on how servers and browsers communicate.

Here is your **Weekly Progress Summary** for Week 3.

# 📊 Weekly Progress Summary

**Week:** 3 of 4
**Dates:** 03/16/2026 to 03/22/2026

---

# Weekly Metrics

| Metric                 | Target | Actual | Status |
| ---------------------- | ------ | ------ | ------ |
| Training Hours         | 15–20  | 8.5    | ✗      |
| Challenges Solved      | 15–25  | 6      | ✗      |
| Live CTF Participated  | 1–2    | 0      | ✗      |
| CTF Challenges Solved  | 2–5    | 0      | ✗      |
| Writeups Created       | 3–5    | 4      | ✓      |
| New Techniques Learned | 2–3    | 4      | ✓      |

---

# Weekly Points Breakdown

| Source                | Points  |
| -------------------- | ------- |
| Training Hours       | 40      |
| Challenges Completed | 30      |
| Quality Bonuses      | 80      |
| Live CTF Performance | 0       |
| Writeups & Learning  | 60      |
| **Weekly Total** | **210** |

---

# Category Distribution (Hours This Week)

```
Web Exploitation:    7.5 hours [=========  ] 88%
Cryptography:        1.0 hour  [=         ] 12%
Binary Exploitation: 0.0 hours [          ] 0%
Reverse Engineering: 0.0 hours [          ] 0%
Forensics:           0.0 hours [          ] 0%
OSINT:               0.0 hours [          ] 0%
Linux Fundamentals:  0.0 hours [          ] 0%
```

---

# Skill Level Assessment (Self-Rated 1–10)

| Specialty                        | Last Week | This Week | Change |
| ------------------------------- | --------- | --------- | ------ |
| Primary #1 (Web Reconnaissance) | 3         | 5         | +2     |
| Primary #2 (HTTP Manipulation)  | 2         | 4         | +2     |
| Secondary (Code De-obfuscation) | 1         | 3         | +2     |

---

# Weekly Achievements

* [x] **Header Hero:** Successfully bypassed server restrictions using `User-Agent` and `Referer` spoofing in "Head Dump."
* [x] **Crawler Insights:** Mastered the use of `robots.txt` for finding hidden administrative paths.
* [x] **De-obfuscation:** Used prettifiers and manual analysis to defeat minified JavaScript in "Unminify."
* [x] **Source Deep-Dive:** Successfully reconstructed flags split across HTML, CSS, and JS files.

---

# Weekly Challenges & Lessons

**Biggest challenge this week**

Analyzing minified code in the "Unminify" challenge. When logic is compressed into a single line without meaningful variable names, it's very easy to lose track of the data flow.

---

**How you overcame it (or plan to)**

I used browser-based Prettifier tools to restore the code's indentation and then used the **Burp Suite Repeater** and browser **DevTools** to monitor how those scripts interacted with the server.



---

**Most valuable lesson learned**

"Security through Obscurity" is a major pitfall for developers. Minifying code or hiding strings in CSS classes doesn't stop an attacker; it only slows them down. If the data is sent to the client's browser, it should be considered public.

---

**Adjustment for next week**

The training hours are slightly below target. To hit the 15-hour mark next week, I plan to engage with **Session Management** vulnerabilities and **Cross-Site Scripting (XSS)**, which usually require longer debugging sessions.
