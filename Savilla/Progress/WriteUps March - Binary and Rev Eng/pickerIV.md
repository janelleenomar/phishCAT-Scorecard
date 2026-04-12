# Challenge Write-Up — Picker IV

---

## 📌 Challenge Overview

| Field           | Information                                                              |
| :-------------- | :----------------------------------------------------------------------- |
| **Competition** | picoCTF                                                                  |
| **Category**    | Binary Exploitation                                                      |
| **Difficulty**  | Easy                                                                     |
| **Objective**   | Find the address of the `win` function using GDB and pass it to the binary to get the flag |

---

## Initial Analysis

I was given a binary that asks you to enter a memory address in hex. It then jumps to whatever address you give it. Looking at the source code, there is a `win` function that prints the flag when it runs — but the program never calls it on its own.

The challenge is straightforward: find the address of `win` and hand it to the program.

My plan:
- Open the binary in GDB
- Look up the address of `win`
- Pass that address to the running program

---

## 🔎 Step 1 — Open the Binary in GDB

```bash
gdb picker-IV
```

---

## Step 2 — List All Functions and Their Addresses

Inside GDB, I ran:

```
(gdb) info functions
```

This printed a list of every function in the binary along with their addresses. The one I needed showed up clearly:

```
0x40129e  win
```

So `win` lives at address `0x40129e`.

---

## Step 3 — Pass the Address to the Binary

I ran the binary normally and when it asked for an address, I typed:

```
0x40129e
```

The program jumped to `win` and printed the flag. ✅

---

## 🏁 Flag

```
picoCTF{n3v3r_jump_t0_u53r_5uppl13d_4ddr35535_b8de1af4}
```

---

## 🔬 What Made This Work

This binary does something very dangerous: it takes a raw address from the user and jumps to it with no checks at all. There is no list of allowed addresses, no validation, nothing. Whatever you type, it runs.

This is called an **arbitrary jump** vulnerability. The programmer probably intended this as a feature to let the program call different functions, but by exposing it directly to user input they gave full control to whoever is running the program.

Unlike PIE TIME, this binary was **not compiled with PIE**. That means the addresses do not change between runs. The address of `win` you find in GDB locally is the same one you use on the remote server every single time.

The one thing that made this exploit possible: **the binary jumped to user input without any validation**.

---

## 🎯 How to Solve Challenges Like This

1. Read the source code and find the function that prints the flag (usually called `win`)
2. Open the binary in GDB and run `info functions` to get its address
3. Run the binary and enter that address when prompted
4. Collect the flag

---

## 🧩 Final Thoughts

Picker IV is a clean example of why programs should never execute arbitrary user input as code or a memory address. The fix here is simple: instead of letting the user type any address, the program should only allow jumping to a predefined list of valid functions.

The flag name itself spells out the lesson: `n3v3r_jump_t0_u53r_5uppl13d_4ddr35535` — never jump to user supplied addresses.

---
