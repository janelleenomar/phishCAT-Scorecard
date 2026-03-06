# OverTheWire Bandit – Quick Cheat Sheet (Levels 0–14)

This cheat sheet summarizes the key concepts and commands used in the **OverTheWire Bandit Wargame** for Levels **0 → 14**.

---

# Level 0 → Level 1
## Concept
Basic SSH login and reading a file.

## Commands
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
ls
cat readme
```

## Key Idea
Use **SSH** to connect to a remote machine and read a file using `cat`.

---

# Level 1 → Level 2
## Concept
Handling filenames that start with `-`.

## Commands
```bash
ls
cat ./-
```

## Key Idea
The dash `-` is interpreted as **stdin**. Use `./` to reference it as a file.

---

# Level 2 → Level 3
## Concept
Handling filenames with **spaces**.

## Commands
```bash
ls
cat "spaces in this filename"
```

Alternative:
```bash
cat spaces\ in\ this\ filename
```

## Key Idea
Wrap filenames in **quotes** or escape spaces with `\`.

---

# Level 3 → Level 4
## Concept
Finding **hidden files**.

## Commands
```bash
cd inhere
ls -a
cat ...Hiding-From-You
```

## Key Idea
Files beginning with `.` are **hidden**. Use `ls -a`.

---

# Level 4 → Level 5
## Concept
Finding the **only human-readable file**.

## Commands
```bash
cd inhere
file ./*
cat -- -file07
```

## Key Idea
Use `file` to detect readable text files.

`--` tells commands **stop parsing options**.

---

# Level 5 → Level 6
## Concept
Searching files using multiple conditions.

## Commands
```bash
find . -type f -size 1033c ! -executable
cat ./inhere/maybehere07/.file2
```

## Key Idea
Use `find` filters:

- `-type f` → files
- `-size` → specific size
- `!` → NOT operator

---

# Level 6 → Level 7
## Concept
Finding files across the **entire system**.

## Commands
```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password
```

## Key Idea

Search using:

- `-user`
- `-group`
- `-size`

Hide permission errors:

```bash
2>/dev/null
```

---

# Level 7 → Level 8
## Concept
Searching inside large files.

## Commands
```bash
grep millionth data.txt
```

## Key Idea
`grep` finds lines containing a **specific pattern**.

---

# Level 8 → Level 9
## Concept
Finding **unique lines** in a file.

## Commands
```bash
sort data.txt | uniq -u
```

## Key Idea

Pipeline:

```
sort → organize lines
uniq -u → show only unique lines
```

---

# Level 9 → Level 10
## Concept
Extracting readable text from **binary files**.

## Commands
```bash
strings data.txt | grep =
```

## Key Idea

- `strings` extracts readable characters
- `grep` filters results

---

# Level 10 → Level 11
## Concept
Decoding **Base64**.

## Commands
```bash
base64 -d data.txt
```

## Key Idea
Base64 is **encoding**, not encryption.

---

# Level 11 → Level 12
## Concept
Decoding **ROT13 cipher**.

## Commands
```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
```

## Key Idea
ROT13 rotates letters **13 positions** in the alphabet.

---

# Level 12 → Level 13
## Concept
Multi-layer **compression extraction**.

## Commands
```bash
mktemp -d
cd /tmp/<directory>
cp ~/data.txt .

xxd -r data.txt data.bin
file data.bin
```

Decompression tools used:

```
gunzip
bunzip2
tar -xf
```

## Key Idea
Always check file type using:

```bash
file <filename>
```

---

# Level 13 → Level 14
## Concept
Using an **SSH private key** for authentication.

## Commands
```bash
ssh -i sshkey.private bandit14@localhost -p 2220
cat /etc/bandit_pass/bandit14
```

## Key Idea

SSH keys provide **passwordless authentication**.

`-i` specifies the **identity file**.

---

# Important Linux Commands Learned

| Command | Purpose |
|------|------|
| ssh | Connect to remote machine |
| ls | List directory contents |
| cat | Display file contents |
| file | Detect file type |
| grep | Search text |
| find | Search files |
| sort | Sort lines |
| uniq | Filter duplicate lines |
| strings | Extract readable text |
| base64 | Encode/decode Base64 |
| tr | Translate characters |
| xxd | Convert hex dump to binary |
| tar | Extract archives |

---

# Useful Symbols

| Symbol | Meaning |
|------|------|
| \| | Pipe output to next command |
| > | Redirect output |
| >> | Append output |
| < | Redirect input |
| ! | Logical NOT |
| 2>/dev/null | Hide error messages |

---

# Linux Philosophy

Many Bandit levels rely on combining small tools:

```
command1 | command2 | command3
```

Each command does **one job well**, and pipelines combine them into powerful workflows.
