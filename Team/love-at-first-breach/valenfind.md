# 📝 Challenge Write-up: Valenfind

| Attribute | Details |
| :--- | :--- |
| **Event** | TryHackMe - Love at First Breach |
| **Category** | Web |
| **Difficulty** | Medium |
| **Target URL** | `http://10.49.143.34:5000` |

## 1. The Challenge Scenario
The challenge introduced us to a new dating app called "Valenfind," accompanied by a note suggesting the creator had only learned to code this year and that the app was "vibe-coded." Our objective was to explore the web application, identify any vulnerabilities left by the inexperienced developer, and exploit them to retrieve the hidden flag. 

![Valenfind Challenge Description](images/valenfind/challenge-description.png)

## 2. The Step-by-Step Solution
To tackle this, we heavily relied on Burp Suite to intercept and analyze the traffic between our browser and the server.

**Step 1: Initial Reconnaissance and Account Creation**
We started by opening the target URL in Firefox with our Burp Suite proxy turned on. We created a dummy account and filled in random profile details to gain access to the main dashboard. 

**Step 2: Exploring Profiles and Finding the Clue**
Once inside, we browsed through various dating profiles. Most were standard, but we noticed one profile named **Cupid** that had the maximum number of likes. Its bio was highly suspicious: "I keep the database secure. No peaking."

**Step 3: Discovering the Local File Inclusion (LFI) Vulnerability**
We decided to investigate Cupid's profile page further by looking at the HTTP responses in Burp Suite. In the response, we found an exposed HTML comment left by the developer: `Feature dynamic layout fetching vulnerability`. This comment explicitly pointed to a vulnerability in a `layout` parameter, hinting at a Local File Inclusion (LFI) flaw. 

**Step 4: Testing the LFI**
We intercepted the request responsible for changing the theme layout. We identified the `layout` parameter in the URL and sent this request to Burp Repeater. To confirm the LFI, we replaced the layout value with a standard directory traversal payload (`../../../../etc/passwd`). The server responded by dumping the `/etc/passwd` file, successfully confirming the vulnerability.

**Step 5: Extracting the Source Code**
We didn't just need system files; we needed the database. Knowing the app was likely built with Python/Flask based on standard web frameworks, we used the LFI vulnerability to hunt for the application's source code. By tweaking our directory traversal payload, we successfully read the contents of `app.py`. 

**Step 6: Analyzing `app.py` for Database Access**
Reading the source code revealed several critical pieces of information:
* An exposed **Admin API Key** variable.
* The database file name: `cupid.db`.
* A hidden backend route: `/api/admin/export_database`.
* A custom authentication header required to access this route: `X-Valentine-Token`. The code specified that this token must match the value of the Admin API Key.

**Step 7: Dumping the Database**
Armed with this knowledge, we crafted a completely new GET request in Burp Suite pointing to `/api/admin/export_database`. We manually added the custom header: `X-Valentine-Token: [The_Admin_API_Key_We_Found]`. Sending this request bypassed the authentication and caused the server to return the entire `cupid.db` SQLite database in the response. 

**Step 8: Finding the Flag**
We searched through the raw SQLite database dump returned in Burp Suite. Scrolling through the data, we successfully located the flag string hidden within the database records.

## 3. The Findings
By chaining a Local File Inclusion vulnerability to read the source code, we successfully bypassed authentication and downloaded the backend database. 

**Critical Information Disclosed:**
* **Vulnerable Parameter:** `layout`
* **Hidden Route:** `/api/admin/export_database`
* **Required Header:** `X-Valentine-Token`

**Target Found:** `THM{Why_coding_is_not_cup_of_mighty}`

## 4. Conclusion
This challenge highlighted two critical web application security flaws. First, it demonstrated the dangers of dynamic file inclusion without proper input sanitization, leading directly to an LFI vulnerability. Second, it showcased why hardcoding sensitive credentials (like Admin API keys) directly into the source code is a fatal mistake, as it allows attackers to escalate a simple file read into a complete database compromise.
