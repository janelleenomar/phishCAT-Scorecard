# OverTheWire: Bandit Level 13 → Level 14

## 1. Objective

The goal of this level is to retrieve the password for **Level 14**, which is stored in the file:

```
/etc/bandit_pass/bandit14
```

This file can only be accessed by the **bandit14** user. Instead of a password, Level 13 provides a **private SSH key** (`sshkey.private`) that allows authentication as the next user.

---

## 2. Connection Details

- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **Username:** `bandit13`
- **Password:** `FO5dwFsc0cbaIIh0h8j2eUks2vdTDwAn`

---

## 3. Technical Process (Terminal Evidence)

This level introduces **SSH key-based authentication**, a common method used for secure logins without passwords.

```bash
# 1. Connect to the Bandit server
ssh bandit13@bandit.labs.overthewire.org -p 2220

# 2. List files in the home directory
bandit13@bandit:~$ ls
sshkey.private

# 3. Restrict permissions on the private key
# SSH requires private keys to be readable only by the owner
bandit13@bandit:~$ chmod 600 sshkey.private

# 4. Use the private key to log in as bandit14
# -i specifies the identity (private key) file
bandit13@bandit:~$ ssh -i sshkey.private bandit14@localhost

# 5. Once logged in as bandit14, retrieve the password
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
MU4VWeTyJk8ROof1qqmcBPaLh7LDCpvS
```
<img width="974" height="374" alt="image" src="https://github.com/user-attachments/assets/0d6db738-bdbd-4bb5-b773-176437f21e25" />
<img width="725" height="979" alt="image" src="https://github.com/user-attachments/assets/d7b7a4d3-22fd-4afa-9f70-17d48e86db77" />
<img width="849" height="633" alt="image" src="https://github.com/user-attachments/assets/4487a26e-1213-4a51-a6f8-3d8fe87e051d" />

---

## 4. Key Takeaways & Commands

- **`ssh -i [keyfile]`**  
  The `-i` flag specifies a private key used for SSH authentication.

- **`chmod 600`**  
  Restricts the private key so that only the owner can read and write it. SSH refuses to use keys with insecure permissions.

- **SSH Key Authentication**  
  Instead of passwords, servers can authenticate users using asymmetric cryptography with **public and private key pairs**.

- **`localhost`**  
  Refers to the same machine. Since the private key belongs to `bandit14`, it allows switching users within the same system.

---

## 5. Reflection & Lessons Learned

- **Alternative Authentication Methods**  
  This level introduced SSH key authentication, which is widely used in real-world server administration and cloud infrastructure.

- **Importance of Private Key Security**  
  A private key functions like a password. If it is leaked or improperly protected, an attacker can gain unauthorized access.

- **File Permission Awareness**  
  Linux enforces strict security policies for SSH keys. Learning to manage permissions with `chmod` is essential for secure system operation.

- **Lateral Movement Concepts**  
  Using credentials from one user to access another account on the same system demonstrates a technique known as **lateral movement**, often used in penetration testing and security assessments.

---

## 6. Password Discovered

**Level 14 Password:**  
```
MU4VWeTyJk8ROof1qqmcBPaLh7LDCpvS
```
