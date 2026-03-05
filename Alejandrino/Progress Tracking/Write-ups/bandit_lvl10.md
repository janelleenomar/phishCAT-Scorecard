# OverTheWire: Bandit Level 10 → Level 11

## 1. Objective

The objective of this level is to retrieve the password for Level 11, which is stored in a file named `data.txt`. The file contains **Base64 encoded data**, which must be decoded to reveal the password.

---

## 2. Connection Details

- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **Username:** `bandit10`
- **Password:** `FGUW5illVJrxX9kMYMmlN4MgbpfMiqey`

---

## 3. Technical Process (Terminal Evidence)

The file `data.txt` contains a string of characters that do not form a standard password. Using the `base64` utility, I decoded the content to obtain the plain-text password.

```bash
# Connect to the server as bandit10
ssh bandit10@bandit.labs.overthewire.org -p 2220

# List the file details to confirm its presence
bandit10@bandit:~$ ls -l data.txt
-rw-r----- 1 bandit11 bandit10 69 Oct 14 09:26 data.txt

# View the raw encoded content
bandit10@bandit:~$ cat data.txt
VGhliHBhc3N3b3JkIGlzIGR1UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmp3cVJyCg==

# Decode the Base64 data to reveal the password
bandit10@bandit:~$ base64 -d data.txt
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

# Logout
bandit10@bandit:~$ exit
```

<img width="975" height="479" alt="image" src="https://github.com/user-attachments/assets/ede0c5b5-62be-46e6-94f8-527974414671" />

---

## 4. Key Takeaways & Commands

- **`base64`** — A command-line utility used to encode or decode data using the Base64 format.
- **`-d` flag** — Stands for **decode**, converting the Base64 string back into readable ASCII text.
- **Base64 Encoding** — A method used to represent binary data in ASCII text format. Commonly used in emails, APIs, and web data transmission.

---

## 5. Reflection & Lessons Learned

- **Recognizing Encodings** — Base64 strings are often recognizable because they typically end with one or two `=` padding characters.
- **Decoding vs. Cracking** — Base64 is **not encryption**, but an encoding scheme. No key is required—only the proper decoding tool.
- **Direct File Processing** — The `base64` command can accept a filename directly, making it more efficient than piping from `cat`.

---

## 6. Password Discovered

**Level 11 Password:** `dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr`
