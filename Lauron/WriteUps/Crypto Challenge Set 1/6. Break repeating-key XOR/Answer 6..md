CHALLENGE 6 SET 1

This part really is the hardest it took me almost a week to be able to answer this because its really hard I had to dig deeper the codes and search for every meaning about it and thanks to this youtube tutorial from NCC group https://www.youtube.com/watch?v=YTA6sXNgMRE&list=PLWvDpnCcem1P6i8pZm2x7KHp5iaxwrK_P&index=6 who was my biggest help. I finally got through it. I watched and rewatched his guide for a couple of hours just to know how to solve this challenge.

STEP 1 – Getting the Data Ready
The first thing that tripped me up was just getting the file into python. I realized that instead of copy and paste it, you can just copy the file cryptopals provided to me. I saved mine in my downloads and used this part here to pull it into the script:
<img width="949" height="177" alt="image" src="https://github.com/user-attachments/assets/ba81e9a4-903d-446b-834b-c3e4f3856bdc" />

I used import base64.b64decode because the data is “base64’d” after being encrypted. We have to decode that first so that the XOR math works.
STEP 2 – The Wokka Wokka Qualifying Test
Before I could break the big file, I had to make sure my Hamming Distance function was actually working. This is the part that counts how many bits are different between two strings. I used bin(x ^ y).count("1") to count those bits. The challenge gives you a test case: the distance between “this is a test” and “wokka wokka!!!” must be exactly 37. When my code printed 37, I knew I was ready.

<img width="1041" height="400" alt="image" src="https://github.com/user-attachments/assets/d7d3e0a5-289c-4d20-abab-ab91bb6b2334" />

Step 3 – Guessing the Key Size
Next, I had to find the length of the key. I tried every keysize from 2 to 40. I took chunks of the ciphertext and measured the Hamming distance between them, then "normalized" it by dividing by the keysize. The smallest normalized distance is usually the right one. My script told me: Best keysize: 29. 

<img width="845" height="414" alt="image" src="https://github.com/user-attachments/assets/841047c5-fc01-4a07-b6a4-9475a726df7a" />

STEP 4 – The Transposing Trick
This was the most confusing part. Once I had a keysize of 29, I had to transpose the blocks. I made a new block out of the 1st byte of every 29-byte chunk, then another for the 2nd byte, and so on so forth. By doing this, each of the 29 blocks became a single-Byte XOR problem. This is similar to what I did in challenge 3 and 4.
STEP 5 The Last
I wrote an english_score function tolook for common letters like etaoin. I ran it on each transposed block to find the best key for that position. When I put all 29 characters together, the key appeared:
Recovered key: b’Terminator X: Bring the noise’
When I finally decrypted it, the lyrics to the “Play That Funky Music” by Vanilla Ice popped out. It’s a “Crypto 101” thing, but actually doing it feels awesome because morepeople “know how” to break it than can actually write the code. But after almost a week of digging I  finally did it.

<img width="583" height="644" alt="image" src="https://github.com/user-attachments/assets/1669553c-7715-4337-a6b7-de63591ec71d" />

Decrypted Text:
<img width="474" height="804" alt="image" src="https://github.com/user-attachments/assets/624b67e9-2e71-4d9c-aa87-b9e9c6dcc5d6" /> <img width="572" height="818" alt="image" src="https://github.com/user-attachments/assets/141b8347-98d2-4e34-bc85-a94e6ff4e069" />

