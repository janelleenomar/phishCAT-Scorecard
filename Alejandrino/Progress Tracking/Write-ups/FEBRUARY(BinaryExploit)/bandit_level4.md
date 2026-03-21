# OverTheWire: Bandit Level 4 → Level 5

## 1. Objective
The goal is to find the password for the next level stored in the only human-readable file within the `inhere` directory.

---

## 2. Connection Details

- **Host:** `bandit.labs.overthewire.org`  
- **Port:** `2220`  
- **Username:** `bandit4`  
- **Password:** `2WmrDFRmJiQ3IPxneAaMGhap0pFhF3NJ`  

---

## 3. Technical Process (Terminal Evidence)

The directory contains multiple files prefixed with a dash (e.g., `-file01`), which are normally interpreted as command flags.

```bash
# Move into the target directory
bandit4@bandit:~$ cd inhere

# Use 'file' with a wildcard and path to identify the data type of all files
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: OpenPGP Public Key
./-file02: OpenPGP Public Key
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data

# Read the file identified as 'ASCII text' using '--' to signal the end of options
bandit4@bandit:~/inhere$ cat -- -file07
4oQYVPkaZubhtS6dbZ6YpGvS7p9v78iz

# Exit
bandit4@bandit:~$ exit
```

---

## 4. Key Takeaways & Commands

- **`file`** — Determines file types by examining their internal data structure (magic bytes).  
- **`--` (Double Dash)** — Signals the end of command options, allowing filenames beginning with `-` to be interpreted correctly.  
- **`*` (Wildcard)** — Used to apply a command to multiple files at once.  

<img width="512" height="252" alt="image" src="https://github.com/user-attachments/assets/2a1a583e-88c9-4b29-b6d8-a36b3b36aa36" />

---

## 5. Reflection & Lessons Learned

This level reinforced important Linux shell concepts:

- **Filenames Are Just Labels** — A filename can resemble a command flag (e.g., `-file07`), which can break standard commands. Using `./` or `--` clarifies intent to the shell.  
- **Identifying Human-Readable Content** — Instead of blindly using `cat` on every file, the `file` command provides a safer and more professional method to identify readable text.  
- **Efficiency with Wildcards** — Using `file ./*` is faster and reduces errors compared to checking each file individually.  
- **Precision in Syntax** — Linux commands require exact syntax. Even small mistakes can result in usage errors, reinforcing the importance of attention to detail.  

---

## 6. Password Discovered

**Level 5 Password:** `4oQYVPkaZubhtS6dbZ6YpGvS7p9v78iz`
