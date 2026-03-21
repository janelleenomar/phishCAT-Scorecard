## Bandit Level 11 $\rightarrow$ Level 12 Write-up

### **1. Objective**

The goal of this level is to retrieve the password for Level 12, which is stored in a file called `data.txt`. The file's content has been obscured using a **ROT13 cipher**, where every lowercase (a-z) and uppercase (A-Z) letter has been rotated by 13 positions.

---

### **2. Connection Details**

* **Host:** `bandit.labs.overthewire.org`
* **Port:** `2220`
* **Username:** `bandit11`
* **Password:** `dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr`

---

### **3. Technical Process (Terminal Evidence)**

Because the file contains a simple substitution cipher, standard reading with `cat` results in unreadable text. I used the `tr` (translate) command to shift the characters back to their original positions.

```bash
# Connect to the game server
ssh bandit11@bandit.labs.overthewire.org -p 2220

# List files to confirm data.txt is present
bandit11@bandit:~$ ls
data.txt

# View the encrypted ROT13 content
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf 7x16WNeHIi5YkIhWsffIQoognUTyj9Q4

# Use the 'tr' command to rotate the alphabet by 13 places
# 'A-Za-z' is the input set, 'N-ZA-Mn-za-m' is the 13-place shifted output set
bandit11@bandit:~$ tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
The password is 7x16WNeHIi5YkIhWsffIQoognUTyj9Q4

# Logout
bandit11@bandit:~$ exit

```

<img width="975" height="444" alt="image" src="https://github.com/user-attachments/assets/3c6a653c-d3ec-46bd-9d2f-32069206f2f8" />

---

### **4. Key Takeaways & Commands**

* **`tr` (Translate)**: A utility used to translate or delete characters from standard input.
* **ROT13**: A specific case of the Caesar cipher. Since there are 26 letters in the English alphabet, rotating by 13 positions twice returns the text to its original state.
* **Input Redirection (`<`)**: Used to feed the contents of `data.txt` into the `tr` command.

---

### **5. Reflection & Lessons Learned**

* **Identifying ROT13**: I learned that if a string looks like scrambled English (e.g., "Gur cnffjbeq" instead of "The password"), ROT13 is a likely culprit.
* **The Power of `tr**`: This level showed me how to map ranges of characters efficiently. By defining the sets `'A-Za-z'` and `'N-ZA-Mn-za-m'`, I can perform complex character swaps in a single line of code.
* **Decoding vs. Encryption**: Similar to Base64, ROT13 is a form of encoding/obfuscation, not secure encryption. It provides zero security against anyone who knows the rotation pattern.
* **Character Set Precision**: I learned that I must include both uppercase and lowercase ranges in the `tr` command to ensure the entire password decodes correctly, as the password contains mixed-case characters.

---

### **6. Password Discovered**

**Level 12 Password:** `7x16WNeHIi5YkIhWsffIQoognUTyj9Q4`
