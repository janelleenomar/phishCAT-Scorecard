# 📊 Weekly Progress Summary

**Week:** 2 of 13  
**Dates:** February 15, 2026 to February 21, 2026

---

# Weekly Metrics

| Metric                  | Target | Actual | Status |
| ---------------------- | ------ | ------ | ------ |
| Training Hours         | 15–20  | 18.25  | ✓      |
| Challenges Solved      | 5–10   | 9      | ✓      |
| Live CTF Participated  | 1–2    | 1      | ✓      |
| CTF Challenges Solved  | 2–5    | 6      | ✓      |
| Writeups Created       | 3–5    | 4      | ✓      |
| New Techniques Learned | 2–3    | 5      | ✓      |

---

# Weekly Points Breakdown

| Source                | Points  |
| -------------------- | ------- |
| Training Hours       | 65      |
| Challenges Completed | 70      |
| Quality Bonuses      | 100     |
| Live CTF Performance | 10      |
| Writeups & Learning  | 0       |
| **Weekly Total**     | **245** |

---

# Time Distribution by Category
```
Cryptography: 12.25 hours [======= ] 67%
OSINT/Web (THM): 5.0 hours [=== ] 27%
Web Exploitation: 1.0 hours [= ] 6%
Binary Exploitation: 0 hours [ ] 0%
Reverse Engineering: 0 hours [ ] 0%
Forensics: 0 hours [ ] 0%
Linux Fundamentals: 0 hours [ ] 0%
```

---

# Skill Level Assessment (Self-Rated 1–10)

| Specialty                        | Last Week | This Week | Change |
| ------------------------------- | --------- | --------- | ------ |
| Primary #1 (Cryptography)       | 4         | 6         | +2     |
| Primary #2 (Cybersecurity/CTF)  | 3         | 4         | +1     |
| Secondary (Python Programming)  | 3         | 4         | +1     |

---

# Weekly Achievements

* [x] Finally cracked **Challenge 6** (Breaking repeating-key XOR) after days of struggle
* [x] Solved **Challenge 7** (AES-128 ECB decryption)
* [x] Solved **Challenge 8** (Detect AES in ECB mode)
* [x] Solved 3 challenges in TryHackMe "Love at First Breach" event
* [x] Solved 2 additional easy challenges in THM event
* [x] Created writeups for Challenges 6, 7, and 8
* [x] Mastered Hamming Distance calculation for keysize guessing
* [x] Learned AES block cipher implementation using PyCryptodome
* [x] Discovered ECB mode vulnerability (deterministic encryption = pattern leakage)
* [x] Maintained 13-day consistency streak
* [x] Proved resilience by pushing through "Challenge 6 Wall"

---

# Weekly Challenges & Lessons

**Biggest challenge this week**

The week started with the lingering "Challenge 6 Wall" - two days of staring at bit-counting logic that felt slightly off. Then transitioned into Challenge 7, where AES-128 ECB decryption brought a new wave of troubleshooting with library implementation and data formatting errors. Challenge 8 had me "half of half way there" before finally clicking.

---

**How you overcame it (or plan to)**

I learned to be flexible with my focus. On low-energy days (Day 11 with only 30 minutes), I just showed up to maintain the streak. When Cryptopals felt overwhelming, I pivoted to the THM event to keep momentum. For Challenge 7, I systematically debugged the Base64 decoding before passing data to the cipher. For Challenge 8, I had to redo the block slicing logic multiple times until the pattern became obvious.

---

**Most valuable lesson learned**

1. **Resilience pays off:** After days of no solves on Challenge 6, the breakthrough finally came. Sometimes the "learning" is just showing up.
2. **ECB is insecure because it's deterministic:** No Initialization Vector means identical plaintext blocks = identical ciphertext blocks. Pattern recognition can break it even without decryption.
3. **Context switching is a superpower:** Moving between THM events and Cryptopals kept motivation high during stall periods.
4. **Small sessions matter:** A 30-minute day (Day 11) kept the streak alive and the context fresh.

---

**Adjustment for next week**

Take a well-deserved **rest day** (as declared on Day 15!). Then prepare to tackle the next set of Cryptopals challenges with renewed energy. Consider starting to build a consolidated cheat sheet of all the Python functions and crypto concepts learned so far.

---

# Challenge Log

| Challenge                          | Category     | Difficulty | Status |
| ---------------------------------- | ------------ | ---------- | ------ |
| Cryptopals Challenge 6             | Cryptography | Hard       | ✓      |
| Cryptopals Challenge 7             | Cryptography | Medium     | ✓      |
| Cryptopals Challenge 8             | Cryptography | Medium     | ✓      |
| THM "Love at First Breach" (3x)    | OSINT/Web    | Easy       | ✓      |
| THM Event (2x additional)          | OSINT/Web    | Easy       | ✓      |

---

# Daily Breakdown

| Date       | Day | Hours | Challenges Solved | Notes |
| ---------- | --- | ----- | ----------------- | ----- |
| Feb 15     | 9   | 3.5   | 3 (THM)           | Rebuilding confidence after Challenge 6 wall |
| Feb 16     | 10  | 2.5   | 2 (THM)           | Continued THM momentum |
| Feb 17     | 11  | 0.5   | 0                 | Just showed up to maintain streak |
| Feb 18     | 12  | 3.5   | 1 (Challenge 6)   | **BREAKTHROUGH** - Finally cracked it! |
| Feb 19     | 13  | 1.75  | 0                 | Stuck on Challenge 7 debugging |
| Feb 20     | 14  | 2.0   | 1 (Challenge 7)   | AES decryption success |
| Feb 21     | 15  | 4.0   | 1 (Challenge 8)   | ECB detection + declared rest day |

---

# Notes

- **Consistency streak:** 13 days and counting (Feb 6 - Feb 21)
- **Breakthrough moment:** Day 12 - Finally solving Challenge 6 after days of frustration
- **Low point:** Day 11 - Only 30 minutes, no progress, but kept streak alive
- **High point:** Day 15 - Completing Challenge 8 and earning a well-deserved rest
- **Theme of the week:** Resilience through the "Challenge 6 Wall" and learning to pivot when stuck
