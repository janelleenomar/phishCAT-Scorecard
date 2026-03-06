# Weekly Progress Summary

**Week:** 1 of 13 | **Dates:** February 5, 2026 to February 6, 2026

## Weekly Metrics

| Metric                 | Target | Actual | Status |
| ---------------------- | ------ | ------ | ------ |
| Training Hours         | 15-20  | 3      | ☐ ✗    |
| Challenges Solved      | 15-25  | 8      | ☐ ✗    |
| Live CTF Participated  | 1-2    | 0      | ☐ ✗    |
| CTF Challenges Solved  | 2-5    | 6      | ☐ ✓    |
| Writeups Created       | 3-5    | 2      | ☐ ✗    |
| New Techniques Learned | 2-3    | 2      | ☐ ✓    |

## Weekly Points Breakdown

| Source               | Points    |
| -------------------- | --------- |
| Training Hours       | 10        |
| Challenges Completed | 70        |
| Quality Bonuses      | 10        |
| Live CTF Performance | 0         |
| Writeups & Learning  | 40        |
| **Weekly Total** | **130** |

## Category Distribution (Hours This Week)

```text
Web Exploitation:     0 hours [        ] 0%
Binary Exploitation:  0 hours [        ] 0%
Cryptography:         0 hours [        ] 0%
Reverse Engineering:  0 hours [        ] 0%
Forensics:            3 hours [========] 100%
OSINT:                0 hours [        ] 0%
```

## Skill Level Assessment (Self-Rated 1-10)

| Specialty  | Last Week | This Week | Change |
| ---------- | --------- | --------- | ------ |
| Primary #1 | 0         | 2         | +2     |
| Primary #2 | 0         | 0         | 0      |
| Secondary  | 0         | 0         | 0      |

## Weekly Achievements

- [x] Solved first challenge in new category
- [ ] Completed difficult challenge independently
- [ ] Helped teammate solve challenge
- [x] Found new technique/exploit
- [ ] Improved solve time by 20%+
- [x] Other: Successfully built a local forensic environment with CLI tools and HxD.

## Weekly Challenges & Lessons

**Biggest challenge this week:**
Initially struggling with command-line syntax and locating practice files in browser-based VMs. Later in the week, I hit a technical wall with Binary Analysis, specifically struggling to manipulate raw file bytes using HxD when files were corrupt or lacked readable strings.

**How you overcame it (or plan to):**
I overcame the initial environment friction by ditching the browser-based VMs and setting up my own local forensic environment (installing strings.exe, exiftool.exe, and HxD directly on my PC). I built strong muscle memory with CLI tools to extract metadata quickly.

**Most valuable lesson learned:**
I learned the core digital forensics lifecycle (Preservation, Analysis, and Reporting) and the importance of the Chain of Custody. Technically, I learned that files are just sequences of bytes; tools like `strings` only show human-readable parts, but a Hex Editor reveals the entire structure and "Magic Bytes" that define the file. 

**Adjustment for next week:**
I need to bridge the gap in my Static Analysis skills by mastering HxD. I will focus on learning File Signatures (Magic Bytes) to fix corrupt headers, and I plan to start my first Network Forensics module with Wireshark.
