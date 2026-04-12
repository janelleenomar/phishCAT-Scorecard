# Weekly Progress Summary

**Week:** 7 of 13 (March Week 3) | **Dates:** March 15, 2026 to March 21, 2026

## Weekly Metrics

| Metric                 | Target | Actual | Status |
| ---------------------- | ------ | ------ | ------ |
| Training Hours         | 15-20  | 8      | ☐ ✗    |
| Challenges Solved      | 15-25  | 7      | ☐ ✗    |
| Live CTF Participated  | 1-2    | 0      | ☐ ✗    |
| CTF Challenges Solved  | 2-5    | 0      | ☐ ✗    |
| Writeups Created       | 3-5    | 7      | ☐ ✓    |
| New Techniques Learned | 2-3    | 4      | ☐ ✓    |

*(Note: Training hours were highly concentrated on advanced Red Teaming tasks).*

## Weekly Points Breakdown

| Source               | Points  |
| -------------------- | ------- |
| Training Hours       | 30      |
| Challenges Completed | 115     |
| Quality Bonuses      | 90      |
| Live CTF Performance | 0       |
| Writeups & Learning  | 0       |
| **Weekly Total** | **235** |

## Category Distribution (Hours This Week)

```text
Web Exploitation:                 0 hours [        ] 0%
Binary Exploitation:              0 hours [        ] 0%
Cryptography:                     0 hours [        ] 0%
Reverse Engineering:              0 hours [        ] 0%
Forensics:                        0 hours [        ] 0%
OSINT:                            0 hours [        ] 0%
Prompt Injection / AI Security:   8 hours [========] 100%
```

## Skill Level Assessment (Self-Rated 1-10)

| Specialty  | Last Week | This Week | Change |
| ---------- | --------- | --------- | ------ |
| Primary #1 (AI Security) | 0         | 3         | +3     |
| Primary #2 (OSINT)       | 4         | 4         | 0      |
| Secondary                | 0         | 0         | 0      |

## Weekly Achievements

- [x] Solved first challenge in new category
- [x] Completed difficult challenge independently
- [ ] Helped teammate solve challenge
- [x] Found new technique/exploit
- [ ] Improved solve time by 20%+
- [x] Other: Successfully cracked dynamic masking filters using purely deductive OSINT techniques (Semantic Leaking).

## Weekly Challenges & Lessons

**Biggest challenge this week:**
Shifting my mindset from traditional technical hacking to linguistic manipulation and social engineering. Dealing with advanced exact-string output filters, secondary GPT intent-evaluators, and dynamic word masking on the Lakera Gandalf platform felt like hitting a brick wall initially because standard bypasses instantly triggered alarms.

**How you overcame it (or plan to):**
I adapted my attack strategies as the AI's defenses escalated. Instead of direct commands, I used dictionary definitions, structural obfuscation (acrostic poems), token masking (hyphens), conversational social engineering, and finally, semantic deduction to outsmart the scanning mechanisms themselves.

**Most valuable lesson learned:**
Basic blocklist security and Data Loss Prevention (DLP) are fundamentally flawed in Large Language Models. An AI's inherent drive to complete structural tasks will often override its security guardrails. Furthermore, "Semantic Leaking"—where an AI replaces a secret word with a contextually similar fake word—gives an attacker the exact breadcrumbs needed to deduce the protected data without ever bypassing the output filter.

**Adjustment for next week:**
I plan to apply these advanced prompt injection methodologies (like roleplay framing, context switching, and payload wrapping) to other AI Red Teaming platforms, or tackle the final boss level of Gandalf (Level 8) before transitioning back to OSINT/Forensics.