## Challenge Write-Up — SSTI2
---
## 📌 Challenge Overview
| Field                 | Information                                              |
| :-------------------- | :------------------------------------------------------- |
| **Competition**       | picoCTF                                                  |
| **Category**          | Web Exploitation                                         |
| **Difficulty**        | Medium                                                   |
| **Objective**         | Bypass login authentication and retrieve the hidden flag |
---
## Initial Analysis
I was given a website that asked for a username and password. I also downloaded an attachment called **app.tar.gz** which had the source code of the site. The files inside were: `admin.html`, `index.html`, `server.js`, and `package.json`. My plan was to:
* Look at the source code to understand how the site works
* Intercept the login request using Burp Suite
* Find a way to bypass the login and get the flag

---
## 🔎 Step 1 — Read the Source Code
I opened `server.js` and saw that the site was using a **MongoDB** database — this is a NoSQL database, not a regular SQL one.

I also noticed in `package.json` that the app handles JSON input. And if I enter wrong credentials, the site shows an **"Invalid Credentials"** error.

Most importantly, I found this in the source code:
```
token: { type: String, required: false, default: "{{Flag}}" }
```
This told me the **flag was stored inside a token field** in the database response.

---
## Step 2 — Intercept the Login Request
I turned on Burp Suite and tried to log in. I caught the POST request and saw it sent the email and password as JSON:

```json
{
  "email": "test@test.com",
  "password": "test"
}
```

Since the app accepts JSON input, I thought I could try a **NoSQL authentication bypass**.

---
## Step 3 — Try the NoSQL Bypass Payload
A common NoSQL bypass trick uses `{ "$ne": null }`, which means "not equal to null" — basically it matches anything. I changed the request to:

```json
{
  "email": { "$ne": null },
  "password": { "$ne": null }
}
```

But I got an error back:
```
"error": "email.startsWith is not a function"
```

This meant the `$` character was being blocked or not parsed correctly.

---
## Step 4 — Fix the Payload with Escape Characters
To get around the parsing issue, I wrapped the values in quotes and used `\"` to escape them:

```json
{
  "email": "{\"$ne\": null}",
  "password": "{\"$ne\": null}"
}
```

This time it worked! The server accepted the request and sent back a response that included the token field.

---
## Step 5 — Decode the Token
In the response I could see:

```
"token": "cGljb0NURntqQmhEMnk3WG9OelB2XzFZeFM5RXc1cUwwdUk2cGFzcWxfaW5qZWN0aW9uXzI1YmE0ZGUxfQ=="
```

I noticed the `==` at the end — that is a sign it is **Base64 encoded**. I decoded it and got the flag.

```text
picoCTF{jBhD2y7XoNzPv_1YxS9Ew5qL0uI6pasql_injection_25ba4de1}
```

---
## 🏁 Flag
```text
picoCTF{jBhD2y7XoNzPv_1YxS9Ew5qL0uI6pasql_injection_25ba4de1}
```
Success.

---
## 🔬 Technical Insight
This challenge showed me a common mistake in web security:

### ❌ Passing User Input Directly into Database Queries
The server was taking the email and password from the user and putting them straight into a MongoDB query — without checking or cleaning the input first. This let me send a special operator (`$ne`) that changed the meaning of the query and bypassed the login check completely.

The attack worked because:
* The app accepted raw JSON objects as input
* MongoDB operators like `$ne` were not blocked properly
* The flag was returned in the response token once I was "logged in"

---
## 🎯 Key Lesson
This challenge follows a simple pattern:
1. Read the source code to understand how the app works
2. Intercept the login request with Burp Suite
3. Try a NoSQL injection payload in the JSON body
4. Fix any parsing errors using escape characters
5. Decode the response token (Base64) to get the flag

---
## 🧩 Final Reflection
"SSTI2" taught me an important lesson:

**Never pass user-controlled input directly into database queries.**

By sending a MongoDB operator in the login fields, I was able to log in as any user without knowing the real password. A safer way would be to check and clean all user input before using it in a query, and to make sure special characters like `$` are not allowed in login fields.

---
