# 🛡️ Shields Up: Cybersecurity Simulation (Forage x AGI)

A simulated real-world cybersecurity analyst project completed through the **Forage x AGI Shields Up Cybersecurity Virtual Experience Program**. This simulation covers how to respond to critical vulnerabilities, communicate risk clearly, and execute brute-force password cracking in response to a ransomware attack.

---

## 📌 Task Overview

### ✅ Task 1: **Advisory Email – Apache Log4j Vulnerability**
- **Objective:** Investigate a high-severity Log4j vulnerability published by CISA, identify affected infrastructure, and inform responsible teams.
- **Skills Applied:** Threat intelligence, vulnerability analysis, communication with infrastructure teams.

### ✅ Task 2: **Bruteforce Decryption – Ransomware Containment**
- **Objective:** Write a Python script to brute-force the password of an encrypted `.zip` file after a ransomware incident.
- **Skills Applied:** Python scripting, incident response, password cracking.

---

## 🔍 Task 1: Vulnerability Advisory

### Background:
- **Threat:** Log4j RCE (Remote Code Execution) vulnerability (`Log4Shell`).
- **Software Affected:** Apache Log4j 2.0-beta9 to 2.14.1.
- **Affected System:** Product Development Staging Environment.
- **Owned by:** Product Development Team (John Doe – product@email.com)

### 🧠 Quiz Answers:
1. **Which infrastructure may be affected by the vulnerability?**  
   → ✅ Product Development Staging Environment

2. **Which team has ownership of the affected infrastructure?**  
   → ✅ Product Development Team

---

### 📨 Advisory Email Sent:

```
From: AIG Cyber & Information Security Team  
To: product@email.com  
Subject: Security Advisory: Critical Log4j Vulnerability Affecting Product Development Staging Environment  

Hello John Doe,

We are writing to alert you of a critical security vulnerability recently identified in the Apache Log4j logging library, which is present in the Product Development Staging Environment.

### ⚠️ Vulnerability Overview  
Apache Log4j (versions 2.0-beta9 to 2.14.1) contains a severe Remote Code Execution (RCE) vulnerability, widely known as Log4Shell. The flaw arises from unsafe usage of the Java Naming and Directory Interface (JNDI), which allows attackers to inject arbitrary lookup requests via specially crafted log messages.

### 🔍 Risk & Exploitation  
- Public exploit code is widely available.  
- Exploitation began as early as December 1, 2021.  
- Attackers can leverage malicious LDAP, DNS, and other JNDI endpoints to trigger the vulnerability.  

### 🔧 Recommended Remediation  
1. Upgrade Log4j to the latest version (2.17.0 or higher).  
2. Upgrade Java 7 to Java 8 if required.  
3. Review logs and firewall activity for signs of exploitation.  
4. Inform users of the affected service.

### ✅ Confirmation Plan  
A follow-up vulnerability check will be scheduled once remediation is confirmed.

Kind regards,  
AIG Cyber & Information Security Team
```

---

## 💻 Task 2: Brute-force Password Recovery

### Scenario:
- A `.zip` file was encrypted by ransomware.
- Attack was stopped before full execution.
- Goal: Crack the zip without paying ransom using RockYou-based brute-forcing.

### 🐍 Python Script Used:

```python
from zipfile import ZipFile, BadZipFile
from tqdm import tqdm
import sys

def main(zip_file='enc.zip', wordlist='rockyou.txt'):
    try:
        with ZipFile(zip_file) as zf, open(wordlist, 'rb') as f:
            for pw in tqdm(f, desc="Brute-forcing"):
                pw = pw.strip()
                try:
                    zf.extractall(pwd=pw)
                    print(f"\n[+] Password found: {pw.decode(errors='ignore')}")
                    return
                except:
                    continue
        print("\n[-] Password not found.")
    except (FileNotFoundError, BadZipFile) as e:
        print(f"[!] Error: {e}")

if __name__ == "__main__":
    main()
```

### 🔓 Decryption Result:
- **Password successfully found:** `SPONGEBOB`
- File successfully decrypted without paying ransom.

---

## 🧠 Key Takeaways

- **Proactive communication** of vulnerabilities is crucial to limiting attack surface.
- **Rapid incident response** can minimize ransomware damage.
- **Python scripting and automation** play a vital role in threat mitigation.
- **Weak attacker hygiene** (e.g., poor password choice) can often be exploited defensively.

---

## 📂 Project Structure

```
.
├── enc.zip              # Encrypted ransomware file (provided in simulation)
├── rockyou.txt          # Wordlist used for brute-forcing
├── crack_zip.py         # Python script used to brute-force password
```

---

## 🏁 Final Notes

This project simulates real-world responsibilities of a cybersecurity analyst:
- Understanding and communicating emerging vulnerabilities
- Coordinating with product teams
- Executing post-exploitation recovery using technical tools

> **Program:** Forage x AGI – Shields Up Cybersecurity Virtual Internship  
> **Role:** Information Security Analyst  
> **Completion:** ✅ All tasks completed  
> **Decryption Key:** `SPONGEBOB`

---

