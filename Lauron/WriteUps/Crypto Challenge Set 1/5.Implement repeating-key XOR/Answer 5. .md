CHALLENGE 5 SET 1

STEP 1 – Understand the Approach
In the previous Challenges, we dealt with a single-character key. This time, the challenge is more complex because the key is full word “ICE”.
Unlike the single-byte version, we cant just use one number for the whole message. We have to “rotate” the key:
This 1st letter of the poem is XPR’d with I.
The 2nd letter is XOR’d with C.
The 3rd is with E and last goes back to I and repeats the cycle.

STEP 2 – The Wrapping Logic (dunno why I name it like this it’s just sound cool to me…)
I came up with this idea about “what if I use the index of the text to pick the key?” because I noticed that the plaintext was more longer thatn the 3-letter key”ICE”. To make the key reapet forever without crashing the program, I used the modulo operator because I noticed people uses them so I just randomly used it without knowin. But, I dig deeper to it and realize that this acts like a “loop-back” button. For example, when the counterreaches 3, 3 % 3 becomes 0, taking us right back to the letter I.

STEP 3 – Implementation & Results
  I notice most who have solve the challenge uses repeating_key_xor so I search it online about what is it and finds the reason/use of it and try to understand why it is necessary. The repeating_key_xor is a function designed to handle cases where the key is shorter than the message. Its job is to recycle the key characters (I, C and E) over and over until every letter of the plaintext has been encrypted.
I ened up writing a python script that uses bytearray to build the result piece by piece. I also made sure to use .encode() because we cant perform XOR math on plaintext we must have to convert them into their numeric byte values first.

In my code I put ICE as my key and the stanza into the script, and it successfully generated the long hex string required by the challenge.

<img width="975" height="431" alt="image" src="https://github.com/user-attachments/assets/73afaf73-0245-4eee-8ae6-6b5d18bc4551" />

