# 📊 Individual Progress Scorecard

## Daily Training Log

**Date:** March 10, 2026 | **Training Day:** 33/90 (3-month plan)

---

## 1. Time Investment

* [x] Training time today: **2 hours**
* [x] Goal met? **Yes**
* [x] Consistency streak: **1 day**

**Points:**

* 2+ hours = **10 points** (Achieved)
* 1-2 hours = 5 points
* <1 hour = 2 points
* Missed day = 0 points (streak resets)

---

## 2. Challenge Completion

| Difficulty      | Challenges Solved | Points Earned |
| --------------- | ----------------- | ------------- |
| Easy            | 2 × 5 pts         | 10            |
| Medium          | 0 × 15 pts        | 0             |
| Hard            | 0 × 30 pts        | 0             |
| Expert          | 0 × 50 pts        | 0             |
| **Daily Total** |                   | **10** |

*Challenges included: SQL Injection Vulnerability Allowing Login Bypass, SQL Injection in WHERE Clause Allowing Retrieval of Hidden Data.*

---

## 3. Quality Indicators

* [x] Created writeup for at least 1 challenge (+10 pts)
* [ ] Reviewed 3+ writeups from others (+5 pts)
* [x] Learned new technique/tool (+10 pts)
* [ ] Updated cheat sheet (+5 pts)
* [ ] Practiced timed challenge (+5 pts)

**Quality Points Total:** **20**

---

## 4. Category Focus Today

Which categories did you practice?

* [x] Web Exploitation
* [ ] Binary Exploitation / Pwn
* [ ] Cryptography
* [ ] Reverse Engineering
* [ ] Forensics
* [ ] OSINT
* [ ] Other: 

**Primary Specialty (SQL Injection):** 120 minutes

**Secondary Specialty (Burp Suite Fundamentals):** 30 minutes

---

## 5. Reflection (Qualitative)

**What went well today?**
I successfully completed two foundational SQL Injection labs on PortSwigger Academy. I mastered the use of the `' OR 1=1 --` payload to bypass authentication and learned how to manipulate `WHERE` clauses to reveal hidden products by commenting out the rest of the query.

**What challenged you?**
Initially, I struggled with the syntax for commenting out the backend query. I had to learn the difference between `--` (with a space) for PostgreSQL/MySQL and `#` for other databases.

**Key learning:**
SQL injection occurs when user input is concatenated directly into a query string instead of being properly parameterized. Even a simple comment character can completely change the logic of the backend database.

**Tomorrow's focus:**
Advance to **UNION-based SQL Injection** to learn how to extract actual data from other tables in the database.
