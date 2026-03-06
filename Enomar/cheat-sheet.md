# 🛡️ Digital Forensics & CTF Cheat Sheet

A quick-reference guide for command-line syntax, file signatures, and analysis tools used in digital forensics and web exploitation challenges.

---

## 💻 Essential Command Line Tools

### 🐧 Kali Linux / Unix Commands
| Command | Usage | Example | Description |
| :--- | :--- | :--- | :--- |
| `cd` | `cd [directory_name]` | `cd Downloads` | **C**hange **D**irectory. Moves you into a different folder. Use `cd ..` to go back one folder. |
| `ls` | `ls -la` | `ls -la` | Lists all files in your current directory, including hidden files (Linux equivalent of `dir`). |
| `grep` | `grep "[string]" [file]` | `grep "picoCTF" flag.txt` | Searches a file for a specific string (case-sensitive by default). |
| `grep -i` | `grep -i "[string]" [file]` | `grep -i "picoctf" flag.txt` | Ignores case sensitivity when searching for a string. |
| `strings` | `strings [file] \| grep "pico"` | `strings target.bin \| grep "pico"` | Extracts human-readable text from binary files. Piping it to `grep` allows you to find flags hidden in "unrunnable" executables instantly. |
| `exiftool`| `exiftool [file]` | `exiftool image.png` | Extracts all hidden metadata (Author, GPS, hidden URLs) from files and images. |
| `base64` | `echo "[string]" \| base64 -d` | `echo "ZmxhZw==" \| base64 -d` | Decodes a Base64 string directly in the terminal. |
| `pdfinfo` | `pdfinfo [file.pdf]` | `pdfinfo document.pdf` | Extracts detailed metadata (Author, Creation Date, software used) specifically from PDF documents. |
| `steghide` | `steghide extract -sf [file.jpg]` | `steghide extract -sf image.jpg` | Extracts hidden steganographic data from image and audio files (usually requires a passphrase). |

### 🪟 Windows CMD Equivalents
| Command | Usage | Example | Description |
| :--- | :--- | :--- | :--- |
| `dir` | `dir` | `dir` | Lists all files and folders in the current directory. |
| `strings.exe` | `strings.exe [file]` | `strings.exe target.bin` | Windows executable version of the Linux `strings` tool. |
| `exiftool.exe`| `exiftool.exe [file]`| `exiftool.exe image.png` | Windows executable version of the ExifTool utility. |

---

## 🔍 Magic Bytes & File Signatures

Operating systems rely on file extensions, but the *true* file type is dictated by its hex signature (Magic Bytes) found at the very beginning of the raw file data.

| File Type | Hex Signature | ASCII Translation | Notes |
| :--- | :--- | :--- | :--- |
| **ZIP Archive** | `50 4B 03 04` | `PK` | PPTX, DOCX, and APK files are also ZIP archives and share this header. |
| **PNG Image** | `89 50 4E 47` | `.PNG` | Standard lossless image format. |
| **JPEG Image** | `FF D8 FF E0` | `...JFIF` | Standard lossy image format. |
| **PDF Document**| `25 50 44 46` | `%PDF` | Standard document format. |
| **Office Doc** | `50 4B 03 04` | `PK` | PPTX, DOCX, and PPTM files are actually renamed ZIP archives. |
| **PCAP File** | `D4 C3 B2 A1` | `....` | Standard packet capture file (often contains plaintext traffic). |

---

## 🛠️ Tool Arsenal & Quick Tactics

### Static Analysis
* **Notepad / Text Editor:** Safest way to perform initial static analysis on suspicious files (like PCAPs or PDFs) without executing them. Bypasses OS security blocks and visual redactions.
* **⚠️ Notepad Limitation:** Do not use basic text editors for large raw binary files (like high-res images). The massive amount of unreadable data will cause the program to freeze or crash. Pivot to CLI tools (like `exiftool` or `strings`) for these.
* **HxD (Hex Editor):** Used to inspect raw binary data, identify magic bytes, and modify broken file structures.
* **Safe Search & Execution Bypass:** If an OS (like Windows) blocks an unknown or suspicious file (such as a `.img` disk image) from opening, NEVER try to force-execute it. Opening it directly in Notepad allows you to safely read the raw binary data without triggering malicious code. From there, using `Ctrl + F` to search for known flag formats (e.g., `picoCTF`) acts as a quick, graphical equivalent to the `grep` command.
* **CLI vs. GUI Parsing:** For massive text files (thousands of lines), avoid standard text editors that might lag. Using `grep` in the Kali terminal is the fastest way to instantly filter out noise and isolate a flag. 
* **⚠️ Grep Case-Sensitivity:** Remember that `grep` is case-sensitive by default. If `grep "picoCTF"` fails, try `grep -i "picoctf"` to ignore capitalization and ensure you don't miss a flag hidden with different casing.

### Decoders & Converters
* **Base64 Identification:** Strings composed of random upper/lowercase letters and numbers that end with `=` or `==` (padding) are almost always Base64 encoded.
* **DevToys:** Offline suite for Base64 decoding, text manipulation, and formatting. Great for quick, local conversions securely.
* **CyberChef:** The "Cyber Swiss Army Knife" web app. 
    * *Pro-Tip:* Use the **"Magic"** operation when you have a random string of text and don't know what encoding was used; it will attempt to brute-force and auto-detect the decoding method.
* **Obfuscated Base64:** If you find a string that looks like Base64 but has spaces between characters (e.g., `Z m x h Z g = =`), remove all whitespace before attempting to decode it in DevToys or CyberChef.

### Extraction Tricks
* **Visual Bypasses:** Drawing a black box over text in a PDF often only masks the text visually. Press `Ctrl + A` (Select All) and paste into a text editor to strip the formatting and reveal hidden data.
* **SVG Analysis:** Because SVG images are built with XML code, hidden text within the image can often be extracted simply by opening the SVG in a web browser, pressing `Ctrl + A` (Select All), and pasting it into a text editor. If the copied text is fragmented or spaced out (e.g., `p i c o C T F`), simply remove the spaces to reconstruct the payload.
* **Extension Restoration / Correction:** If a file lacks an extension or has a fake one (like a `.txt` that throws an error or shows gibberish), inspect its header in a text editor. Look for ASCII magic bytes at the very beginning (like `PNG` for images, `JFIF` for JPEG, `%PDF` for PDF, or `PK` for ZIP). Renaming the file to match its true extension (e.g., `flag.txt` -> `flag.png`) will force the OS to render it correctly.
* **Hidden/Appended Strings:** Challenge creators often append plain-text flags to the very end of binary files (like `.jpg` images). Opening the file in Notepad and using `Ctrl + F` (or running the `strings` command in Linux) is the fastest way to extract data hidden in plain sight without needing advanced steganography tools.
* **Metadata Inspection:** Always make `exiftool` your first step for any media file (images, audio). Challenge creators frequently conceal flags or Base64 payloads inside obscure metadata properties such as the `License`, `Comment`, or `Attribution URL` fields.
* **Metadata Inspection (Notepad Method):** If you are on a Windows machine without ExifTool, you can still perform basic metadata analysis by opening any media file (JPG, PNG, PDF) directly in **Notepad**. Use `Ctrl + F` to search for `picoCTF` or other flag prefixes. This will often jump you straight to the "hidden" strings stored in the file's metadata fields (like the Artist or Comment properties) that aren't visible in an image viewer.
   * **Decoy Content:** If a file is filled with garbled nonsense or unselectable blacked-out text, ignore the visual content entirely. These are often decoys meant to waste time. Immediately pivot to metadata extraction (`pdfinfo` or `exiftool`) to find encoded payloads hidden in administrative fields like "Author."
* **Visual Layer Bypass (PDF):** Digital redaction (black boxes) in PDFs is often just a visual layer on top of the text. Using `Ctrl + A` (Select All) in a PDF viewer, copying, and pasting into Notepad will strip the visual overlays and reveal the "hidden" text underneath.

### Visual Data (QR Codes)
* **QR Code Payloads:** If a challenge provides an image that is just a QR code, the flag is encoded directly into the pixels. Use a scanner (mobile or online) to decode it.
* **Recursive Extraction:** Sometimes flags are buried deep inside multiple folders within a ZIP file. In Linux, use `find . -name "*.png"` after unzipping to quickly locate any image files without clicking through every subfolder.

### Polyglot Files (Dual-Format)
* **Polyglot Identification:** If a file provides one piece of a flag in one format (like a PDF) but the challenge title or hints suggest it is "multilingual" or "conflicting," it is likely a polyglot. 
* **Header Checking:** Inspect the file in a text editor or HxD. If a PDF document also contains a `PNG` or `PK` header, it is designed to be read by two different programs.
* **Combining Payloads:** Open the file twice—once with the original extension and once with the second identified extension (e.g., `.pdf` then `.png`). Combine the text found in both versions to reconstruct the full flag.
