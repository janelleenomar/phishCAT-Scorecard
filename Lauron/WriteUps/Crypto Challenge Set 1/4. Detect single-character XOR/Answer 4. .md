CHALLEGNE 4 Set 1

In this challenge, we are given a file containing many 60-character hex strings, with each line representing a different cypher text.
The challenge states that among 60 character hex strings there is only 1 that was encrypted using a single character XOR cipher, similar to challenge 3. Our task here is to identify which line contains the encrypted message and decrypt it.
STEP 1 – Understand the Approach
Since we have already solved Challenge3, we now know how a single-byte XOR cipher works.
I tried my best solving this using the cyberchef tool by using the same method to what I did for the challenge 3, but the methos turned out to be helpless.
Then I came up to this idea “what if I will put all the string inside a data variable?”
I realized that if I could group all the hex strings together into one block of text in python, I wouln’t have to stay stuck in a browser tool. I could just tell the code to “look for something” for me.

STEP 2 – Writing the “Searcher”
I looked for guidance online about codes and etc to see how to handle a big block of text like that. Until I stumbled upon by using .splitlines(), I could turn that big chunk of data into a list.

Once the data was in a list, I could create a loop. Think of it like a metal detector the code “scans” the first line, then the second, third and so on searching for that one English hidden message that took me so much time.

STEP 3 – The Scoring Breakthrough
The biggest challenge was telling the computer what “English” looks like. So I look for it online and saw that you can use scoring function and soi did, I Used scoring function that looks for the most common letters like the, spaces, t and so on.

Instead of me looking at the screen and guessing it, I let the math do the work by using allof my gathered resources(knowledge from different ideas). The line that got the highest “score” was the winner
<img width="946" height="592" alt="image" src="https://github.com/user-attachments/assets/b807f004-a20f-4da5-97de-74a780cc98db" />
As shown in the image, the script successfully identified the one line of English text buried in the file
The decrypted message was “Now that the party is jumping”
key found “53”
