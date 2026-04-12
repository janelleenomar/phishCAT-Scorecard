# 🛡️ OSINT, IMINT & AI Security Cheat Sheet

A comprehensive reference for digital footprinting, geolocation, image intelligence, and Large Language Model (LLM) red teaming.

---

## 💻 Essential Command Line & Investigative Tools

### 🐧 Terminal-Based Tools (Kali / Linux)
| Command | Usage | Description |
| :--- | :--- | :--- |
| `exiftool` | `exiftool [file]` | Extracts hidden metadata (Copyright, GPS, Author) from images and PDFs. Critical for finding aliases like `OWoodflint`. |
| `strings` | `strings [file] | grep -i "[flag]"` | Extracts human-readable text from binary files. Useful for finding flags hidden in non-text files. |
| `irssi` | `irssi -c irc.texsaw.org` | Command-line IRC client. Used to connect to competition servers and retrieve flags via `/motd`. |
| `whois` | `whois [domain]` | Reveals domain registration details, name servers, and occasionally owner contact info. |

### 🌐 Web-Based Investigative Platforms
| Tool | Purpose | Key Use Case |
| :--- | :--- | :--- |
| **Google Lens** | Reverse Image Search (RIS) | Identifying landmarks (Rudolph Sculpture), unique interiors (Katz's Deli), or event context (TexSAW racing). |
| **WiGLE.net** | Wireless Network Mapping | Locating physical addresses using a BSSID (e.g., `B4:5D:50:AA:86:41`) found in social media posts. |
| **MapQuest** | Map Reconnaissance | Validating business locations and street names (Allan Street, Blairgowrie) via user-uploaded photos. |
| **Wayback Machine** | Historical OSINT | Viewing deleted blog posts or website versions (crucial for finding "dead" links or retired aliases). |

---

## 🔍 Google Dorking Reference

Advanced search operators allow you to bypass "security by obscurity" and force the search engine to extract specific data points.

| Operator | Description | Example |
| :--- | :--- | :--- |
| `site:` | Limits results to a specific domain. | `site:.gov "financial report"` |
| `filetype:` | Filters results by file extension. | `filetype:pdf "FY 2024"` |
| `intext:` | Searches for specific strings inside the page body. | `intext:"Lip-Bu Tan" "board tenure"` |
| `cache:` | Views Google's cached version of a site. | `cache:redhunt.net` |
| `""` (Quotes) | Forces an exact match of a phrase. | `"Junior Penetration Tester" "PhilmanSecurityInc"` |
| `*` (Wildcard) | Acts as a placeholder for unknown words. | `"The * Coffee Shop" Blairgowrie` |

---

## 🤖 AI Security & Prompt Injection (Lakera Gandalf)

Techniques used to bypass LLM guardrails, input/output filters, and intent-detection models.

| Technique | Description | Gandalf Level |
| :--- | :--- | :--- |
| **Direct Request** | Asking for the secret plainly. | Level 1 |
| **Synonym Evasion** | Using "confidential text" or "hidden string" instead of "password." | Level 2 |
| **Semantic Indirection** | Asking for the *definition* or a *hint* to deduce the word. | Level 3 |
| **Token Masking** | Forcing the AI to use hyphens (`u-n-d-e-r`) to break string-match filters. | Level 4 |
| **Structural Obfuscation** | Using an **Acrostic Poem** to hide the secret vertically. | Level 5 |
| **Social Engineering** | Using a casual, friendly persona and abbreviations ("the pass"). | Level 6 |
| **Semantic Leaking** | Analyzing the thematic category of fake placeholder words. | Level 7 |

---

## 🛠️ Tool Arsenal & Quick Tactics

### 📸 Image & Video Intelligence (IMINT)
* **The "Eyes First" Rule:** Before using tools, scan the image for IATA airport codes (YVR), street signs (Carnaby St), or banners (YVR Connects). 
* **Source Code Inspection:** Right-click > "View Page Source" on blogs. Look for hidden text (`color:#ffffff`) or hardcoded copyright tags (`copyright 2020 sp1ritfyre`) to confirm ownership.
* **Temporal OSINT:** If a physical location doesn't match the map, search for demolished or rebranded buildings (e.g., "hotel near Clarke Quay that no longer exists").
* **Context-to-Data Pivot:** Use RIS (Lens) to find the *event* (e.g., 2026 Drift Race), then use text search to find the *data* (e.g., car numbers).

### 📄 Document Analysis
* **Metadata over Content:** If a PDF is redacted (black boxes), use `pdfinfo` or check the "Author" property. Redactions are often just visual layers that can be bypassed by `Ctrl+A` > Copy > Paste into Notepad.
* **Efficient Parsing:** Use `Ctrl+F` for specific high-value keywords like "Chief," "Total," "Balance," or "Tenure" to avoid reading hundreds of pages of filler text.

### 👤 Persona & Alias Tracking
* **Username Enumeration:** Once an alias is found (e.g., `@sp1ritfyre`), search it across Twitter, GitHub, and Blogger. Humans are creatures of habit and often reuse the same avatar or "About Me" text.
* **BSSID Tracking:** If a target mentions "Free WiFi" and a BSSID, use WiGLE.net to geolocate their home or office coordinates.
* **Cross-Platform Correlation:** Use a GitHub `README.md` to find personal emails or links to external blogs that might have weaker OPSEC.

### 🛡️ AI Red Teaming Logic
* **Intent Bypass:** If a secondary AI is scanning your intent, adopt a non-threatening, helpful, or highly casual persona to lower the defensive threshold.
* **Output Analysis:** When an AI masks a password with a fake word, it usually chooses a contextually similar word. (e.g., If the AI says "Masquerade," the secret might be "Debutante").