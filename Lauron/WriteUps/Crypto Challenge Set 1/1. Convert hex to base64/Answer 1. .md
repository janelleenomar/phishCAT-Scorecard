CHALLENGE 1 SET 1
The first challenge of Cyrptopals is simple, you all need to convert the hex string into base64, you can use any tools for this one but i choose python because I want to practice it.

STEP 1 CONVERT HEX TO STRING
Before we can get to Base64, we have to turn the hex string into raw bytes. In Python, we use bytes.fromhex() to do the heavy lifting.

STEP 2: ENCODE TO BASE64 
Now that we have the raw data, we use the base64 library to encode it. This takes groups of 3 bytes (24 bits) and represents them as 4 characters from the Base64 index.

<img width="975" height="430" alt="image" src="https://github.com/user-attachments/assets/29431ac0-045e-4c8c-a92b-6f636a218e11" />

or in short can be like this

<img width="810" height="187" alt="image" src="https://github.com/user-attachments/assets/46449256-ec48-4e8b-adc9-91daaa925322" />
