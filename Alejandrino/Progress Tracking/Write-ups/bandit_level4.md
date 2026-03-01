# OverTheWire: Bandit Level 5 → Level 6

## 1. Objective
The goal is to find the password for the next level stored in a file somewhere under the `inhere` directory. The file has three specific properties:

- Human-readable  
- 1033 bytes in size  
- Not executable  

---

## 2. Connection Details

- **Host:** `bandit.labs.overthewire.org`  
- **Port:** `2220`  
- **Username:** `bandit5`  
- **Password:** `4oQYVPkaZubhtS6dbZ6YpGvS7p9v78iz`  

---

## 3. Technical Process (Terminal Evidence)

The `inhere` directory contains many nested folders, making a manual search difficult. I used the `find` command to filter for the exact file properties.

```bash
# Connect to the server
ssh bandit5@bandit.labs.overthewire.org -p 2220

# Use 'find' to locate the file based on the given criteria:
# .             -> Search starting from the current directory
# -type f       -> Look specifically for files (not directories)
# -size 1033c   -> Look for a file exactly 1033 bytes ('c' stands for bytes)
# ! -executable -> Look for files that are NOT executable
bandit5@bandit:~$ find . -type f -size 1033c ! -executable
./inhere/maybehere07/.file2

# Read the contents of the discovered file
bandit5@bandit:~$ cat ./inhere/maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUA6EG

# Logout
bandit5@bandit:~$ exit
```

<img width="512" height="254" alt="image" src="https://github.com/user-attachments/assets/48a1a59c-bb5c-442e-b0eb-7256d049c2ae" />

---

## 4. Key Takeaways & Commands

- **`find`** — A highly versatile tool for searching the file system using specific filters.  
- **`-size 1033c`** — The `c` suffix specifies bytes. Without it, `find` may search by block size instead.  
- **`! -executable`** — The exclamation mark acts as a logical NOT operator, excluding files with execution permissions.  
- **`-type f`** — Ensures that only regular files are returned, ignoring directories.  

---

## 5. Password Discovered

**Level 6 Password:** `HWasnPhtq9AVKe0dmk45nxy20cvUA6EG`
