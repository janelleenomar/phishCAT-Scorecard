# 📝 Challenge Write-up: Binary Search

| Attribute | Details |
|---|---|
| **Event** | picoCTF 2024 |
| **Category** | General Skills |
| **Difficulty** | Easy |

---

## 1. The Challenge Scenario

The objective of this challenge is to find a hidden number between **1 and 1000** chosen by the server. However, there is a strict constraint: you only have **10 guesses**.

This challenge simulates real-world cybersecurity scenarios where analysts must search through massive datasets (logs, forensics, or vulnerability reports). Using a **Binary Search** algorithm allows us to find the correct entry in **O(log n)** time, making it mathematically impossible to fail if the algorithm is followed correctly.

---

## 2. The Step-by-Step Solution

### Step 1: Establishing Connection

I connected to the picoCTF instance via SSH using the provided credentials.

**Command:**

```bash
ssh -p 58530 ctf-player@atlas.picoctf.net
```

**Password:**

```
f3b61b38
```

Once connected, the script `guessing_game.sh` starts automatically.

---

### Step 2: Implementing the Algorithm

To ensure success within 10 guesses (**2^10 = 1024**), I followed the Binary Search pattern: always guessing the **median** of the current possible range.

1. **Lower Bound:** 1  
2. **Upper Bound:** 1000  
3. **Calculation:**

```
Guess = floor((Lower + Upper) / 2)
```

---

### Step 3: The Search Process (Example Execution)

**Initial Guess:** `500`  
Response: **Higher**  
New Range: `501 – 1000`

**Second Guess:** `750`  
Response: **Lower**  
New Range: `501 – 749`

**Third Guess:** `625`  
Response: **Higher**  
New Range: `626 – 749`

**Fourth Guess:** `687`  
Response: **Higher**  
New Range: `688 – 749`

I continued this **halving process** until the server confirmed the correct number.

---

### Step 4: Capturing the Flag

Once the correct number was guessed, the server executed a command that revealed the flag stored in the system environment.

---

## 3. The Findings

The Binary Search algorithm reduced **1,000 possible values to a single correct answer in fewer than 10 guesses**.

**Target Number Identified:** *(Varies per instance)*

**Flag:**

```
picoCTF{g00d_gu355_XXXXXXXX}
```
<img width="975" height="1094" alt="image" src="https://github.com/user-attachments/assets/7f85bd09-5b4a-4399-adc1-413006bd286b" />

---

## 4. Conclusion

This challenge demonstrates the efficiency of **logarithmic search algorithms**. In cybersecurity, analysts frequently deal with large datasets where linear searching would be inefficient.

Binary Search significantly reduces the number of required operations by repeatedly dividing the search space in half.

### Key Takeaways

- **Efficiency:** Binary Search reduces a search space of 1,000 values to a maximum of **10 guesses**.
- **Precision:** For sorted data (e.g., timestamps in logs), jumping directly to the midpoint is far more efficient than scanning sequentially.
- **Shell Interaction:** Practicing interaction with remote scripts builds familiarity with **SSH environments and command-line workflows**.
