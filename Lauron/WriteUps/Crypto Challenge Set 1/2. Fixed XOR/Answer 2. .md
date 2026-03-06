CHALLENGE 2 SET 1 
The second challenge requires us to take two equal-length hex strings and XOR them against each other. This is the "Hello World" of cryptography operations.

STEP 1: HEX TO BYTES
Just like in the first challenge, we can't perform math directly on a hex string. We have to convert both inputs into raw bytes first so Python can work with the individual bits.

STEP 2: THE BITWISE XOR The "Fixed XOR" means we pair up the bytes: b1[0] with b2[0], b1[1] with b2[1], and so on. In Python, the zip() function is perfect for this because it lets us iterate through both byte objects simultaneously.

<img width="809" height="264" alt="image" src="https://github.com/user-attachments/assets/4d0cfefa-707b-4d5c-9cff-01ef0d101670" />

or can be like this

<img width="811" height="238" alt="image" src="https://github.com/user-attachments/assets/85b8ec3c-7062-4a76-9f52-085be4beb722" />
