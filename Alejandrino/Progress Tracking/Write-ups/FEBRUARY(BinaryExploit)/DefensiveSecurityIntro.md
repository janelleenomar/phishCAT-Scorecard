# TryHackMe: Defensive Security Intro – FakeBank

## 1. Objective

The goal of this lab was to investigate a security alert triggered in the **FakeBank monitoring system** and take defensive action to protect the bank’s infrastructure.

The task involved identifying suspicious activity through the **SIEM dashboard**, analyzing the attack behavior, and implementing mitigation steps to stop the attacker.

---

## 2. Scenario

As a member of the **FakeBank Defensive Security Team**, I received an alert indicating suspicious web activity targeting sensitive endpoints. The alert suggested a potential **Web Discovery Attack**, where an attacker attempts to locate hidden or administrative web pages.

My responsibility was to analyze the alert and respond appropriately to secure the system.

---

## 3. Incident Details

The SIEM system reported the following information:

- **Event ID:** `SEC-000001`
- **Attack Type:** Web Directory Discovery
- **Source IP Address:** `32.122.195.63`
- **Attack Duration:** 16 minutes and 32 seconds
- **Total Requests Attempted:** 31 URLs

This pattern indicated that an automated script or scanning tool was attempting to discover hidden directories or administrative endpoints on the bank’s web server.

---

## 4. Investigation Process

Using the SIEM interface, I performed the following analysis steps:

1. **Alert Review**  
   The SIEM flagged an abnormal number of requests targeting restricted directories.

2. **Traffic Analysis**  
   The attacker repeatedly attempted to access multiple possible administrative paths, indicating the use of automated enumeration tools.

3. **Threat Identification**  
   The pattern of requests confirmed a **Web Discovery Attack**, where attackers try to uncover hidden resources that may contain sensitive functionality.

---

## 5. Mitigation & Response

To prevent further exploitation, the following defensive actions were taken:

- **IP Address Blocking**  
  The attacking IP (`32.122.195.63`) was added to the blocklist to stop additional requests.

- **Access Protection**  
  Administrative endpoints were reviewed and secured to ensure unauthorized access could not occur.

- **Incident Closure**  
  After confirming the attack had stopped, the investigation status was marked as **Completed**.

---

## 6. Key Security Concepts

### SIEM (Security Information and Event Management)

A SIEM system aggregates and analyzes logs from multiple sources to detect suspicious activity in real time.

### Web Directory Discovery

An attack technique where automated tools attempt to discover hidden directories or pages on a web server.

### Defensive Response

Security teams must quickly analyze alerts, identify malicious activity, and apply mitigation strategies to prevent compromise.

---

## 7. Reflection & Lessons Learned

This lab demonstrated how defensive security teams monitor and respond to potential threats in real time.

Key takeaways include:

- **Importance of Centralized Logging**  
  A SIEM provides visibility across systems and helps detect abnormal behavior early.

- **Behavior-Based Detection**  
  Patterns such as multiple requests to sensitive directories can indicate automated scanning.

- **Rapid Mitigation**  
  Blocking malicious IP addresses and securing endpoints are critical steps in stopping ongoing attacks.

This exercise provided insight into how **Blue Team security analysts monitor, investigate, and respond to incidents in production environments.**

---

## 8. Flag

**System Status:** SECURED  
**Flag:** `THM{FAKEBANK-SECURED}`
<img width="975" height="446" alt="image" src="https://github.com/user-attachments/assets/7ee03d79-0350-46c0-8af4-a0ca086cabf3" />

  
