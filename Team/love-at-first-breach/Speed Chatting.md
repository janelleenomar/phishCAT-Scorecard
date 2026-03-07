# 📝 Challenge Write-up: TryHeartMe (Gift Shop)

| Attribute | Details |
|---|---|
| **Event** | TryHackMe - Love at First Breach |
| **Category** | Web / Authentication |
| **Difficulty** | Easy |

---

## 1. The Challenge Scenario
his challenge features Speed Chatter, a messaging platform that allows users to communicate and customize their profiles. The platform includes a profile picture upload feature that, if not properly secured, can lead to Remote Code Execution (RCE).

Our objective is to exploit the file upload vulnerability to gain a reverse shell and retrieve the hidden flag:

Root Flag: THM{R3v3rs3_Sh3ll_L0v3_C0nn3ct10ns}

By uploading a malicious Python script, we aim to intercept the server's execution flow and establish a direct connection back to our attacker machine.
<img width="975" height="719" alt="image" src="https://github.com/user-attachments/assets/26858756-b145-44f6-8a14-325661c14db7" />

---

## 2. The Step-by-Step Solution
Step 1: Initial Reconnaissance
After navigating to the Speed Chatter platform, we analyze the technology stack. Using tools like Wappalyzer, we identify that the backend is running on Python using the Flask framework.
<img width="442" height="56" alt="image" src="https://github.com/user-attachments/assets/7e969a85-5cf7-4ed0-b1a8-e68cb96fda85" />

We identify a profile picture upload tool as the primary entry point. In Flask applications, improper handling of uploaded files can often allow an attacker to upload and execute scripts.

---

Step 2: Preparing the Reverse Shell Script
Create the Script: Write or obtain a Python reverse shell script.
Configure IP and Port: Open the script (e.g., using nano app.py) and replace the placeholder IP with your Attacker IP (the VPN or TryHackMe Kali IP) and set the listening port to 4444.
Save the File: Save the script as app.py.
<img width="973" height="447" alt="image" src="https://github.com/user-attachments/assets/b514d3a1-0872-4ab6-b859-eb8c148be4a9" />

Step 3: Set Up the Listener
•	Start Netcat: On your attacker machine, open a terminal and start a listener to catch the incoming connection: nc -lnvp 4444.
```
nc -lnvp 4444
```

Step 4: Execute the Exploit
•	Upload the Payload: Go to the website's upload tool, select your app.py file, and click the Upload button.
•	Trigger the Shell: Once the file is uploaded/processed by the server, your Netcat listener will receive a connection, giving you a terminal inside the target machine.


Step 5: Retrieve the Flag
•	List Directory: Type ls to view the files in the current directory.
•	Read the Flag: Locate flag.txt and use the cat command to display the flag: cat flag.txt.
```
cat flag.txt
```

T<img width="975" height="463" alt="image" src="https://github.com/user-attachments/assets/8e4b8157-e9d5-4054-8afd-403d74e9d3c3" />
