# Challenge Write-Up — Local Target

---

## 📌 Challenge Overview

| Field           | Information                                                                      |
| :-------------- | :------------------------------------------------------------------------------- |
| **Competition** | picoCTF                                                                          |
| **Category**    | Binary Exploitation                                                              |
| **Difficulty**  | Easy                                                                             |
| **Objective**   | Overflow an input buffer to overwrite an adjacent variable with the value 65 to get the flag |

---

## Initial Analysis

I was given a binary and its source code. Reading through the source, the win condition was obvious right away: if a variable called `num` equals `65`, the program prints the flag.

The problem is that nothing in the program ever sets `num` to `65` on its own. But there is a buffer nearby that we can overflow to write into it.

My plan:
- Understand how `input` and `num` sit in memory
- Figure out how many characters are needed to reach `num`
- Craft a payload that puts the value `65` into `num` through the overflow

---

## 🔎 Step 1 — Read the Source Code

The source code showed two key things. First, the win condition:

```c
if (num == 65) {
    // print the flag
}
```

Second, the vulnerable input:

```c
char input[16];
scanf("%s", input);
```

The `input` array is 16 bytes long. `scanf("%s", ...)` has no size limit, so if we type more than 16 characters, the extra bytes spill over into whatever comes next in memory — which is `num`.

This is a classic **stack buffer overflow**.

---

## Step 2 — Work Out the Payload

We need to:
1. Fill the 16 bytes of `input` with anything
2. Add extra bytes until we reach `num`
3. Make the byte that lands on `num` equal to `65`

`65` in decimal is `0x41` in hex, which is the ASCII character `A`.

So the payload is 16 or more filler characters followed by the letter `A`. After some trial and error, the working payload turned out to be:

```
123456789123456789123456A
```

That is 24 characters of filler to get past `input` and any padding in between, with `A` at the end to land on `num` and write the value `65` into it.

---

## Step 3 — Run the Exploit

I ran the binary and typed the payload when prompted:

```
123456789123456789123456A
```

The program checked `num`, saw `65`, and printed the flag. ✅

---

## 🏁 Flag

```
picoCTF{l0c4l5_1n_5c0p3_ee58441a}
```

---

## 🔬 What Made This Work

A buffer overflow happens when a program lets you write more data than the buffer can hold. The extra data does not just disappear — it keeps writing into whatever memory comes right after the buffer. In this case, `num` was sitting right next to `input` on the stack, so overflowing `input` wrote directly into `num`.

The key detail is that `A` has the ASCII value of `65`. So by placing `A` at just the right position in our input, we wrote `65` into `num` without ever directly touching it.

The one thing that made this possible: `scanf("%s", input)` reads unlimited input into a fixed 16 byte buffer with no bounds checking.

---

## 🎯 How to Solve Challenges Like This

1. Read the source code and find what value a variable needs to be set to
2. Find the input buffer that sits nearby in memory
3. Note the buffer size
4. Build a payload: fill the buffer with junk, then add the target value at the end
5. Use trial and error or GDB to fine tune the exact number of filler characters needed
6. Run the binary with the payload and read the flag

---

## 🧩 Final Thoughts

The big lesson here: **never use `scanf("%s", ...)` on a fixed size buffer**.

The fix is one small change: `scanf("%15s", input)` limits input to 15 characters, leaving room for a null terminator and preventing any overflow into `num`. That one missing number in the format string is all it took to make this exploitable.

Buffer overflows like this are one of the oldest and most well known vulnerability classes in computing. They show up again and again because the fix is easy to forget and the consequences of forgetting are severe.

---
