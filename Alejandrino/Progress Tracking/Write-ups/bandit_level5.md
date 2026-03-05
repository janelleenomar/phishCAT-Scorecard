# OverTheWire: Bandit Level 5 → Level 6

## 1. Objective

The goal is to find the password for Level 6 stored in a file located somewhere under the `inhere` directory. The target file must meet three specific criteria:

- **Human-readable**
- **Exactly 1033 bytes in size**
- **Not executable**

---

## 2. Connection Details

- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **Username:** `bandit5`
- **Password:** `4oQYVPkaZubhtS6dbZ6YpGvS7p9v78iz`

---

## 3. Technical Process (Terminal Evidence)

The `inhere` directory contains 20 subdirectories, each filled with multiple files. Searching manually would be inefficient. I used the `find` command to filter the file system for the exact properties provided.

```bash
# Connect to the Bandit server
ssh bandit5@bandit.labs.overthewire.org -p 2220

# Use 'find' with specific flags to isolate the file
# .             -> Look in current directory and subdirectories
# -type f       -> Filter for files only (ignore directories)
# -size 1033c   -> Filter for exactly 1033 bytes ('c' = bytes)
# ! -executable -> Filter for files that are NOT executable
bandit5@bandit:~$ find . -type f -size 1033c ! -executable
./inhere/maybehere07/.file2

# Read the file content to retrieve the password
bandit5@bandit:~$ cat ./inhere/maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUA6EG

# Close the session
bandit5@bandit:~$ exit
```

<img width="512" height="254" alt="unnamed" src="https://github.com/user-attachments/assets/9cf82ab1-e683-42b8-99c0-e8958df32387" />

---

## 4. Key Takeaways & Commands

- **`find`** — A powerful utility for searching through directory hierarchies.
- **Size Suffixes** — In the `find` command, `c` denotes bytes, while `k` denotes kilobytes.
- **Logical Operators** — The `!` (NOT) operator allows for negative filtering, useful for excluding unwanted file types.
- **Type Filtering** — Using `-type f` ensures only regular files are returned, preventing directories from appearing in results.

---

## 5. Reflection & Lessons Learned

- **Handling Complexity** — As challenges scale, manual exploration becomes inefficient. Tools like `find` are essential for managing large volumes of data.
- **Learning from Syntax Errors** — An incorrect flag (such as `-f`) results in an "unknown predicate" error. Linux requires precise syntax (e.g., `-type f`) to execute correctly.
- **The Importance of Metadata** — File metadata (size, permissions, ownership) can be just as important as filenames when investigating a system.
- **Hidden File Persistence** — Even with complex filters, the discovered file (`.file2`) was hidden, reinforcing that critical data is often intentionally obscured.

---

## 6. Password Discovered

**Level 6 Password:** `HWasnPhtq9AVKe0dmk45nxy20cvUA6EG`
