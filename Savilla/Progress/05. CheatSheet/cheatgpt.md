
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

This file tells search engines what not to index — which often reveals hidden directories.
