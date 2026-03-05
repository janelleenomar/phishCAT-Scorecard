# OverTheWire: Bandit Level 7 → Level 8

## 1. Objective

The goal is to retrieve the password for the next level, which is stored in a file named `data.txt`. The password is located specifically next to the word **"millionth"**.

---

## 2. Connection Details

- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **Username:** `bandit7`
- **Password:** `morbNTdkSW6jILUc0ymOdMaLnOlFVAaj`

---

## 3. Technical Process (Terminal Evidence)

The `data.txt` file is very large, making manual searching inefficient. I used the `grep` command to search for the specific keyword `"millionth"` to isolate the password.

```bash
# Connect to the server
ssh bandit7@bandit.labs.overthewire.org -p 2220

# List files to confirm data.txt exists
bandit7@bandit:~$ ls
data.txt

# Use grep to find the line containing the word "millionth"
bandit7@bandit:~$ grep millionth data.txt
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

# Logout
bandit7@bandit:~$ exit
```

<img width="1600" height="784" alt="lvl7" src="https://github.com/user-attachments/assets/b2711a0a-9d9c-43bc-9da3-c13c0a960d76" />

---

## 4. Key Takeaways & Commands

- **`grep`** — A command-line utility used for searching plain-text data for lines that match a keyword or regular expression.
- **Pattern Matching** — `grep` is essential when working with large files where using `cat` would overwhelm the terminal.

---

## 5. Reflection & Lessons Learned

- **Isolating Data** — Finding information is not just about locating a file, but extracting specific content from within it.
- **Tools for Scale** — Instead of manually scrolling through a massive file, `grep` provides instant, precise results.
- **Contextual Clues** — The objective provided an anchor word ("millionth"). Identifying anchor terms is a critical skill when analyzing logs or large datasets.

---

## 6. Password Discovered

**Level 8 Password:** `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`
