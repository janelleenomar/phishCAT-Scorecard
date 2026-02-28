# OverTheWire: Bandit Level 3 → Level 4

## 1. Objective
The objective of this level is to retrieve the password for Level 4, which is hidden in a file within the `inhere` directory located in the home folder.

---

## 2. Connection Details

- **Host:** `bandit.labs.overthewire.org`  
- **Port:** `2220`  
- **Username:** `bandit3`  
- **Password:** `MNk8DnH3Vsilo41PRUeoDFPqfxLP1Sms`  

---

## 3. Technical Process (Terminal Evidence)

To solve this level, I had to navigate to a specific directory and reveal a hidden file that does not appear with a standard directory listing.

```bash
# Connect to the server as bandit3
ssh bandit3@bandit.labs.overthewire.org -p 2220

# Change directory into 'inhere'
bandit3@bandit:~$ cd inhere

# A standard 'ls' command returns no output, appearing empty
bandit3@bandit:~/inhere$ ls

# Using 'ls -a' reveals all files, including hidden ones starting with a dot
bandit3@bandit:~/inhere$ ls -a
.  ..  ...Hiding-From-You

# Read the content of the hidden file discovered
bandit3@bandit:~/inhere$ cat ...Hiding-From-You
2WmrDFRmJiQ3IPxneAaMGhap0pFhF3NJ

# Exit the session
bandit3@bandit:~/inhere$ exit
```
<img width="512" height="255" alt="image" src="https://github.com/user-attachments/assets/820fc13d-186b-4251-b940-2f6dfb29958c" />

---

## 4. Key Takeaways & Commands

- **`cd`** — Used to change the current working directory to `inhere`.  
- **`ls -a`** — Lists *all* files, including hidden ones (those beginning with a `.`) that are normally not displayed.  
- **`find`** — An alternative command that can be used to search for files within the current directory tree.  
- **Hidden Files** — In Linux, files starting with a dot (`.`) are considered hidden. The file `...Hiding-From-You` used multiple dots to further obscure itself.  

---

## 5. Password Discovered

**Level 4 Password:** `2WmrDFRmJiQ3IPxneAaMGhap0pFhF3NJ`
