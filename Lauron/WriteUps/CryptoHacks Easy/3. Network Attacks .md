Problem:
Many cybersecurity challenges are dynamic, requiring direct interaction with a remote server. This setup simulates real-world scenarios where you might perform Man-in-the-Middle (MITM) attacks or exploit vulnerable network services.

To ensure a structured exchange of data, these interactive servers communicate using JSON (JavaScript Object Notation) objects. Our goal is to establish a socket connection and send a specific data packet to retrieve the flag.
<img width="1519" height="621" alt="image" src="https://github.com/user-attachments/assets/98a71e55-adb4-40f7-a051-fec22ffb8b81" />
Step 1: Identify the Connection Parameters
The challenge provides a specific endpoint for the interaction:

Host: socket.cryptohack.org

Port: 11112

You can manually verify the connection using Netcat:
```
nc socket.cryptohack.org 11112
```
Understand the Payload Requirement
The server expects a JSON object. JSON is a key-value format. We are required to send a "buy" request for the flag.
```
{ "buy": "flag" }
```
While manual interaction is possible, using Python's telnetlib (or the more modern pwntools) allows for automation in future, more complex challenges.

Solution:
<img width="523" height="815" alt="image" src="https://github.com/user-attachments/assets/ef005d34-a933-443d-bafa-7fe963c3de51" />
