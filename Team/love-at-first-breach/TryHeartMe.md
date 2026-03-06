# 📝 Challenge Write-up: TryHeartMe (Gift Shop)

| Attribute | Details |
|---|---|
| **Event** | TryHackMe - Love at First Breach |
| **Category** | Web / Authentication |
| **Difficulty** | Easy |

---

## 1. The Challenge Scenario
<img width="1919" height="868" alt="image" src="https://github.com/user-attachments/assets/c457a01e-430c-475e-b789-7057bc456e98" />
<img width="1919" height="843" alt="image" src="https://github.com/user-attachments/assets/f83ce937-c201-418e-b054-96807a8ab411" />

In this challenge, we are introduced to **TryHeartMe**, a Valentine's-themed online gift shop. The goal of the challenge is to purchase a special item called the **Hidden Valent Flag**.

Upon creating an account and accessing the store, we quickly notice two limitations:

- Our account starts with **0 credits**

- The **Hidden ValenFlag** item is not visible in the shop
<img width="1919" height="828" alt="image" src="https://github.com/user-attachments/assets/396a1baf-8d0c-466a-b159-13ff1703e48f" />

This suggests that the application is enforcing **access control and credit-based restrictions**. During further analysis, we discovered that the application uses **JSON Web Tokens (JWT)** stored in browser cookies to manage user sessions and store user information such as **credits** and **roles**.

The objective becomes clear: manipulate the JWT to gain enough privileges and credits to purchase the hidden flag.

---

## 2. The Step-by-Step Solution

### Step 1: Account Creation and Initial Reconnaissance

First, we registered a new account using a test email (e.g., `aa@gmail.com`) to gain access to the store.

After logging in, we observed the following:

- Account balance: **0 credits**
<img width="1918" height="841" alt="image" src="https://github.com/user-attachments/assets/8644a9ee-5550-432d-b7de-0501474637a9" />
- User role: **user**

With no available credits and no way to add funds, purchasing any item — especially the hidden flag — was impossible through normal means.

This indicated that the system likely relies on **client-side session data** that could potentially be manipulated.

---

### Step 2: Intercepting the JWT

Using **Burp Suite**, we intercepted the HTTP requests between the browser and the web server.

During inspection of the request headers, we discovered a cookie named:

```
tryheartme_jwt
```

This cookie contained a **JSON Web Token**, which appeared to store the user's session data.
<img width="1598" height="893" alt="image" src="https://github.com/user-attachments/assets/bfc2cd57-cbda-486f-bd47-2c4f22d32fee" />

---

### Step 3: Decoding the JWT

To analyze the token, we copied the JWT and pasted it into **https://jwt.io**.

After decoding the token, we observed the following payload:

```json
{
  "credits": 0,
  "role": "user"
}
```
<img width="651" height="421" alt="image" src="https://github.com/user-attachments/assets/bdd09a04-5a75-4ab1-9107-4bcdbcc46f85" />

This revealed that the application was storing **sensitive authorization data directly inside the JWT**, which raised a potential security issue.

---

### Step 4: Credit Manipulation

To bypass the credit restriction, we modified the token payload.

Steps performed:

1. Edited the payload in **JWT.io**
2. Changed the value:

```
"credits": 0
```

to

```
"credits": 10000
```
<img width="1351" height="806" alt="image" src="https://github.com/user-attachments/assets/104ddb01-5524-42c8-92b2-5cfded3d81dc" />

3. Generated the modified JWT
4. Replaced the original cookie in the browser using:

```
Developer Tools → Application → Cookies
```

After refreshing the page, the account balance updated to **10,000 credits**, confirming that the server was **trusting the client-side token without proper validation**.

---

### Step 5: Privilege Escalation

Despite having enough credits, the **Hidden Valent Flag** item was still not visible in the store.

This suggested that the item might be restricted to a higher privilege level, such as **admin users**.

To test this hypothesis, we modified the JWT payload again:

```
"role": "user"
```

changed to

```
"role": "admin"
```

After replacing the cookie with the modified token and refreshing the page, an **admin-only section** appeared in the shop.

---

### Step 6: Purchasing the Hidden Flag

With the **admin role** and **10,000 credits**, the restricted shop item became visible:

```
ValenFlag
Price: 777 credits
```

We successfully purchased the item.

After completing the transaction, the application redirected us to the **receipt page**, where the challenge flag was revealed.

---

## 3. The Findings

By exploiting insecure JWT implementation, we were able to perform:

- **Credit manipulation** by modifying the `credits` field
- **Privilege escalation** by changing the `role` from `user` to `admin`

This allowed full control over the user session without authentication checks on the server.

### Final Flag

```
THM{v4l3nt1n3_jwt_c00k13_t4mp3r_4dm1n_sh0p}
```

---

## 4. Conclusion

This challenge demonstrates the dangers of **trusting client-controlled data in authentication tokens**.

The application relied entirely on the information contained within the JWT without verifying its authenticity or validating the token against server-side data.

Key security lessons from this challenge include:

- **Always verify JWT signatures on the server side**
- **Never store sensitive authorization data (roles, credits, permissions) solely inside client tokens**
- **Implement proper backend authorization checks for sensitive actions**
- **Follow the Principle of Least Privilege**

Failing to enforce these practices allowed attackers to modify their own permissions and bypass application security controls, ultimately gaining unauthorized access to restricted functionality.

---
