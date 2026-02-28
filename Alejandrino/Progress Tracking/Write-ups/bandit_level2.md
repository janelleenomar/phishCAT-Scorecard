# OverTheWire: Bandit Level 2 → Level 3

## 1. Objective
The goal is to retrieve the password for Level 3, which is stored in a file called `spaces in this filename` located in the home directory.

---

## 2. Connection Details

- **Host:** `bandit.labs.overthewire.org`  
- **Port:** `2220`  
- **Username:** `bandit2`  
- **Password:** `2633GJPfgU6LtdEvgfWUiXP5yac29mFx`  

---

## 3. Technical Process (Terminal Evidence)

Filenames with spaces require special handling in the shell to prevent the terminal from treating each word as a separate argument.

```bash
# Connect to the game server
ssh bandit2@bandit.labs.overthewire.org -p 2220

# List files to find the one with spaces
bandit2@bandit:~$ ls
spaces in this filename

# Use double quotes to wrap the filename so the shell reads it as one unit
bandit2@bandit:~$ cat "spaces in this filename"
MNk8DnH3Vsilo41PRUeoDFPqfxLP1Sms

# Logout
bandit2@bandit:~$ exit
```
<img width="512" height="268" alt="bandit3" src="https://github.com/user-attachments/assets/4e481569-1957-49fe-83c4-1722c4c45a2d" />

---

## 4. Key Takeaways & Commands

- **Handling Spaces** — When a filename contains spaces, you must wrap it in quotes (`"file name"`) or escape each space with a backslash (`file\ name`).  
- **`cat`** — Used to print the contents of the file once the spacing issue is resolved.  

---

## 5. Password Discovered

**Level 3 Password:** `MNk8DnH3Vsilo41PRUeoDFPqfxLP1Sms`
