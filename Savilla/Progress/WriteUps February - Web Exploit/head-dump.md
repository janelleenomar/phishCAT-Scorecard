## Challenge Write-Up — head-dump
---
## 📌 Challenge Overview
| Field                 | Information                                                        |
| :-------------------- | :----------------------------------------------------------------- |
| **Competition**       | picoCTF                                                            |
| **Category**          | Web Exploitation                                                   |
| **Difficulty**        | Easy                                                               |
| **Objective**         | Find a hidden endpoint that exposes a memory dump containing the flag |
---
## Initial Analysis
I was given a simple blog website. The challenge told me that one of the articles talks about API documentation and that the flag was hidden inside a file generated from the server's memory. My plan was to:
* Look at the page source for any hidden clues
* Find the API documentation page
* Look for any endpoints that shouldn't be public
* Download and search the memory file for the flag

---
## 🔎 Step 1 — View the Page Source
I opened the site in my browser and pressed `Ctrl+U` to view the page source.

I found this interesting path in the code:
```
/api-docs/#/
```

This told me the site was using **Swagger** — a tool that shows all the available API endpoints of a web app. This is very useful for finding hidden or unintended endpoints.

---
## Step 2 — Open the Swagger API Docs
I went to:
```
http://verbal-sleep.picoctf.net:51368/api-docs/#/
```

This opened the **API documentation page**, which listed all the endpoints the server had. I looked through all of them and found one that stood out right away:

```
GET /heapdump
```

A heapdump endpoint should never be public — it gives out a snapshot of everything the server has in memory at that moment, which can include sensitive data like passwords, tokens, and flags.

---
## Step 3 — Download the Heap Dump
I went to the heapdump URL and downloaded the file using `wget`:

```bash
wget http://verbal-sleep.picoctf.net:51368/heapdump -O heapdump
```

I then checked what type of file it was:

```bash
file heapdump
# Output: ASCII text, with very long lines
```

This told me it was a **Node.js heap snapshot** — basically a very large JSON file full of everything the server had in memory.

---
## Step 4 — Search the File for the Flag
Instead of reading through the whole file manually, I used a quick command to search for the flag:

```bash
strings heapdump | grep picoCTF
```

This looked through all readable text in the file and found any line containing "picoCTF". It worked right away and gave me the flag:

```text
picoCTF{Pat!3nt_15_Th3_K3y_f1179e46}
```

---
## 🏁 Flag
```text
picoCTF{Pat!3nt_15_Th3_K3y_f1179e46}
```
Success.

---
## 🔬 Technical Insight
This challenge showed me how dangerous exposed memory dumps can be:

### ❌ Leaving Debug Endpoints Open on a Live Server
A heap dump is a full snapshot of the server's memory. It can contain:
* Passwords and secret tokens
* Session data
* Hidden flags (as in this challenge)
* Any other data the app was holding at that moment

The `/heapdump` endpoint was only meant for debugging, but it was left open for anyone to access. Combined with the Swagger docs also being public, finding it was easy.

Tools I used to analyze the file:
* `wget` — to download the file
* `file` — to check what kind of file it was
* `strings` + `grep` — to search for readable text inside it

---
## 🎯 Key Lesson
This challenge follows a simple pattern:
1. View the page source to find hidden paths
2. Open the Swagger/API docs to see all endpoints
3. Look for endpoints that should not be public
4. Download the exposed file
5. Use `strings` and `grep` to search for the flag

---
## 🧩 Final Reflection
"head-dump" taught me an important lesson:

**Never leave debug endpoints open on a public server.**

A heap dump is a very powerful tool for developers, but it should never be accessible to anyone outside the development team. If I can reach `/heapdump` from my browser, so can anyone else — and everything in memory is exposed. Always remove or protect these kinds of endpoints before putting a site live.

---
