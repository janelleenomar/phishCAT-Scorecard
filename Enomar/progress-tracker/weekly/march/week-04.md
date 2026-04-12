# Weekly Progress Summary

**Week:** 8 of 13 (March Week 4) | **Dates:** March 22, 2026 to March 28, 2026

## Weekly Metrics

| Metric                 | Target | Actual | Status |
| ---------------------- | ------ | ------ | ------ |
| Training Hours         | 15-20  | 7      | ☐ ✗    |
| Challenges Solved      | 15-25  | 4      | ☐ ✗    |
| Live CTF Participated  | 1-2    | 1      | ☐ ✓    |
| CTF Challenges Solved  | 2-5    | 2      | ☐ ✓    |
| Writeups Created       | 3-5    | 3      | ☐ ✓    |
| New Techniques Learned | 2-3    | 3      | ☐ ✓    |

## Weekly Points Breakdown

| Source               | Points  |
| -------------------- | ------- |
| Training Hours       | 30      |
| Challenges Completed | 30      |
| Quality Bonuses      | 100     |
| Live CTF Performance | 100     |
| Writeups & Learning  | 0       |
| **Weekly Total** | **260** |

## Category Distribution (Hours This Week)

```text
Web Exploitation:     0 hours [        ] 0%
Binary Exploitation:  0 hours [        ] 0%
Cryptography:         0 hours [        ] 0%
Reverse Engineering:  0 hours [        ] 0%
Forensics:            0 hours [        ] 0%
OSINT:                6 hours [========] 85%
Misc / Sanity Check:  1 hour  [=       ] 15%
```

## Skill Level Assessment (Self-Rated 1-10)

| Specialty           | Last Week | This Week | Change |
| ------------------- | --------- | --------- | ------ |
| Primary #1 (OSINT)  | 4         | 6         | +2     |
| Primary #2 (AI Sec) | 3         | 3         | 0      |
| Secondary (Misc)    | 0         | 1         | +1     |

## Weekly Achievements

- [x] Solved first challenge in new category (Misc/IRC)
- [x] Completed difficult challenge independently (TexSAW OSINT)
- [ ] Helped teammate solve challenge
- [x] Found new technique/exploit (Google Lens to context pivoting)
- [x] Improved solve time by 20%+
- [x] Other: Successfully established connectivity to competition infrastructure via Irssi.

## Weekly Challenges & Lessons

**Biggest challenge this week:**
The shift from static lab environments to a live CTF (TexSAW 2026). Specifically, the "YOU SNOZE YOU LOZE" challenge provided a low-light, blurry image that made manual identification impossible. Additionally, the sheer density of the 102-page CFPB financial report required high mental stamina to avoid "keyword fatigue."

**How you overcame it (or plan to):**
I moved away from "staring at the problem" and started "pivoting through the problem." Using Google Lens to identify the racing event allowed me to move from a visual dead-end to a text-based investigation. For the large PDF documents, I mastered the use of multi-layered Google Dorks (`site:`, `filetype:`, and `intext:`) to let the search engine do the filtering for me before I even opened the file.

**Most valuable lesson learned:**
"Security by obscurity" fails every time. Even if a government document isn't linked on a homepage, it is discoverable if it's on the server. On the technical side, I learned that OSINT is about building a chain: Image -> Context (Lens) -> Data (Search Queries) -> Flag.

**Adjustment for next week:**
I need to increase my training volume to hit the 15-20 hour target. Since OSINT skills are sharpening, I plan to introduce a secondary technical focus like Cryptography or Network Forensics (Wireshark) to ensure I don't become a "one-tool" investigator.