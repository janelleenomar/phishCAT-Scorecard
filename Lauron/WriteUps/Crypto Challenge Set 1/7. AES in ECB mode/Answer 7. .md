CHALLENGE 7 SET 1
The challenge 7 is about AES(Advance Encryption Standard) in ECB(ElectronicCodebook) mode. The challenge provides a file that was Base64 encoded and encrypted with the 128-bit key: “YELLOW SUBMARINE”

STEP 1 – SETTING UP THE LIBRARY
In here, I was wondering why I kept getting this message “from Crypto.Cipher import AES” ModuleNotFoundError: No module named 'Crypto' 

<img width="719" height="59" alt="image" src="https://github.com/user-attachments/assets/49138a0d-5594-4fb7-b922-528a3366ea66" />

Then I realize that the import AES is not package when you download python so you must first install the AES library to work in Python environment. So, first I need to install pycryptodome since I haven’t installed it yet then now itsfixed, 

<img width="771" height="651" alt="image" src="https://github.com/user-attachments/assets/e7734cf6-30ed-4805-943b-54c3e07a18b7" />

I used this code to get started,

Import sys and from Crypto.Cipher importAES
And double check if I already had AES by “Print(“AES works”)”

<img width="552" height="92" alt="image" src="https://github.com/user-attachments/assets/2cbaadaa-aac4-4f37-96eb-c21f3d89b0ff" />

STEP 2 – HANDLING THE DATA
Just like the earlier challenges, the input is a file. I realized I had to clean itup before the decryption work. First I  open the 7.txt file and used .replace(“\n”, “”) to remove all the newlines. Then, I used base64.b64decode(data) toturn that string intro raw bytes.

<img width="730" height="58" alt="image" src="https://github.com/user-attachments/assets/fd0abea3-dbaf-4076-a2c8-5bde562cf3cb" />

STEP 3 – DECRYPTION
Since AES is a standard algorithm, I didn’t have to buildthe math from scratch. I just used the library:
The key, The cypher and The action.

<img width="975" height="165" alt="image" src="https://github.com/user-attachments/assets/14e918b9-4227-4395-aaf2-514be77dbb17" />

OUTPUT of challenge 7 is similar to Challenge no.6

<img width="485" height="763" alt="image" src="https://github.com/user-attachments/assets/bb0f7f51-c006-461f-9be9-dec425022829" />

<img width="555" height="760" alt="image" src="https://github.com/user-attachments/assets/ce60e0b1-21fd-4dc6-8b97-fc14e2be8c83" />

