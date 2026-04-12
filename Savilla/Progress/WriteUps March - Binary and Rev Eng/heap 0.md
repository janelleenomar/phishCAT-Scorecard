# Challenge Write-Up — Heap 0

---

## 📌 Challenge Overview

| Field           | Information                                                              |
| :-------------- | :----------------------------------------------------------------------- |
| **Competition** | picoCTF                                                                  |
| **Category**    | Binary Exploitation                                                      |
| **Difficulty**  | Easy                                                                     |
| **Objective**   | Overflow a heap buffer to overwrite an adjacent variable and trigger the flag |

---

## Initial Analysis

I was given a binary, its source code, and a connection to a remote server. The challenge description asked:

> *Are overflows just a stack concern?*

That was a hint right away — this wasn't a stack overflow. The target was the **heap**, which is a different area of memory used for variables that are created while the program is running.

My plan:
- Read the source code to understand how memory is set up
- Find out which variable I needed to change
- Figure out how many characters I needed to type to overwrite it

---

## 🔎 Step 1 — Read the Source Code

The source code showed two variables stored on the heap:

- `input_data` — starts with the value `"pico"`
- `safe_var` — starts with the value `"bico"`

The program has a `check_win()` function that checks if `safe_var` still says `"bico"`. If it does — nothing happens. If it says **anything else** — it prints the flag.

```c
void check_win() {
    if (strcmp(safe_var, "bico") != 0) {
        printf("\nYOU WIN\n");
        // reads and prints flag.txt
    } else {
        printf("Looks like everything is still secure!\n");
    }
}
```

So the goal was clear: **change `safe_var` away from `"bico"`**.

---

## Step 2 — Find the Vulnerability

The program also has a `write_buffer()` function that lets you type input into `input_data`:

```c
void write_buffer() {
    printf("Data for buffer: ");
    scanf("%s", input_data);
}
```

The problem is `scanf("%s", ...)` — it reads whatever you type with **no size limit**. If you type more characters than `input_data` can hold, the extra characters spill over into the next chunk of memory — which is exactly where `safe_var` lives.

This is called a **heap overflow**.

---

## Step 3 — Find How Many Characters to Type

The program has a "print heap" option that shows the memory addresses of both variables:

```
[*] 0x63c3882552b0 -> pico   (input_data)
[*] 0x63c3882552d0 -> bico   (safe_var)
```

I subtracted the two addresses to find the gap between them:

```
0x63c3882552d0 - 0x63c3882552b0 = 0x20
```

`0x20` in decimal is **32**. So `safe_var` starts 32 bytes after `input_data`.

That means I need to type at least **33 characters** — 32 to fill the gap, plus 1 more to start overwriting `safe_var`.

---

## Step 4 — Run the Exploit

I connected to the remote server, chose the "write to buffer" option, and typed a string of 33 or more characters:

```
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
```

That's 33 `a`'s. The overflow overwrote `safe_var`, changing it from `"bico"` to something else.

---

## Step 5 — Get the Flag

I then chose the "print flag" option. Since `safe_var` no longer said `"bico"`, the check passed and the program printed the flag:

```
YOU WIN
picoCTF{...flag...}
```

✅

---

## 🏁 Flag

```
picoCTF{h34p_0v3rfl0w_<hash>}
```

---

## 🔬 What Made This Work

The heap is just another region of memory. When the program creates two variables back to back on the heap, they end up sitting next to each other in memory. If you can write past the end of the first one, you start writing into the second one.

The two things that made this possible:
- `scanf("%s", ...)` has **no size limit** — it writes as much as you type
- `input_data` and `safe_var` were **allocated right next to each other** on the heap

The program thought only the stack could be overflowed. This challenge proved that the heap can be just as vulnerable.

---

## 🎯 How to Solve Challenges Like This

1. Read the source code and look for variables stored on the heap
2. Find any input function with no size limit (like `scanf("%s", ...)` or `gets()`)
3. Use the program's debug output to find the addresses of both variables
4. Subtract the addresses to get the gap size
5. Type that many characters + 1 to overflow into the next variable
6. Trigger the win condition

---

## 🧩 Final Thoughts

The big lesson here: **overflows are not just a stack problem**.

Any time a program writes user input into a fixed-size buffer without checking the length, there is a potential overflow — whether it is on the stack or the heap. The heap just tends to get less attention, which makes it easy to overlook.

The fix is simple: use `scanf("%Ns", input_data)` where `N` is the max number of characters allowed. That one change would have stopped this attack completely.

---
