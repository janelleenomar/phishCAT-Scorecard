# 📝 Challenge Write-up: Introduction to OSINT Capstone

| Attribute | Details |
| :--- | :--- |
| **Event** | Security Blue Team |
| **Category** | OSINT |
| **Difficulty** | Medium |
| **Target** | `@sp1ritfyre` |

## 1. The Challenge Scenario
This capstone challenge required taking on the role of an OSINT analyst for a law enforcement organization. The objective was to track a person-of-interest associated with a hacking group that recently compromised a Managed Service Provider (MSP). Armed with a single starting point—a Twitter handle (`@sp1ritfyre`)—the goal was to build a comprehensive profile of the hacker, uncovering their real name, location, employment details, and digital footprint.

## 2. The Step-by-Step Solution
To solve this, the investigation moved from social media enumeration to metadata inspection, eventually linking the target's aliases to personal blogs containing severe OPSEC failures.

**Step 1: The Initial Pivot (Twitter)**
The investigation started with the given Twitter handle: `@sp1ritfyre`. Reviewing the profile revealed a specific avatar (a red lightbulb) used by the threat actor. 

**Step 2: Uncovering the Personal Website**
By conducting broader web searches for the alias `sp1ritfyre`, a standalone website was discovered. Inspecting the page's footer and source code revealed a hardcoded copyright tag (`copyright 2020 sp1ritfyre`), confirming the domain belonged to our target. The URL of this site is **https://redhunt.net**.

**Step 3: Finding the Blog & Personal Profile (Blogger)**
Continuing to pivot on the alias led to the discovery of Blogger/Blogspot profiles. The target maintained blogs, specifically **https://sammiewoodsec.blogspot.com/** and **https://sp1ritfyrehackerstories.blogspot.com/**. 

Checking the profile section on Blogger cracked the case wide open. The user explicitly listed their personal details:
* **First Name:** Sammie (Sam)
* **Last Name:** Woods
* **Age:** 23
* **Location:** United Kingdom
* **Interests:** Security, Photography, Gaming, Camping, Malware analysis

**Step 4: Locating the Email Address**
While on the Blogger profile, clicking the "Contact Me" section revealed the target's personal email address, which they failed to obfuscate: **d1ved33p@gmail.com**.

**Step 5: Identifying the Employer**
To find the employment information, I dug into the actual blog archives. In a post dated June 2019 titled "How I got into Cyber Security," Sammie discusses their professional life. The post reveals that they work for **PhilmanSecurityInc** and currently hold the position of **Junior Penetration Tester**.

## 3. The Findings
By chaining together the alias, source code copyrights, and careless profile details on Blogger, all 10 challenge questions were successfully answered:

* **[1] What is the hacker's first name?** `Sammie`
* **[2] What is the hacker's last name?** `Woods`
* **[3] What is the hacker's age?** `23`
* **[4] What country does the hacker live in?** `United Kingdom`
* **[5] What are some of the hacker's interests?** `Security, Photography, Gaming, Camping, Malware analysis`
* **[6] What company does the hacker work for?** `PhilmanSecurityInc`
* **[7] What is the hacker's position within the company?** `Junior Penetration Tester`
* **[8] What is the full url of the website owned by the hacker?** `https://redhunt.net`
* **[9] List any full URLs of websites not owned, but used by the hacker (Blogs only):** `https://sammiewoodsec.blogspot.com/` and `https://sp1ritfyrehackerstories.blogspot.com/`
* **[10] What email address has been used by the hacker?** `d1ved33p@gmail.com`

## 4. Conclusion
This capstone challenge effectively demonstrated the power of username enumeration and digital footprinting. A single Twitter handle was enough to uncover a personal website via copyright metadata, which then linked to a Blogger profile. The target's failure to maintain Operational Security (OPSEC) on their blog—openly listing their full name, age, email, and exact job title—allowed for the complete deanonymization of the threat actor.
