# Weekly Progress Summary

**Week:** 4 of 13 | **Dates:** February 22, 2026 to March 1, 2026

## Weekly Metrics

| Metric                 | Target | Actual | Status |
| ---------------------- | ------ | ------ | ------ |
| Training Hours         | 15-20  | 3.0    | ☐ ✗    |
| Challenges Solved      | 15-25  | 3      | ☐ ✗    |
| Live CTF Participated  | 1-2    | 0      | ☐ ✗    |
| CTF Challenges Solved  | 2-5    | 0      | ☐ ✗    |
| Writeups Created       | 3-5    | 3      | ☐ ✓    |
| New Techniques Learned | 2-3    | 2      | ☐ ✓    |

## Weekly Points Breakdown

| Source               | Points |
| -------------------- | ------ |
| Training Hours       | 10     |
| Challenges Completed | 35     |
| Quality Bonuses      | 25     |
| Live CTF Performance | 0      |
| Writeups & Learning  | 0      |
| **Weekly Total** | **70** |

## Category Distribution (Hours This Week)

    Web Exploitation:     0.0 hours [        ] 0%
    Binary Exploitation:  0.0 hours [        ] 0%
    Cryptography:         0.0 hours [        ] 0%
    Reverse Engineering:  0.0 hours [        ] 0%
    Forensics:            3.0 hours [========] 100%
    OSINT:                0.0 hours [        ] 0%

## Skill Level Assessment (Self-Rated 1-10)

| Specialty                 | Last Week | This Week | Change |
| ------------------------- | --------- | --------- | ------ |
| Primary #1 (Forensics)    | 4         | 5         | +1     |
| Primary #2 (Web Exploit)  | 2         | 2         | 0      |
| Secondary                 | 0         | 0         | 0      |

## Weekly Achievements

- [ ] Solved first challenge in new category
- [x] Completed difficult challenge independently
- [ ] Helped teammate solve challenge
- [x] Found new technique/exploit
- [ ] Improved solve time by 20%+
- [x] Other: Maintained technical progress by solving three challenges efficiently before shifting entirely to rest and university study mode for the week.

## Weekly Challenges & Lessons

**Biggest challenge this week:**
Balancing time and technical limitations. On the technical side, I hit a massive performance wall when Notepad crashed trying to read a large binary image file during one of the forensics challenges. On the personal side, managing my time became the biggest hurdle. With prelim exams fast approaching for demanding subjects like Net 2, SQL Database Management, and GE Ethics, I had to deliberately step back from CTF training to prioritize my academic workload and take necessary rest days.

**How you overcame it (or plan to):**
To bypass the technical crash, I abandoned Windows text editors for large files and immediately pivoted to my native Kali Linux environment, utilizing `exiftool` to smoothly extract the payload. For the scheduling conflict, I accepted the need to throttle my training hours this week. I condensed my CTF practice into a single highly productive 2-hour session, allowing me to dedicate the rest of the week to studying and recovering.

**Most valuable lesson learned:**
Basic text editors simply cannot handle large binary files; utilizing dedicated CLI forensics tools like `exiftool` on Kali Linux is a requirement for stability. I also learned that packet captures (.pcap) often contain easily readable plain text, and digital redactions in PDFs are frequently just superficial visual layers that don't destroy the underlying data. Finally, integrating an offline tool like DevToys for Base64 decoding significantly sped up my workflow.

**Adjustment for next week:**
My primary adjustment will be passing my preliminary exams. Once my academic schedule clears up, I plan to dive into proper packet analysis. While opening a PCAP in Notepad worked for an unencrypted challenge this week, I know I need to master Wireshark and basic packet filtering for more complex network forensics moving forward.
