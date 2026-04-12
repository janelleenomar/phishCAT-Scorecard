# Challenge Write-Up — two-sum

---

## 📌 Challenge Overview

| Field           | Information                                                                         |
| :-------------- | :---------------------------------------------------------------------------------- |
| **Competition** | picoCTF 2023                                                                        |
| **Category**    | Binary Exploitation                                                                 |
| **Difficulty**  | Easy                                                                                |
| **Objective**   | Trigger an integer overflow by giving the program two numbers that break addition   |

---

## Initial Analysis

The challenge description asked a strange math question:

> What two positive numbers can make this possible: n1 > n1 + n2 OR n2 > n1 + n2?

Normally that is impossible. If both numbers are positive, adding them together should always produce a bigger result. But the hint said "integer overflow" — meaning this is not really a math problem. It is a computer memory problem.

My plan:
- Read the source code to understand what the program checks
- Understand how integer overflow works
- Find two numbers large enough to trigger it

---

## 🔎 Step 1 — Read the Source Code

The program reads two numbers from the user and passes them to a function called `addIntOvf`. That function checks whether the addition of the two numbers wrapped around and became negative:

```c
static int addIntOvf(int result, int a, int b) {
    result = a + b;
    if(a > 0 && b > 0 && result < 0)
        return -1;  // overflow happened
    ...
    return 0;       // no overflow
}
```

If `addIntOvf` returns `-1`, the program knows an overflow occurred and prints the flag. If it returns `0`, the program exits with "No overflow."

So the goal is to make `addIntOvf` return `-1`.

---

## Step 2 — Understand Integer Overflow

Computers store integers in a fixed amount of space. A 32-bit signed integer can hold values from roughly negative 2 billion up to positive 2,147,483,647. That upper limit is the maximum.

When you add two numbers and the result goes past that maximum, the number does not keep growing. Instead it wraps around and becomes a large negative number. This is called integer overflow.

For example:

```
2,147,483,647 + 1 = -2,147,483,648
```

That is impossible in real math, but that is exactly what happens in C with a 32-bit int. The two inputs are both positive, but the result is negative — which is exactly the condition the `addIntOvf` function checks for.

---

## Step 3 — Pick the Numbers and Run the Exploit

I needed two positive numbers that add up to more than 2,147,483,647. The simplest option is to use the maximum value itself for both numbers:

```
n1 = 2147483647
n2 = 2147483647
```

Their sum would be 4,294,967,294 — way past the 32-bit limit — so the result wraps around to a negative number. The overflow check triggers and the program prints the flag. ✅

---

## 🏁 Flag

```
picoCTF{Tw0_Sum_Integer_Bu773R_0v3rfl0w_76f333c8}
```

---

## 🔬 What Made This Work

Integer types in C have a hard ceiling. When addition pushes the value past that ceiling, C does not throw an error or stop the program. It just silently wraps the number around to the negative end of the range. This is called undefined behavior for signed integers, and it is a real source of bugs in production software.

The program actually tried to detect overflow using `addIntOvf`, but the check itself relies on the overflow happening first and producing a negative result. So there is no way to prevent the exploit — the very thing it is checking for is the exploit.

The two things that made this possible:
- The program used a 32-bit signed `int` with no bounds check on the inputs
- C silently wraps integers instead of crashing or rejecting the value

---

## 🎯 How to Solve Challenges Like This

1. Read the source code and find what condition triggers the flag
2. Look for any integer check or comparison involving user input
3. Check what data type is used — a 32-bit signed int maxes out at 2,147,483,647
4. Supply two numbers whose sum exceeds that limit
5. The overflow wraps the result to negative, satisfying the condition

---

## 🧩 Final Thoughts

The big lesson here: **computers cannot do math the way humans can**.

In real life, adding two big positive numbers always gives a bigger positive number. In C, if the result does not fit in the integer type, it wraps around silently. Programs that trust user input to stay within safe ranges without checking are vulnerable to exactly this kind of manipulation.

The fix would be to use a larger data type like a 64-bit `long long`, or to explicitly check whether either input is close to the maximum before doing the addition. Either change would have made this exploit impossible.

---
