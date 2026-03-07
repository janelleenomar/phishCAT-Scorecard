# 📝 Challenge Write-up: TryHeartMe (Gift Shop)

| Attribute | Details |
|---|---|
| **Event** | TryHackMe - Love at First Breach |
| **Category** | Web / Authentication |
| **Difficulty** | Easy |

---

## 1. The Challenge Scenario
The Love Letter Lock application is a private storage service where users can write and save Valentine's letters "for your eyes only". The challenge description, however, hints at insecurity with a suspicious question mark regarding the privacy of these letters.

Our objective is to exploit an Insecure Direct Object Reference (IDOR) vulnerability to access archived letters that do not belong to our account, specifically to find the one containing the flag.

<img width="975" height="730" alt="image" src="https://github.com/user-attachments/assets/e3cfc866-1a5f-4a6b-813e-3f2bc193ca99" />

---

## 2. The Step-by-Step Solution
Step 1: Initial Reconnaissance & Account Setup
After accessing the site, we create a test account (e.g., username: user) to understand how the application handles data. Once logged in, the dashboard shows a "tip" from Cupid: "Every love letter you get a unique number in the archive. Numbers make everything easier to find".
First create account
<img width="975" height="616" alt="image" src="https://github.com/user-attachments/assets/73cb0fbe-a77f-45aa-ae94-3cda8e39bb56" />

login your created account
<img width="975" height="613" alt="image" src="https://github.com/user-attachments/assets/24b68e9b-27ba-44c0-9f43-6f2be37de030" />

create message

<img width="948" height="450" alt="image" src="https://github.com/user-attachments/assets/cffc7acc-91ee-4992-9506-17cfeda7b147" />

Step 2: Identify the IDOR Vulnerability
To test how letters are retrieved, we write a "sample letter". After saving, we open the letter and observe the URL structure:
```
http://[TARGET_IP]/view_letter.php?id=3
```
Find the flag by change the last number 3 into 2
<img width="698" height="40" alt="image" src="https://github.com/user-attachments/assets/fb204cd3-c176-45d6-871f-28c613c5763c" />
And since we still havent find the code then change it to 1
<img width="813" height="362" alt="image" src="https://github.com/user-attachments/assets/44f85314-ea0b-4ba0-9631-d13ff54edf7a" />
And there it is.
<img width="838" height="417" alt="image" src="https://github.com/user-attachments/assets/11d2ba77-9c7c-4ad5-bb58-e1dab59d7409" />

3. The Findings
By manipulating the URL parameter, we successfully bypassed the "private" lock of the application.

IDOR Flag
```
THM{1D0R_L0V3_L3TT3R_EXPOSURE}
```

<img width="1919" height="910" alt="image" src="https://github.com/user-attachments/assets/fb5ef72b-40e7-4631-8240-98dfe9bd39b0" />

