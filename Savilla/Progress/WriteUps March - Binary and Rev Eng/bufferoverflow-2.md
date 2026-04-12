# Challenge Write-Up — Buffer Overflow 2

---

## 📌 Challenge Overview

| Field           | Information                                                                                          |
| :-------------- | :--------------------------------------------------------------------------------------------------- |
| **Competition** | picoCTF 2022                                                                                         |
| **Category**    | Binary Exploitation                                                                                  |
| **Difficulty**  | Medium                                                                                               |
| **Objective**   | Overflow the buffer to redirect execution to `win()`, then also plant the two correct argument values on the stack so the flag check passes |

---

## Initial Analysis

I was given a 32-bit binary and its source code. This challenge builds directly on Buffer Overflow 1. We still need to overflow the buffer and hijack the return address to call `win()`. But this time, `win()` has a twist: it checks two arguments before printing the flag, and both have to match specific values.

Simply jumping to `win()` is not enough. We also need to control what is on the stack after the return address, because that is where the function will look for its arguments.

My plan:
- Read the source code to understand what `win()` checks
- Use GDB to find the exact offset to the return address
- Figure out the stack layout after the return address to place the arguments correctly
- Build a payload with padding, the address of `win()`, filler for the fake return address, and then the two required argument values

---

## 🔎 Step 1 — Read the Source Code

The source code had three functions. `main()` called `vuln()`, and `vuln()` read input using `gets()` into a buffer — the same unsafe pattern from the previous challenges.

`win()` was never called anywhere, but it contained the flag. The catch was the check inside it:

```c
void win(uint arg1, uint arg2) {
    if (arg1 != 0xCAFEF00D)
        return;
    if (arg2 != 0xF00DF00D)
        return;
    // print the flag
}
```

If either argument is wrong, the function exits silently. We need both values to be exactly right.

Running `checksec` on the binary showed:

```
NX: enabled
PIE: disabled
```

No PIE means the address of `win()` is fixed at `0x08049296`. NX means we cannot run shellcode from the stack, but we do not need to — we are just calling an existing function.

---

## Step 2 — Find the Offset to the Return Address

I opened the binary in GDB and used the cyclic pattern technique to find exactly how many bytes are needed before we start overwriting EIP:

```bash
gdb ./vuln
(gdb) pattern create 200
```

I ran the binary, pasted the pattern as input, and the program crashed. The value in EIP at the crash was `0x62616164`. I looked that up:

```bash
(gdb) pattern offset 0x62616164
# → 112
```

The offset was **112 bytes**. That means 112 bytes of junk fills the buffer and the saved frame pointer, and then the next 4 bytes land on EIP.

---

## Step 3 — Understand How Arguments Work on a 32-bit Stack

On a 32-bit system, when one function calls another, arguments are pushed onto the stack before the call. After the call, the stack looks like this from top to bottom:

```
[return address]  ← we control this (set it to win())
[arg1]            ← win()'s first argument
[arg2]            ← win()'s second argument
```

But there is one more thing: after the return address comes what would normally be the caller's return address — a 4-byte slot we need to fill with something (even junk) before placing the arguments. So the full layout we need to build is:

```
[112 bytes padding] + [address of win()] + [4 bytes junk] + [arg1] + [arg2]
```

---

## Step 4 — Verify the Argument Positions With GDB

I set breakpoints inside `win()` at the two comparison instructions to confirm the arguments were landing in the right place. After adding the argument values to the payload and running with GDB, I could see that the memory addresses being compared matched `0xCAFEF00D` and `0xF00DF00D`. ✅

---

## Step 5 — Build the Final Payload

With all the pieces confirmed, the final exploit script looked like this:

```python
#!/usr/bin/env python3

from pwn import *
import sys

host = sys.argv[1]
port = 56164

binary = context.binary = ELF("./vuln")
context(os="linux", arch="i386")

connect = remote(host, port)

connect.recvuntil(b"Please enter your string:")

payload  = b"A" * 112          # overflow up to the return address
payload += p32(0x08049296)     # address of win()
payload += b"A" * 4            # fake return address (junk)
payload += p32(0xCAFEF00D)     # arg1
payload += p32(0xF00DF00D)     # arg2

connect.sendline(payload)
connect.recv()
connect.interactive()
```

Running this against the server passed both argument checks inside `win()` and printed the flag. ✅

---

## 🏁 Flag

```
picoCTF{argum3nt5_4r3_b0r1ng_<hash>}
```

---

## 🔬 What Made This Work

On a 32-bit system, function arguments live on the stack right after the return address. Because we can write freely past the end of `buf`, we control not just the return address but also everything that comes after it — including the slots where `win()` will look for its arguments when it runs.

The 4 bytes of junk between `win()`'s address and the first argument represents a fake return address. This is where `win()` would return to when it finishes. We do not care where it goes because `win()` calls `exit()` after printing the flag anyway.

The three things that made this exploit possible:
- `gets()` in `vuln()` with no size limit
- No PIE, so `win()`'s address was fixed
- 32-bit calling convention, which puts arguments on the stack where we can reach them

---

## 🎯 How to Solve Challenges Like This

1. Read the source code and find what values `win()` checks for in its arguments
2. Use the cyclic pattern trick in GDB to find the return address offset
3. Confirm the argument positions by examining the stack in GDB at the comparison instructions
4. Build the payload: padding + address of win() + 4 bytes junk + arg1 + arg2
5. Send it to the server and collect the flag

---

## 🧩 Final Thoughts

Buffer Overflow 2 adds an important new layer on top of Buffer Overflow 1. Redirecting execution is not always enough. Many real-world functions need specific arguments to do anything useful, and this challenge shows that those arguments are just more values sitting on the stack — values we can plant just as easily as we plant the return address.

The fix is the same as always: replace `gets()` with `fgets()`. That one change would have capped the input and prevented any of this from reaching past the buffer, let alone all the way to the return address and beyond.

---
