CHALLENGE 8 SET 1
So for this one, I had to find which hex string in a giant file was encrypted using AES in ECB mode. I started by looking online for topics related to detecting AES and ECB mode to figure out how people actually spot it
STEP 1 – THE DETECION STRATEGY
While researching, I realized the biggest weakness of ECB: it is deterministic. This means if you have the same 16-byte block of data, it will always produce the exact same ciphertext. If a message has patterns, the encrypted version will have those same patterns. I found a specific logic online for a count_repeated_blocks function and realized it was exactly what I needed to solve this.

STEP 2 – IMPLEMENTATION
I took that logic and implemented it into my script to act as a duplicate detector. Here is how I understood what the function was actually doing:
<img width="680" height="152" alt="image" src="https://github.com/user-attachments/assets/40dcf5c3-a32f-4ca9-9442-7abf94f62864" />

STEP 3 – SCANNING THE FILE
Next I opened my file8.txt and let it loop through every line. I wasn’t just looking at randomhex; I was looking for the line with the highest “repeat” score. Then I detected ECB line and I put the code that would print how much the blocks repeated.

<img width="859" height="603" alt="image" src="https://github.com/user-attachments/assets/be47657a-c361-4b65-9b22-a708b107576d" />
