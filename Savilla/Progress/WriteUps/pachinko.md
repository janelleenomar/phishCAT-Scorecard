## Challenge Write-Up — Pachinko
---
## 📌 Challenge Overview
| Field                 | Information                                                   |
| :-------------------- | :------------------------------------------------------------ |
| **Competition**       | picoCTF 2025                                                  |
| **Category**          | Web Exploitation                                              |
| **Difficulty**        | Medium                                                        |
| **Objective**         | Fuzz the NAND circuit API to find the correct node values and retrieve the flag |
---
## Initial Analysis
I was given a web app with a **NAND Simulator** — a circuit builder where I could add nodes, connect them, and submit the circuit for checking. The challenge had two flags total, but this writeup covers the first one. My plan was to:
* Play around with the circuit builder to understand how it works
* Intercept the request using Burp Suite to see what data gets sent
* Fuzz the node values to find the one that gives a successful response

---
## 🔎 Step 1 — Play With the NAND Simulator
I opened the challenge site and saw an interactive circuit builder. I connected a few random nodes — for example: `1 → 5`, `1 → 6`, `6 → 2` — and clicked **Submit Circuit**.

A popup appeared saying the result was **"Wrong"**. That was expected since I just guessed randomly. But it told me the server was checking my input and giving feedback.

---
## Step 2 — Try Reflected XSS (Dead End)
I also tried injecting a simple XSS payload into the URL just to see what would happen:

```
<script>alert(1)</script>
```

Nothing happened. XSS was not the way in, so I moved on.

---
## Step 3 — Intercept the Request With Burp Suite
I turned on **Intercept** in Burp Suite and clicked **Submit Circuit** again. I caught a POST request being sent to `/check`:

```
POST /check HTTP/1.1
Host: activist-birds.picoctf.net:56704
Content-Type: application/json
```

```json
{
  "circuit": [
    {"input1": 5, "input2": 6, "output": 1},
    {"input1": 6, "input2": 7, "output": 2}
  ]
}
```

This told me the server expected a JSON object describing the circuit — each node had an `input1`, `input2`, and `output` field. All values were just numbers.

---
## Step 4 — Fuzz the Node IDs Using Burp Intruder
Since the values were just numbers, I figured I could brute-force them to find the right combination. I sent the request to **Intruder** and set it up like this:

* **Attack Type:** Sniper
* **Payload:** Numbers from 0 to 100
* **Target:** Each position — `input1`, `input2`, and `output`

I started the attack and let Burp try all the numbers automatically.

---
## Step 5 — Find the Successful Response
As the attack ran, I watched the responses. Most of them looked the same, but one stood out:

* It had a **Status Code 200**
* It had a **longer response length** than the others

I clicked on that response and saw:

```json
{
  "status": "success",
  "flag": "picoCTF{p4ch1nk0_f146_0n3_e947b9d7}"
}
```

---
## 🏁 Flag
```text
picoCTF{p4ch1nk0_f146_0n3_e947b9d7}
```
Success.

---
## 🔬 Technical Insight
This challenge showed me how fuzzing can break a web app even when the logic seems complex:

### ❌ Not Protecting the API From Brute-Force
The server accepted any combination of numbers as a circuit input. There was no rate-limiting or lockout to stop me from trying hundreds of combinations automatically. By using Burp Intruder to try numbers 0 to 100, I found the correct node IDs without understanding the actual circuit logic at all.

The key signs to watch for during fuzzing:
* A different **status code** from the rest
* A longer or shorter **response length**
* A different message in the **response body**

Tools I used:
* Burp Suite Intruder (Sniper mode) — to automate the number guessing
* Burp Suite Repeater — to check individual responses

---
## 🎯 Key Lesson
This challenge follows a simple pattern:
1. Play with the app manually to understand what it does
2. Intercept the request with Burp Suite to see the data format
3. Identify values that can be brute-forced (like node IDs)
4. Set up Burp Intruder with a number list and run the attack
5. Look for the response that is different — that one has the flag

---
## 🧩 Final Reflection
"Pachinko" taught me an important lesson:

**Even a complex-looking interface can have a simple vulnerability underneath.**

I did not need to understand how NAND circuits work to solve this. I just needed to notice that the circuit values were plain numbers and that the server had no protection against trying them all. Rate-limiting and input validation on the server side would have stopped this attack completely.

---
