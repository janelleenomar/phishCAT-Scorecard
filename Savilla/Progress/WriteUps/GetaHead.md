## Challenge Write-Up — GET aHEAD
---
## 📌 Challenge Overview
| Field                 | Information                                              |
| :-------------------- | :------------------------------------------------------- |
| **Competition**       | picoCTF                                                  |
| **Category**          | Web Exploitation                                         |
| **Difficulty**        | Easy                                                     |
| **Objective**         | Change the HTTP request method to reveal the hidden flag |
---
## Initial Analysis
I was given a simple webpage with two buttons — one to change the background to red and one to change it to blue. The challenge name **"GET aHEAD"** was a big hint. I figured the flag was hidden somewhere in the HTTP response headers. My plan was to:
* Look at the page source for any clues
* Intercept the request using Burp Suite
* Try changing the HTTP method from GET to HEAD

---
## 🔎 Step 1 — Open the Website and Look Around
I opened the challenge URL and saw a simple page with two buttons:
* **"Choose Red"** — changes the background to red
* **"Choose Blue"** — changes the background to blue

I checked the page source with `Ctrl+U` but found nothing useful. So I decided to look at the actual HTTP requests being made.

---
## Step 2 — Intercept the Request with Burp Suite
I turned on **Intercept** in Burp Suite and clicked one of the buttons to catch the request.

The request was sent as a normal **GET** method:

```
GET / HTTP/1.1
Host: ...
```

Nothing unusual here. But the challenge name kept hinting at the **HEAD** method, so I decided to try changing it.

---
## Step 3 — Change GET to HEAD
In Burp Suite, I changed the HTTP method from **GET** to **HEAD** and forwarded the request.

The **HEAD** method works just like GET, but the server only sends back the **headers** — not the full page content. This makes it useful for finding hidden information that only shows up in the response headers.

---
## Step 4 — Get the Flag from the Response
After sending the HEAD request, the flag appeared in the response headers:

```text
picoCTF{r3j3ct_th3_du4l1ty_02cdde49}
```

---
## 🏁 Flag
```text
picoCTF{r3j3ct_th3_du4l1ty_02cdde49}
```
Success.

---
## 🔬 Technical Insight
This challenge showed me something important about HTTP methods:

### ❌ Hiding Sensitive Data in Response Headers
The server was sending the flag inside the HTTP response headers — but only when a HEAD request was made. Since most people only use GET or POST, this kind of information can go unnoticed. However, any tool like Burp Suite makes it easy to change the method and see what the server sends back.

Here is a quick summary of the HTTP methods involved:
* **GET** — asks the server for the full page content
* **HEAD** — asks the server for just the headers, no body

Tools I used:
* Burp Suite — to intercept and modify the HTTP request

---
## 🎯 Key Lesson
This challenge follows a simple pattern:
1. Open the site and look at what it does
2. Intercept the request with Burp Suite
3. Notice the HTTP method being used (GET)
4. Change it to HEAD and forward the request
5. Read the response headers to find the flag

---
## 🧩 Final Reflection
"GET aHEAD" taught me an important lesson:

**Sensitive data should never be placed in HTTP response headers.**

Just because the page body looks normal does not mean the headers are safe. Anyone with a tool like Burp Suite can easily change the request method and read whatever the server puts in its headers. Always check all parts of the HTTP response — not just what shows up in the browser.

---
