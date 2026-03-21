# OverTheWire: Bandit Level 6 → Level 7

## 1. Objective

The goal is to find the password for the next level stored **somewhere on the server**. The file has the following properties:

- **Owned by user `bandit7`**
- **Owned by group `bandit6`**
- **33 bytes in size**

---

## 2. Connection Details

- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **Username:** `bandit6`
- **Password:** `HWasnPhtq9AVKe0dmk45nxy20cvUA6EG`

---

## 3. Technical Process (Terminal Evidence)

Since the file could be anywhere on the server, I searched starting from the root directory (`/`). I also redirected "Permission denied" errors to keep the output clean.

```bash
# Connect to the server
ssh bandit6@bandit.labs.overthewire.org -p 2220

# Search the entire file system for the specific owner, group, and size
# 2>/dev/null redirects error messages so only the match is shown
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password

# Read the contents of the discovered file
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
morbNTdkSW6jILUc0ymOdMaLnOlFVAaj

# Logout
bandit6@bandit:~$ exit
```

<img width="1600" height="794" alt="lvl6" src="https://github.com/user-attachments/assets/4c47e12c-b151-4b47-99ac-64505318f70f" />

---

## 4. Key Takeaways & Commands

- **`find /`** — Searching from the root directory covers the entire server, not just the home folder.
- **`-user` and `-group`** — These flags filter files based on Linux ownership permissions.
- **`2>/dev/null`** — Suppresses error messages. `2` represents the standard error stream (stderr); redirecting it to `/dev/null` discards it.
- **`-size 33c`** — Searches for a file that is exactly 33 bytes in size.

---

## 5. Reflection & Lessons Learned

- **System-Wide Searching** — Passwords are not always stored in obvious directories. Searching from `/` is powerful but generates many permission errors.
- **Filtering Noise** — Using `2>/dev/null` keeps output readable and prevents important results from being buried under error messages.
- **Ownership as a Filter** — Searching by file ownership is a realistic forensic technique for locating sensitive data.
- **Precision Matters** — Combining multiple filters (user, group, size) allows the `find` command to pinpoint a single file among thousands.

---

## 6. Password Discovered

**Level 7 Password:** `morbNTdkSW6jILUc0ymOdMaLnOlFVAaj`
