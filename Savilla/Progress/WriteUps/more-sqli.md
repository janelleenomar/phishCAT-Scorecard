## Challenge Write-Up — More SQLi
---
## 📌 Challenge Overview
| Field                 | Information                                              |
| :-------------------- | :------------------------------------------------------- |
| **Competition**       | picoCTF                                                  |
| **Category**          | Web Exploitation                                         |
| **Difficulty**        | Medium                                                   |
| **Objective**         | Use SQL injection to bypass the login and retrieve the flag |
---
## Initial Analysis
I was given a login page that looked like it might be vulnerable to SQL injection. My plan was to:
* Try logging in with test values to see how the app responds
* Check if the app shows the raw SQL query in the response
* Craft a SQL injection payload to bypass the login
* Use Burp Suite to find the flag in the response

---
## 🔎 Step 1 — Try the Login with Test Values
I started by entering simple test credentials:

```
Username: test
Password: test
```

After clicking login, the response showed me the actual SQL query the server was running:

```sql
SELECT id FROM users WHERE password = 'test' AND username = 'test'
```

This was a big clue. The app was taking my input and putting it straight into the SQL query without cleaning it first. This means I can change what the query does just by typing special characters.

---
## Step 2 — Inject SQL Code to Bypass the Login
I knew that `1=1` is always true in SQL. So I tried this payload in both the username and password fields:

```
' OR 1=1; -- //
```

This changed the query to:

```sql
SELECT id FROM users WHERE password = '' OR 1=1; -- //' AND username = 'test'
```

Here is what each part does:
* `'` — closes the original string early
* `OR 1=1` — makes the condition always true
* `; -- //` — comments out the rest of the query so it is ignored

Since the condition is always true, the server thinks I am a valid user and lets me in.

---
## Step 3 — Use Burp Suite to Get the Flag
After logging in, I intercepted the request with **Burp Suite** and sent it to the **Repeater** tab.

I used the same SQL injection payload again:

```
' OR 1=1; -- //
```

I sent the request and looked at the response. The server returned user details and, inside the response body, the flag was there.

---
## Step 4 — Read the Flag from the Response
I found the flag inside the Burp Suite Repeater response:

```text
picoCTF{G3tting_5QL_1nJ3c7I0N_l1k3_y0u_m3an_1t_3cab9f85}
```

---
## 🏁 Flag
```text
picoCTF{G3tting_5QL_1nJ3c7I0N_l1k3_y0u_m3an_1t_3cab9f85}
```
Success.

---
## 🔬 Technical Insight
This challenge showed me how dangerous it is when apps do not clean user input:

### ❌ Putting User Input Directly Into SQL Queries
The server was taking whatever I typed in the login form and dropping it straight into a SQL query. This let me:
* Break out of the intended query structure using `'`
* Add my own SQL logic with `OR 1=1`
* Comment out the rest of the query using `-- //`
* Bypass the login check completely

The real fix is to use **prepared statements** (also called parameterized queries), which keep the user input separate from the SQL code so it can never change what the query does.

Tools I used:
* Browser — to test the login and see the raw query
* Burp Suite Repeater — to send modified requests and read the full response

---
## 🎯 Key Lesson
This challenge follows a simple pattern:
1. Try a test login and check if the raw SQL query is visible in the response
2. If it is, the app is likely vulnerable to SQL injection
3. Use `' OR 1=1; -- //` to make the condition always true
4. Intercept and replay the request in Burp Suite
5. Read the flag from the server's response

---
## 🧩 Final Reflection
"More SQLi" taught me an important lesson:

**Never put user input directly into a SQL query.**

If the app had used prepared statements, my payload would have been treated as plain text and not as SQL code. SQL injection is one of the oldest and most common web vulnerabilities, but it is also one of the easiest to prevent with the right coding practices.

---
