# TryHackMe Write-up: Offensive Security Intro – FakeBank

## 1. Objective

The objective of this lab was to perform a basic **web application penetration test** against the FakeBank system in order to identify security weaknesses and exploit them to gain unauthorized functionality.

The exercise demonstrates a common web vulnerability: **Broken Access Control**, where sensitive application features are accessible without proper authentication.

---

## 2. Scenario

As part of a simulated penetration testing engagement, I was tasked with assessing the security of the **FakeBank** web application.

The goal was to investigate the system, identify weaknesses in the application's design, and exploit those weaknesses to manipulate account balances.

---

## 3. Technical Findings

| Vulnerability | Severity | Description |
|---|---|---|
| **Broken Access Control** | **Critical** | Administrative functionality is accessible without authentication through direct URL access. |
| **Security Through Obscurity** | **High** | Sensitive pages were hidden from the interface but not protected by authentication checks. |

---

## 4. Step-by-Step Exploitation Process

### Phase 1 – Information Gathering

The investigation began by reviewing the **FakeBank account dashboard**.

One account stood out:

- **Account ID:** `8881`
- **Account Owner:** Mrs. G. Benjamin
- **Balance:** `-$1,232.32`

This negative balance suggested that the lab might require manipulating the account balance to complete the challenge.
<img width="956" height="878" alt="image" src="https://github.com/user-attachments/assets/1b4776a2-3d2a-4add-8833-cb2874096053" />

---

### Phase 2 – Hidden Endpoint Discovery

Using directory discovery techniques and manual URL exploration, a hidden administrative endpoint was discovered:

```
/bank-transfer
```

This page was not accessible through the normal user interface, suggesting that it was intended for internal or administrative use.

<img width="1914" height="946" alt="image" src="https://github.com/user-attachments/assets/95b2174e-e211-4aa7-8aee-ffbcf8713188" />

---

### Phase 3 – Vulnerability Validation

By manually navigating to the discovered endpoint in the browser:

```
http://<target>/bank-transfer
```

The application immediately displayed a **bank transfer form** without requiring authentication.

This confirmed the presence of a **Broken Access Control vulnerability**, as sensitive financial functionality was exposed to unauthorized users.

<img width="1919" height="882" alt="image" src="https://github.com/user-attachments/assets/26454137-1d88-446a-b9ae-019d4ba13d55" />

---

### Phase 4 – Exploitation

Using the exposed transfer form, an unauthorized transaction was performed.

Transfer parameters:

- **Destination Account:** `8881`
- **Transfer Amount:** `$2000`

After submitting the transaction, the main dashboard reflected the updated account balance.

The balance for account **8881** was successfully corrected, confirming the vulnerability could be used to manipulate financial data.
<img width="1919" height="879" alt="image" src="https://github.com/user-attachments/assets/79852971-2df3-458e-93b0-29891987f6cb" />
<img width="955" height="885" alt="image" src="https://github.com/user-attachments/assets/8cf2b44f-9c04-4c74-8b25-6a21542a274f" />

---

## 5. Remediation Recommendations

To prevent this vulnerability in a real-world environment, the following security measures should be implemented:

### 1. Enforce Server-Side Authentication

All sensitive endpoints must verify authentication and authorization **on the server side**, not just through hidden links.

### 2. Implement Proper Access Control

Administrative functionality should only be accessible to authorized users with the appropriate roles.

### 3. Security Logging and Monitoring

Financial operations such as account transfers should trigger **audit logs and SIEM alerts** to detect suspicious activity.

### 4. Principle of Least Privilege

Users should only be granted access to features necessary for their role.

---

## 6. Lessons Learned

This lab highlights a fundamental security principle:

> **Hiding functionality is not the same as securing it.**

Key takeaways:

- Sensitive endpoints must always enforce authentication.
- Attackers frequently discover hidden functionality through **directory enumeration**.
- Broken access control is one of the **most common and dangerous web vulnerabilities**.

---

## 7. Final Proof of Compromise

**System Status:** HACKED  
**Flag:** `BANK-HACKED`

---

## 8. Skills Practiced

- Web application enumeration
- Identifying broken access control vulnerabilities
- Manual URL manipulation
- Basic penetration testing workflow
- Security reporting and documentation
