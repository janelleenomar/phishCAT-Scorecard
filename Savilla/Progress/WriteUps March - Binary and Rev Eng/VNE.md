# Challenge Write-Up — VNE

---

## 📌 Challenge Overview

| Field           | Information                                                                              |
| :-------------- | :--------------------------------------------------------------------------------------- |
| **Competition** | picoCTF 2023                                                                             |
| **Category**    | Binary Exploitation                                                                      |
| **Difficulty**  | Easy                                                                                     |
| **Objective**   | Abuse an environment variable to inject extra commands into a root-level binary          |

---

## Initial Analysis

I was given SSH access to a remote server. On it there was a binary called `bin` that could list directories with root privileges. The goal was to use that elevated access to read the flag, which was stored somewhere only root could reach.

The key clue was in the tags: **env** and **injection**. The binary relied on an environment variable to decide what to do, and that variable was fully controlled by the user.

My plan:
- Connect to the server and run the binary to see what it expects
- Set the environment variable to point at the root directory
- Inject an extra command into the variable to read the flag file directly

---

## 🔎 Step 1 — Connect and Run the Binary

I SSHed into the server:

```bash
ssh ctf-player@saturn.picoctf.net -p 59803
# password: af86add3
```

Then I ran the binary:

```bash
./bin
```

It immediately complained:

```
Error: SECRET_DIR environment variable is not set
```

So the binary reads a `SECRET_DIR` environment variable and uses it as the directory to list. Without it, it refuses to run.

---

## Step 2 — Set the Environment Variable

I set `SECRET_DIR` to point at the root directory, which is where the flag was most likely stored:

```bash
export SECRET_DIR=/root
```

Running `./bin` again now listed the contents of `/root`. I could see `flag.txt` was there.

---

## Step 3 — Inject a Command to Read the Flag

Listing the directory was not enough. I needed to actually read the file. The binary was passing `SECRET_DIR` directly into a shell command without any sanitization. That means I could tack on extra shell commands at the end of the variable and they would get executed too.

I updated `SECRET_DIR` to include a second command after the directory path:

```bash
export SECRET_DIR="/root; cat /root/flag.txt"
```

The `;` tells the shell to run one command, then run the next one. So the binary first listed `/root` as usual, then ran `cat /root/flag.txt` and printed the flag. ✅

---

## 🏁 Flag

```
picoCTF{Power_t0_man!pul4t3_3nv_1ac0e5a3}
```

---

## 🔬 What Made This Work

Environment variables are just strings that programs read at runtime. When a program takes one of those strings and passes it directly into a shell command, the user has full control over what gets executed.

By putting a `;` inside `SECRET_DIR`, I ended the intended command early and started a completely new one. The binary had no idea — it just handed the whole string to the shell and the shell ran both commands.

This is called **environment variable injection**, and it is a specific form of command injection. The root cause is always the same: user-controlled input being passed to a shell without any cleaning or escaping.

The two things that made this possible:
- `SECRET_DIR` was set entirely by the user with no restrictions
- The binary passed it to the shell as-is, with no validation or escaping

---

## 🎯 How to Solve Challenges Like This

1. Connect to the server and run the binary to see what environment variable it needs
2. Set the variable to a valid path first to confirm the binary works
3. Add a `;` followed by your own command at the end of the variable value
4. Run the binary again and read the output

---

## 🧩 Final Thoughts

The big lesson here: **never pass user-controlled data directly into a shell command**.

The fix would be to validate `SECRET_DIR` before using it. For example, the binary could check that the value is a real directory path with no special characters like `;`, `|`, or `&&`. Better yet, it could avoid calling a shell altogether and use a direct system call like `opendir()` instead of passing the path to `ls`.

The flag name says it all: `Power_t0_man!pul4t3_3nv` — power to manipulate the environment. One unvalidated variable gave us full read access to the root filesystem.

---
