# OverTheWire: Bandit Level 8 → Level 9

## 1. Objective

The goal is to retrieve the password for Level 9, which is stored in the file `data.txt`. The password is the **only line of text that occurs only once** in the entire file.

---

## 2. Connection Details

- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **Username:** `bandit8`
- **Password:** `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`

---

## 3. Technical Process (Terminal Evidence)

To find a unique line, the data must first be sorted so that duplicate lines are grouped together. Then, the `uniq` command can filter out anything that repeats.

```bash
# Connect to the server
ssh bandit8@bandit.labs.overthewire.org -p 2220

# Sort the file and pipe it into uniq with the -u (unique) flag
# This suppresses any lines that appear more than once
bandit8@bandit:~$ sort data.txt | uniq -u
4CKmh1Jl91bUIZZPXDqGanal4xvAg0JM

# Logout
bandit8@bandit:~$ exit
```

<img width="975" height="512" alt="image" src="https://github.com/user-attachments/assets/f09749b8-5654-471f-8f94-82d6466385cb" />

---

## 4. Key Takeaways & Commands

- **`sort`** — Arranges the lines of a text file in alphanumeric order. This step is required for `uniq` to work correctly.
- **`uniq -u`** — Normally removes adjacent duplicate lines, but the `-u` flag tells it to print **only lines that appear once**.
- **`|` (Pipe)** — Sends the output of one command (`sort`) as the input to another command (`uniq`).

---

## 5. Reflection & Lessons Learned

- **Piping for Power** — This level demonstrates the Linux philosophy of combining small tools (`sort` and `uniq`) to solve larger problems.
- **Order of Operations** — `uniq` only detects duplicates if they are adjacent, which is why `sort` must be used first.
- **Syntax Troubleshooting** — Small mistakes in command flags (e.g., typing `uniq q` instead of `uniq -u`) produce errors, reinforcing the need for precision in command syntax.
- **Data Analysis in Security** — This technique can be applied to log analysis, such as identifying a single unusual IP address among thousands of repeated entries.

---

## 6. Password Discovered

**Level 9 Password:** `4CKmh1Jl91bUIZZPXDqGanal4xvAg0JM`
