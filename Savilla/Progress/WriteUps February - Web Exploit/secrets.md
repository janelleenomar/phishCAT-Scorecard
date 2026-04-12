## Challenge Write-Up — Secrets
---
## 📌 Challenge Overview
| Field                 | Information                                                      |
| :-------------------- | :--------------------------------------------------------------- |
| **Competition**       | picoCTF                                                          |
| **Category**          | Web Exploitation                                                 |
| **Difficulty**        | Medium                                                             |
| **Objective**         | Navigate through hidden web directories to find the flag         |
---
## Initial Analysis
I was given a website with the prompt: **"We have several pages hidden. Can you find the one with the flag?"**

Since this is a Web Exploitation challenge, my plan was to:
* Inspect the page source and developer tools for hidden clues
* Look for hidden directories in the site's file structure
* Keep navigating deeper into those directories until I found the flag

---
## 🔎 Step 1 — Inspect the Page with Developer Tools
I right-clicked the page and selected **Inspect** to open the browser developer tools. I went to the **Sources** tab and looked through the files the page was loading.

Inside the `assets` folder, I noticed a directory called **`secret`**. This looked suspicious — it was not a normal folder name for a public website.

---
## Step 2 — Navigate to the Secret Directory
I typed the hidden path directly into the browser URL bar:

```
http://picoctf.net/secret/
```

The page loaded and showed a message:

```
You almost found me.
```

This confirmed I was on the right track. The flag was somewhere deeper inside this directory.

---
## Step 3 — Go Deeper: Find the Hidden Directory
I kept exploring and found another folder hidden inside `/secret/` called **`hidden`**.

I navigated to:

```
http://picoctf.net/secret/hidden/
```

The page loaded again but still no flag. I needed to go even deeper.

---
## Step 4 — Find the Superhidden Directory
Inside `/secret/hidden/`, I found one more folder called **`superhidden`**.

I navigated to:

```
http://picoctf.net/secret/hidden/superhidden/
```

This time the page showed the flag inside the page elements.

```text
picoCTF{succ3ss_@h3n1c@10n_39849bcf}
```

---
## 🏁 Flag
```text
picoCTF{succ3ss_@h3n1c@10n_39849bcf}
```
Success.

---
## 🔬 Technical Insight
This challenge showed me how hidden directories on a web server can expose sensitive content:

### ❌ Leaving Hidden Directories Accessible on a Live Server
Web servers work like folders on a computer. If a directory is not properly protected, anyone can visit it just by typing its path in the URL bar. Even if it is not linked anywhere on the site, it can still be found by:
* Checking the browser's Sources tab in developer tools
* Guessing common folder names
* Using directory brute-force tools

In this challenge, the directories were named `secret`, `hidden`, and `superhidden` — none of which were linked on the main page, but all were still fully accessible.

---
## 🎯 Key Lesson
This challenge follows a simple pattern:
1. Open developer tools and check the Sources tab for folder names
2. Type the folder path directly into the URL bar
3. If the page loads, look inside for more folders or files
4. Keep going deeper until you find the flag

---
## 🧩 Final Reflection
"Secrets" taught me an important lesson:

**Hidden does not mean protected.**

Just because a directory is not linked on the main page does not mean it is safe. If a server does not block access to a folder, anyone who knows — or guesses — the path can open it. Sensitive directories should always be properly protected with authentication or access controls, not just hidden from view.

---
