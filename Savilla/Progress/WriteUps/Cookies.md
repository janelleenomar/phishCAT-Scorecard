## Challenge Write-Up — Cookies
---
## 📌 Challenge Overview
| Field                 | Information                                              |
| :-------------------- | :------------------------------------------------------- |
| **Competition**       | picoCTF                                                  |
| **Category**          | Web Exploitation                                         |
| **Difficulty**        | Easy                                                     |
| **Objective**         | Manipulate the web cookie to find the hidden flag        |
---
## Initial Analysis
I was given a simple web app with a search form. Since this is a Web Exploitation challenge, my plan was to:
* Try searching different words and see what happens
* Look at how the site uses cookies
* Find a way to change the cookie to get the flag

---
## 🔎 Step 1 — Try the Search Form
I opened the site and tried submitting the word the page suggested: **"snickerdoodle"**.

The site sent me to a new page: `/check` and showed a positive message.

Then I tried a random word like **"text"**. This time I was NOT redirected. Instead, a red message appeared saying the word was not a valid biscuit.

So I learned that the site only redirects me when I search for a real biscuit name.

---
## Step 2 — Look at the Cookies
I opened the Firefox developer tools and checked my cookies while using the site.

I noticed three things:
* When I first opened the page, my cookie was set to: `name=-1`
* When I searched for a valid biscuit (like "snickerdoodle"), it changed to: `name=0`
* When I searched for an invalid word, it reset back to `-1`

This told me the server was using the cookie to track which biscuit I searched for.

---
## Step 3 — Test My Theory
I searched for another biscuit name: **"gingerbread"**. It worked — and my cookie changed to `name=23`.

This confirmed my idea: the server gives each biscuit a number, and stores that number in the cookie. Then the `/check` page reads the cookie and shows a message based on that number.

So if I change the cookie number myself, I can see different messages — and maybe find the flag.

---
## Step 4 — Write a Python Script to Try All Numbers
Instead of manually changing the cookie one by one, I wrote a simple Python script to try all numbers from 0 to 24 automatically:

```python
#!/bin/python3
import requests

for i in range(25):
    cookie = 'name={}'.format(i)
    headers = {'Cookie': cookie}

    r = requests.get('http://mercury.picoctf.net:<port>/check', headers=headers)

    if (r.status_code == 200) and ('picoCTF' in r.text):
        print(r.text)
```

The script sends a GET request to `/check` with a different cookie number each time. If the response contains the word `picoCTF`, it prints the result.

---
## Step 5 — Run the Script and Get the Flag
I ran the script and it found the flag automatically.

```text
picoCTF{3v3ry1_l0v3s_c00k135_064663e2}
```

---
## 🏁 Flag
```text
picoCTF{3v3ry1_l0v3s_c00k135_064663e2}
```
Success.

---
## 🔬 Technical Insight
This challenge showed me a common mistake in web security:

### ❌ Trusting Cookie Values Without Checking
The server let the cookie control what content was shown on the `/check` page. Since I could change my own cookie to any number I wanted, I could access content I was never supposed to see. The server never checked if I actually earned that cookie value.

This kind of attack is simple to do with:
* A Python script with a loop
* Burp Suite Intruder (as an alternative)

---
## 🎯 Key Lesson
This challenge follows a simple pattern:
1. Look at how the site behaves with different inputs
2. Check what cookies the site sets
3. Figure out what the cookie value controls
4. Change the cookie value to access hidden content
5. Automate it with a script to try all possible values

---
## 🧩 Final Reflection
"Cookies" taught me an important lesson:

**Never trust data that the user can change, like cookies, to control what they can see.**

The site gave me a cookie and then trusted whatever number was in it — without checking if I actually searched for that biscuit. A safer way would be to track this on the server side so users can't just change the value themselves.

---
