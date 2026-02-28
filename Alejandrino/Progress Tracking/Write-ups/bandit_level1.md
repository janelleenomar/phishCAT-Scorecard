# OverTheWire: Bandit Level 1 → Level 2

## 1. Objective
The goal is to find the password for the next level, which is stored in a file called `-` located in the home directory.

---

## 2. Connection Details

- **Host:** `bandit.labs.overthewire.org`  
- **Port:** `2220`  
- **Username:** `bandit1`  
- **Password:** `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`  

---

## 3. Technical Process (Terminal Evidence)

---<img width="216" height="512" alt="bandit1" src="https://github.com/user-attachments/assets/f1e862b7-ec49-489c-a858-5bf33b5d33a7" />

---

## 4. Key Takeaways & Commands

- **Filenames with Dashes** — In Linux, many commands treat `-` as a special character (representing `stdin`). To force the terminal to treat it as a filename, you must precede it with a path like `./`.  
- **`./`** — Represents the "current directory." It tells the shell exactly where to look for the file.  
- **Relative vs. Absolute Paths** — Using `./-` is a relative path. An absolute path for this file would be `/home/bandit1/-`.  

---

## 5. Password Discovered

**Level 2 Password:** `2634ebS9A06EBn9p4BNELrg9sgY9tkS8`
