# 📝 Challenge Write-up: When Hearts Collide

| Attribute | Details |
| :--- | :--- |
| **Event** | TryHackMe — When Hearts Collide |
| **Category** | Cryptography / Web |
| **Difficulty** | Easy |
| **Target URL** | `https://tryhackme.com/room/lafb2026e1` |

---

## 1. The Challenge Scenario

We were presented with an MD5 hash collision puzzle themed around dog pictures. The room description hinted to us that two dog pictures share the same MD5 hash — a deliberate pointer to the concept of hash collisions, where two different files with different content can produce the exact same hash digest.

We noted that a hash collision occurs when two distinct inputs to a hash function yield the same output. While collisions are theoretically possible with any hash function, we knew that MD5 is particularly vulnerable because researchers have demonstrated practical, fast methods to engineer them. We identified that this challenge leverages that weakness to simulate a real-world scenario where trust in MD5-based integrity checks is exploited.

---

## 2. The Step-by-Step Solution

We determined that our solution required generating two image files that share an identical MD5 hash value, then uploading them both to the challenge application to satisfy its verification check.

### Step 1: Navigate to the Working Directory

We started by navigating into the Pictures directory where the base image was stored:

```bash
cd Pictures
```

### Step 2: Pull the fastcoll Docker Image

We chose `fastcoll`, a well-known MD5 collision generator, and pulled it using Docker to avoid any local dependency issues:

```bash
docker pull brimstone/fastcoll
```

### Step 3: Generate the Colliding Files

Using the provided base image (`thm-ab-bg-1803.png`) as a prefix, we ran the fastcoll tool to produce two output files — `twin_a.jpg` and `twin_b.jpg` — that would share the same MD5 hash:

```bash
docker run --rm -v $PWD:/work -w /work \
  brimstone/fastcoll --prefixfile thm-ab-bg-1803.png \
  -o twin_a.jpg twin_b.jpg
```
![LoveNote Challenge Description](images/when-hearts-collide/commandline.webp)
After execution, we confirmed that both files had identical MD5 digests despite being different files by running:

```bash
md5sum twin_a.jpg twin_b.jpg
```

### Step 4: Upload Both Files to the Application

We navigated to the challenge web application and uploaded both generated files one by one. The application verified that the two uploaded files shared the same MD5 hash — and since our collision-generated pair satisfied this condition, it accepted them and revealed the flag.

---

## 3. The Findings

By exploiting the mathematical weakness of the MD5 hashing algorithm, we successfully engineered two distinct image files with an identical hash digest. Uploading these to the challenge application allowed us to bypass its integrity check, revealing the flag:

```
THM{hash_puppies_4_all}
```

**🏁 Flag:** `THM{hash_puppies_4_all}`

Through this process, we made the following key technical observations:

- MD5 is cryptographically broken and must not be used for integrity or security-critical checks.
- We found that the `fastcoll` tool can generate MD5 collisions in seconds on modern hardware.
- By using a shared prefix (the original image), we ensured both output files appeared visually similar, demonstrating how stealthy this attack can be in real-world scenarios.
- We confirmed that any system relying solely on MD5 to distinguish or verify files is trivially bypassable using this technique.

---

## 4. Conclusion

Through this challenge, we gained hands-on experience with a real-world cryptographic weakness. While MD5 may still appear in legacy systems and checksums, we were reminded that it has been considered cryptographically broken since the early 2000s, with practical collision attacks publicly demonstrated.

The core lesson we took away: algorithm strength matters just as much as implementation. A system can use hashing correctly in design, but if it selects a broken algorithm like MD5, the entire trust model collapses. We recommend using collision-resistant alternatives such as SHA-256 or SHA-3 for any security-sensitive hash verification.

*As the flag itself reminds us — hash puppies are for all. 🐶*
