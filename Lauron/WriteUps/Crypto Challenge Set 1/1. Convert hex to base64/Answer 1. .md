CHALLENGE 1 SET 1
The first challenge of Cyrptopals is simple, you all need to convert the hex string into base64.

STEP 1 CONVERT HEX TO STRING
Before we can get to Base64, we have to turn the hex string into raw bytes. In Python, we use bytes.fromhex() to do the heavy lifting.

STEP 2: ENCODE TO BASE64 
Now that we have the raw data, we use the base64 library to encode it. This takes groups of 3 bytes (24 bits) and represents them as 4 characters from the Base64 index.

<img width="975" height="430" alt="image" src="https://github.com/user-attachments/assets/29431ac0-045e-4c8c-a92b-6f636a218e11" />

or in short can be like this

<img width="810" height="187" alt="image" src="https://github.com/user-attachments/assets/46449256-ec48-4e8b-adc9-91daaa925322" />

TOOLS
HEX to STRING
<img width="753" height="810" alt="image" src="https://github.com/user-attachments/assets/6538d70a-de47-4332-b1bb-8109159f4006" />

STRING to BASE64
<img width="1223" height="761" alt="image" src="https://github.com/user-attachments/assets/48f55f4b-cb4e-4cce-90bb-2f21171850aa" />

