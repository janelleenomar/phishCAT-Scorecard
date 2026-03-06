## Challenge Write-Up — Cookie Monster Secret Recipe
---
## 📌 Challenge Overview
| Field                 | Information                                              |
| :-------------------- | :------------------------------------------------------- |
| **Competition**       | picoCTF                                                  |
| **Category**          | Web Exploitation                                         |
| **Difficulty**        | Easy                                                     |
| **Objective**         | Find a hidden cookie value and decode it to get the flag |
---
## Initial Analysis
I was given a website for "Cookie Monster." Since the challenge name mentions cookies, I figured the flag was probably hidden inside the browser's web cookies. My plan was to:
* Open the site and try logging in
* Use the browser's developer tools to check the cookies
* Decode whatever value I found in the cookies

---
## 🔎 Step 1 — Open the Website
I opened the challenge link in my browser. It showed a simple Cookie Monster themed login page.

---
## Step 2 — Open the Developer Tools
I pressed **Ctrl+Shift+I** to open the browser developer tools. This lets me see the HTML code, cookies, and other data the site is using in the background.

---
## Step 3 — Log In With Random Values
I tried logging in with any random username and password. Access was denied, but the error message gave a hint pointing to cookies.

I then went to the **Application tab** in the developer tools and clicked on **Storage → Cookies**.

I could see a cookie stored with the name **`secret_recipe`**. Its value was a long encoded string:

```
cGljb0NURntjMDBrMWVfbTBuc3Rlcl9sMHZlc19jMDBraWVzXzZFODFGQzFFfQ==
```

The `==` at the end was a clue — this looked like a **Base64 encoded** string.

---
## Step 4 — Decode the Cookie Value
I went to **CyberChef** (https://gchq.github.io/CyberChef/) and pasted the string in. I selected **"From Base64"** as the operation and decoded it.

The decoded result was the flag:

```text
picoCTF{c00k1e_m0nster_l0ves_c00kies_6E81FC1E}
```

---
## 🏁 Flag
```text
picoCTF{c00k1e_m0nster_l0ves_c00kies_6E81FC1E}
```
Success.

---
## 🔬 Technical Insight
This challenge showed me how cookies can hide sensitive data in plain sight:

### ❌ Storing Sensitive Data in Browser Cookies
The site stored the flag directly inside a browser cookie — just encoded in Base64. Base64 is **not encryption**. Anyone can decode it in seconds using free tools like CyberChef. Storing secret values in cookies that the user can see and read is a big security mistake.

Tools I used:
* Browser Developer Tools — to view the stored cookies
* CyberChef — to decode the Base64 string

---
## 🎯 Key Lesson
This challenge follows a simple pattern:
1. Open the site and try logging in
2. Open the developer tools and go to the Application tab
3. Check the cookies stored by the site
4. Look for any encoded or suspicious values
5. Decode the value using CyberChef or a similar tool

---
## 🧩 Final Reflection
"Cookie Monster Secret Recipe" taught me an important lesson:

**Never store secrets in browser cookies without proper encryption.**

Base64 looks like gibberish at first, but it is not secure — anyone can decode it instantly. If a site needs to store something sensitive, it should use real encryption and keep the secret on the server side, not in a cookie that the user can read and change.

---
