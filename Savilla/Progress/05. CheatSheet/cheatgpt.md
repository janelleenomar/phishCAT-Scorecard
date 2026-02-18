
---

## Common CTF Techniques (Web & Beginner Level)

Capture The Flag (CTF) challenges often test observation, curiosity, and understanding of how web applications work internally. Many flags are hidden in places that normal users do not check.

---

### 1. Check HTML / CSS / JavaScript Using Inspect

Modern browsers allow you to inspect the structure of a webpage.

### What to check:

* Hidden HTML elements (`display:none`, `hidden`, or comments)
* Disabled buttons or inputs
* JavaScript variables containing secrets
* Hardcoded flags or hints
* Obfuscated scripts

### How:

* Right click → **Inspect**
* Open **Elements** tab
* Search (`Ctrl + F`) for:

  * `flag`
  * `secret`
  * `hidden`
  * suspicious comments

### Why this works:

Developers sometimes hide information on the client side assuming users won’t look at the source.

---

## 2. Check Network Requests, Cookies, and Headers

Websites constantly send requests between browser and server. Flags or hints may appear here.

### Network Tab:

Look for:

* API responses containing hidden data
* JSON responses
* Files loaded in background
* Requests returning unusual responses

Steps:

1. Open Developer Tools
2. Go to **Network**
3. Refresh the page
4. Inspect requests one by one

### Cookies:

Cookies may contain:

* Encoded values
* Session data
* Base64 strings
* Role information (e.g., `user=admin`)

Try decoding cookie values using:

* Base64 decode
* URL decode

### Headers:

Check:

* `Authorization`
* `User-Agent`
* Custom headers
* Server information

Sometimes flags are placed in headers intentionally.

---

## 3. Use Burp Suite to Modify Requests or Responses

Burp Suite is a proxy tool used in web security testing.

### What you can do:

* Intercept requests before sending
* Modify parameters
* Change headers
* Replay requests
* Test authentication bypass

### Common uses in CTF:

* Change `role=user` → `role=admin`
* Modify IDs (`id=1` → `id=2`)
* Remove restrictions
* Bypass client-side validation

### Example:

If a request sends:

```
POST /login
username=user&admin=false
```

Try changing it to:

```
username=user&admin=true
```

---

## 4. View Page Source

Different from Inspect.

### Difference:

* **View Source** shows original HTML sent by server.
* **Inspect** shows modified DOM after JavaScript runs.

### What to check:

* HTML comments
* Hidden links
* Unused scripts
* Metadata

Shortcut:

```
Ctrl + U
```

---

## 5. Edit the URL (Directory and File Discovery)

Many challenges hide files in predictable locations.

### Common examples:

* `/robots.txt`
* `/admin`
* `/backup`
* `/hidden`
* `/flag.txt`
* `/index.old`

### robots.txt

---

# 6. ATTACKER MINDSET

When you see:

* `?file=`
* `?layout=`
* `?template=`
* `?page=`
* `/api/`
* `/admin/`
* `/export/`
* `/download/`

Think:

> “Can I make this return something unintended?”

Always test:

* Absolute paths
* Relative traversal
* Config files
* Source code

---

# 7. ENUMERATION CHECKLIST

## 🔍 Parameter Testing

If you see:

```
/api/fetch_layout?layout=something.html
```

Test:

```
/etc/passwd
../../../../etc/passwd
/opt/app/app.py
app.py
```

Goal:

* Confirm file read
* Identify app location
* Identify tech stack

---

## 🔍 Basic LFI Test Payloads

```
/etc/passwd
/etc/hosts
/var/www/html/app.py
/opt/app/app.py
../../../../etc/passwd
```

If output changes → vulnerability confirmed.

---

# 8. LOCAL FILE INCLUSION (LFI)

## 🔥 Definition

Occurs when user-controlled input is used in file operations without validation.

Example vulnerable code:

```python
file_path = os.path.join(base_dir, layout_file)
open(file_path)
```

No sanitization → attacker controls path.

---

## 🔥 Indicators of LFI

* File contents displayed in response
* Error messages revealing file paths
* No strict extension validation

---

## 🛡 Common Developer Mistakes

* Using `os.path.join()` without checking traversal
* Blacklist filtering instead of whitelist
* Not validating filename against allowed list

---

# 9. SOURCE CODE REVIEW CHECKLIST

Once you get source code:

Search for:

```
API_KEY
SECRET
TOKEN
PASSWORD
DB
admin
export
debug
```

In Python apps:

Look for:

```python
ADMIN_API_KEY =
app.secret_key =
DATABASE =
```

---

# 10. SECRET DISCOVERY SECTION

## 🔥 Hardcoded Secrets

If you find:

```python
ADMIN_API_KEY = "CUPID_MASTER_KEY_2024_XOXO"
```

Ask:

* Where is this used?
* Is there an admin endpoint?
* Is it checked in headers?

---

## 🔥 Header-Based Authentication

Look for:

```python
request.headers.get()
```

Exploit with:

```
curl -H "Header-Name: value"
```

Example:

```
curl /api/admin/export_db -H "X-Valentine-Token: KEY"
```

---

# 11. PRIVILEGE ESCALATION VIA API

If admin endpoint found:

Test:

```
GET /api/admin/
GET /api/admin/export
GET /api/admin/download
GET /api/admin/debug
```

Check:

* Token validation
* Weak comparison
* Hardcoded keys

---

# 12. DATABASE ENUMERATION

If DB downloaded:

### SQLite

```
sqlite3 database.db
.tables
.schema users
select * from users;
```

Look for:

* admin accounts
* flags
* password reuse
* internal notes

---

# 13. FULL ATTACK FLOW MODEL

Use this mental model:

1. 🔎 Find input parameter
2. 🔓 Exploit file read
3. 📂 Retrieve source code
4. 🔑 Find secrets
5. 🚪 Access hidden endpoint
6. 💾 Dump database
7. 🚩 Extract flag

This pattern appears VERY often in CTFs.

---
