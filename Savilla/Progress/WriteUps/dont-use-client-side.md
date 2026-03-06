## Challenge Write-Up — dont-use-client-side
---
## 📌 Challenge Overview
| Field                 | Information                                              |
| :-------------------- | :------------------------------------------------------- |
| **Competition**       | picoCTF                                                  |
| **Category**          | Web Exploitation                                         |
| **Difficulty**        | Easy                                                     |
| **Objective**         | Find the hidden flag by reading the page source code     |
---
## Initial Analysis
I was given a link to a "super secure portal" that asked for a password. Since the challenge name was **"dont-use-client-side"**, it was a big hint that the password check was happening in the browser — not on the server. My plan was to:
* Look at the page source for anything hidden
* Find the flag or the password hidden in the client-side code

---
## 🔎 Step 1 — Open the Website
I opened the challenge link in my browser:
```
https://jupiter.challenges.picoctf.org/problem/17682/
```

I saw a simple login page asking me to enter a password to get into the portal.

---
## Step 2 — View the Page Source
Since there were no other hints, the first thing I did was press **Ctrl+U** to view the page source.

I looked through the HTML and JavaScript code and found the flag — split into parts inside the source code. I joined the parts together and got the full flag.

---
## Step 3 — Put the Flag Together
After joining the flag parts found in the source code:

```text
picoCTF{no_clients_plz_b706c5}
```

---
## 🏁 Flag
```text
picoCTF{no_clients_plz_b706c5}
```
Success.

---
## 🔬 Technical Insight
This challenge showed me a very common beginner mistake in web development:

### ❌ Doing Security Checks in the Browser (Client-Side)
The password check was written in JavaScript that runs in the browser. This means anyone can just open the page source and read the code — including any passwords or flags hidden inside it. The browser receives all the code before running it, so nothing in the client-side code is truly secret.

Things that should never be hidden in client-side code:
* Passwords or password checks
* Flags or secret values
* API keys or tokens

---
## 🎯 Key Lesson
This challenge follows a simple pattern:
1. Open the site and see what it does
2. Press `Ctrl+U` to view the page source
3. Search through the HTML and JavaScript for hidden values
4. Join any flag parts together to get the full flag

---
## 🧩 Final Reflection
"dont-use-client-side" taught me a very basic but important lesson:

**Never trust the client to keep secrets.**

Any code or data sent to the browser can be read by the user. If a password check or secret value is written in JavaScript, anyone can find it by just looking at the page source. Security checks should always happen on the server, where the user cannot see the code.

---
