CHALLEGNE 3 SET 1	
This challenge says that the string was XOR’d with a single character and that our goal is to find the key and decrypt the message.
Step 1 – Identify the Encoding
The ciphertext is written in hexadecimalformat, meaning each pair of characters represents one byte. Before we perform any cryptographicoperation, the hex data must first be converted into its raw bytes representation.

<img width="945" height="425" alt="image" src="https://github.com/user-attachments/assets/f4031f64-b5d7-499d-b5e6-e310c73d2dcd" />


I used this website called CyberChef in order to solvethe challenge faster, in CyberChef I used 2 operations the first is “From Hex” and after the ciphertext is decoded into raw bytes it can now be processed by other operations
STEP 2 – Brute Force the XOR Key

Then I used the 2nd operation called “XOR Brute Force” since the problem specifies that the ciphertext was encrypted with a single-byte XORkey. The correct key must be one of the 256 possible bytes values (0-255). Instead testing each key manually, CyberChef provides an operation that can automatically try all possibilities.
STEP 3 – Identify Readable English Output
After applying the “XOR Brute Force” the tool “CyberChef” generates multiple outputs. Hence, I manually check and read all outputs and found one output clearly contains redable English text:

<img width="822" height="67" alt="image" src="https://github.com/user-attachments/assets/3d1a30e4-8adc-4388-bdcc-759f6c57c465" />

And that’s the answer…
