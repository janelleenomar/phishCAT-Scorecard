# Challenge Write-Up — Format String 1

---

## 📌 Challenge Overview

| Field           | Information                                                                    |
| :-------------- | :----------------------------------------------------------------------------- |
| **Competition** | picoCTF                                                                        |
| **Category**    | Binary Exploitation                                                            |
| **Difficulty**  | Easy                                                                           |
| **Objective**   | Exploit a format string vulnerability to leak stack memory and decode the flag |

---

## Initial Analysis

I was given a binary, its source code, and access to a remote server. The program takes user input and prints it back — simple enough on the surface. But looking at the source code, there was one line that stood out immediately as dangerous.

My plan:
- Find the vulnerable line in the source code
- Send format string tokens as input to dump memory
- Decode the hex output into readable text to get the flag

---

## 🔎 Step 1 — Find the Vulnerability in the Source Code

Inside the source code, I found this line:

```c
printf(buf);
```

This is a **format string vulnerability**. Normally, `printf` should be written like this:

```c
printf("%s", buf);
```

The difference matters a lot. When you write `printf(buf)` and the user controls `buf`, the user can put format tokens like `%p`, `%x`, or `%s` directly into their input. `printf` will then treat those tokens as real instructions and **read values off the stack** — memory it was never supposed to show you.

---

## Step 2 — Send `%p` Tokens as Input

I connected to the remote server and instead of typing normal text, I typed a long chain of `%p` tokens:

```
%p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p
```

`%p` tells `printf` to print the next value on the stack as a pointer (a hex number). Since I gave it 20 of them, it printed 20 values straight off the stack.

The output looked something like this:

```
0x1 0x7ffce4a20000 0x405314 0x6969696969696969 0x7025207025207025
0x6f636970 0x7b465443 0x346e316d 0x355f316c 0x5f337...
```

That's raw memory — stack data dumped as hex numbers.

---

## Step 3 — Decode the Hex Output

The flag was sitting in that dump, just encoded as hex. I used **CyberChef** (a free browser tool for data conversion) to decode it.

The steps in CyberChef:
1. Take each hex value from the output
2. Use **"From Hex"** to convert the numbers to text
3. **Reverse** the bytes (because x86 systems store bytes in little-endian order — the bytes are backwards)
4. Trim any junk values that aren't part of the flag

After rearranging the decoded chunks in the right order, the flag appeared.

---

## 🏁 Flag

```
picoCTF{4n1m41_57y13_4x4_f14g_50396c64}
```

---

## 🔬 What Made This Work

A format string vulnerability happens when user input is passed directly to `printf` with no format string. `printf` uses the format tokens (like `%p`, `%x`, `%s`) to decide what to read and print. When the user controls those tokens, they can read things from memory that the program never intended to share.

In this case, the flag was stored somewhere on the stack. By sending enough `%p` tokens, I was able to dump the stack values one by one until the flag data showed up in the output.

**Why the output was backwards:** x86 processors store multi-byte values in **little-endian** format, meaning the smallest byte comes first. So the text "pico" in memory is stored as `6f636970` (reversed). The reverse step in CyberChef fixes that.

The two things that made this possible:
- `printf(buf)` instead of `printf("%s", buf)` — one small mistake with big consequences
- The flag data was stored in stack memory close enough to be leaked by `%p` tokens

---

## 🎯 How to Solve Challenges Like This

1. Read the source code and look for `printf(buf)` or any `printf` where user input is the first argument
2. Connect to the server and send a long string of `%p %p %p ...` as input
3. Copy the hex output and paste it into CyberChef
4. Apply "From Hex" then "Reverse"
5. Look for the `picoCTF{` pattern in the decoded output — that's your flag

---

## 🧩 Final Thoughts

The big lesson here: **one missing argument in `printf` can leak your entire stack**.

The fix is just two characters — changing `printf(buf)` to `printf("%s", buf)`. That tells `printf` exactly how to treat the input: as a plain string, nothing more. Without that fix, the user is in control of how `printf` reads memory, which is a very dangerous position to be in.

Format string bugs are easy to miss in code review but very easy to exploit. Any time you see `printf` taking a variable as its first and only argument, that's a red flag worth investigating.

---
