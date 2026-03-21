# OverTheWire: Bandit Level 9 → Level 10

## 1. Objective

The goal is to retrieve the password for Level 10, which is stored in the file `data.txt`. The password is one of the few **human-readable strings** in the file and is preceded by several `=` characters.

---

## 2. Connection Details

- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **Username:** `bandit9`
- **Password:** `4CKmh1Jl91bUIZZPXDqGanal4xvAg0JM`

---

## 3. Technical Process (Terminal Evidence)

The file `data.txt` contains binary data, making it difficult to read using standard commands like `cat`. I used the `strings` command to extract human-readable text and filtered for the `=` character.

```bash
# Connect to the Bandit server
ssh bandit9@bandit.labs.overthewire.org -p 2220

# Use 'strings' to find readable text and 'grep' to filter for the '=' prefix
bandit9@bandit:~$ strings data.txt | grep "="
========== the
9=H`
[!#=Z
========== password
xWf=
f\Z'========== is
ei{\#
/1s
nS=F
M=Sl
=LGT
y =1
========== FGUW5illVJrxX9kMYMmlN4MgbpfMiqey

# Optional: Clean up the output using 'tr' to remove the '=' characters
bandit9@bandit:~$ strings data.txt | grep "=" | tr -d '='

# Logout
bandit9@bandit:~$ exit
```

<img width="624" height="308" alt="lvl9" src="https://github.com/user-attachments/assets/483f622d-ed53-4da4-b6e8-a56d255ac526" />

---

## 4. Key Takeaways & Commands

- **`strings`** — Extracts printable character sequences from binary files.
- **`grep "="`** — Filters output to show only lines containing the `=` character.
- **`tr -d '='`** — Deletes the `=` characters to make the password easier to copy.
- **Command Piping (`|`)** — Allows multiple commands to process data sequentially.

---

## 5. Reflection & Lessons Learned

- **Binary vs ASCII** — Not all `.txt` files contain plain text. Binary files can display unreadable symbols when viewed with `cat`.
- **Pattern Recognition** — Searching for repeated characters (`====`) helps isolate important information within noisy data.
- **Command Chaining** — Combining `strings`, `grep`, and `tr` demonstrates how Linux tools can work together to solve complex problems efficiently.

---

## 6. Password Discovered

**Level 10 Password:** `FGUW5illVJrxX9kMYMmlN4MgbpfMiqey`
