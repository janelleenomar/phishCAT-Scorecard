# 🛡️ Digital Forensics & CTF Cheat Sheet

A quick-reference guide for command-line syntax, file signatures, and analysis tools used in digital forensics challenges.

---

## 💻 Essential Command Line Tools (Linux/Kali)

| Command | Usage | Example | Description |
| :--- | :--- | :--- | :--- |
| `grep` | `grep "[string]" [file]` | `grep "picoCTF" flag.txt` | Searches a file for a specific string (case-sensitive by default). |
| `grep -i` | `grep -i "[string]" [file]` | `grep -i "picoctf" flag.txt` | Ignores case sensitivity when searching for a string. |
| `strings` | `strings [file]` | `strings target.bin` | Extracts and prints all human-readable text from any binary or executable file. |
| `base64` | `echo "[string]" \| base64 -d` | `echo "ZmxhZw==" \| base64 -d` | Decodes a Base64 string directly in the terminal. |

---

## 🔍 Magic Bytes & File Signatures

Operating systems rely on file extensions, but the *true* file type is dictated by its hex signature (Magic Bytes) found at the very beginning of the raw file data.

| File Type | Hex Signature | ASCII Translation | Notes |
| :--- | :--- | :--- | :--- |
| **ZIP Archive** | `50 4B 03 04` | `PK` | PPTX, DOCX, and APK files are also ZIP archives and share this header. |
| **PNG Image** | `89 50 4E 47` | `.PNG` | Standard lossless image format. |
| **JPEG Image** | `FF D8 FF E0` | `...JFIF` | Standard lossy image format. |
| **PDF Document**| `25 50 44 46` | `%PDF` | Standard document format. |

---

## 🛠️ Tool Arsenal & Quick Tactics

### Static Analysis
* **Notepad / Text Editor:** Safest way to perform initial static analysis on suspicious files without executing them. Bypasses OS security blocks.
* **HxD (Hex Editor):** Used to inspect raw binary data, identify magic bytes, and modify file structures.

### Decoders & Converters
* **DevToys:** Offline suite for Base64 decoding, text manipulation, and formatting.
* **CyberChef:** The "Cyber Swiss Army Knife" web app for stacking multiple decoding operations (Base64, Hex, ROT13, etc.).

### Browser Tricks
* **SVG Analysis:** Because SVG images are built with XML code, hidden text within the image can often be extracted simply by opening the SVG in a web browser, pressing `Ctrl + A` (Select All), and pasting into a text editor.
