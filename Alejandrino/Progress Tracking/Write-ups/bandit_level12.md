# OverTheWire: Bandit Level 12 → Level 13

## 1. Objective

The goal of this level is to retrieve the password stored in `data.txt`, which is a **hexdump** of a file that has been **repeatedly compressed**. The challenge requires creating a temporary workspace, reversing the hexdump, and iteratively decompressing the file using various Linux tools.

---

## 2. Connection Details

- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **Username:** `bandit12`
- **Password:** `7x16WNeHIi5YkIhWsffIQoognUTyj9Q4`

---

## 3. Technical Process (Terminal Evidence)

This level involves a complex **multi-layer decompression process**. I used the `file` command at each step to determine the compression format and decide which tool to use next.

```bash
# 1. Create a temporary working directory
bandit12@bandit:~$ mktemp -d
/tmp/tmp.ZLDczLjbme

# Move into the directory
bandit12@bandit:~$ cd /tmp/tmp.ZLDczLjbme

# Copy the data file
bandit12@bandit:/tmp/tmp.ZLDczLjbme$ cp ~/data.txt .

# 2. Reverse the hexdump to create the binary file
bandit12@bandit:/tmp/tmp.ZLDczLjbme$ xxd -r data.txt data.bin

# 3. Identify the file type
bandit12@bandit:...$ file data.bin
data.bin: gzip compressed data

# Rename and decompress gzip
bandit12@bandit:...$ mv data.bin data.gz
bandit12@bandit:...$ gunzip data.gz

# 4. Identify next layer
bandit12@bandit:...$ file data
data: bzip2 compressed data

# Decompress bzip2
bandit12@bandit:...$ mv data data.bz2
bandit12@bandit:...$ bunzip2 data.bz2

# 5. Identify tar archive
bandit12@bandit:...$ file data
data: POSIX tar archive

# Extract tar archive
bandit12@bandit:...$ tar -xf data

# Repeat process as new files appear
# Eventually the final file is ASCII text

bandit12@bandit:...$ cat data8
FO5dwFsc0cbaIIh0h8j2eUks2vdTDwAn
```
<img width="975" height="377" alt="image" src="https://github.com/user-attachments/assets/8035245c-a3ab-47cd-bf32-0be24c52ae78" />
<img width="975" height="804" alt="image" src="https://github.com/user-attachments/assets/19c9292c-f78b-4960-9253-a7431bfabf21" />

---

## 4. Key Takeaways & Commands

- **`mktemp -d`** – Creates a secure temporary directory where files can be safely manipulated.
- **`xxd -r`** – Reverses a hex dump back into its original binary format.
- **`file`** – Identifies the actual file type regardless of the filename extension.
- **`gunzip`** – Decompresses `.gz` (Gzip) files.
- **`bunzip2`** – Decompresses `.bz2` (Bzip2) files.
- **`tar -xf`** – Extracts files from a `.tar` archive.

---

## 5. Reflection & Lessons Learned

- **The "File First" Rule** – I learned never to trust file extensions. Many files in this challenge were labeled `.bin` but actually contained compressed archives. Using `file` first prevents mistakes.
- **Working in `/tmp`** – Home directories in CTF environments often restrict file creation. Using `mktemp` in `/tmp` provides a clean workspace for creating temporary files.
- **Layered Compression** – This challenge simulated real-world scenarios where attackers or software pack files multiple times. Decompressing step-by-step is similar to malware unpacking techniques.
- **Tool Sensitivity** – Some decompression tools rely on correct file extensions, requiring files to be renamed before they can be processed.

---

## 6. Password Discovered

**Level 13 Password:** `FO5dwFsc0cbaIIh0h8j2eUks2vdTDwAn`
