
# Datacom Cybersecurity Simulation Documentation

This document contains the completed write-up for the Datacom cybersecurity virtual simulation experience. The content includes task analysis, professional responses, and tailored enhancements based on practical cybersecurity knowledge and best practices.

---

## 🛡️ TASK 1: Researching APT34 and Threat Landscape

### 📌 Overview
You were assigned the role of a cybersecurity consultant to investigate a sophisticated cyberattack carried out by APT34 (also known as OILRIG). The attack led to a breach involving customer data and IP theft.

### 🧠 Objective
Conduct OSINT research on APT34 and apply the MITRE ATT&CK framework to:
- Identify group TTPs (Tactics, Techniques, and Procedures)
- Determine affected industries and motives
- Suggest mitigation strategies

### ✅ Report: APT34 (OILRIG)

**🕰️ History**  
APT34, aka OILRIG, has operated since at least 2014, conducting long-term cyber-espionage operations across the Middle East.

**🌐 Nation-State Association**  
Believed to be backed by the Iranian government, with links to the Iranian Ministry of Intelligence (MOIS).

**🏢 Targeted Sectors**  
- Government agencies  
- Energy and Oil & Gas sectors  
- Telecommunications  
- Financial institutions  
- Critical infrastructure

**🎯 Motives**  
The group’s primary goal is cyber espionage — stealing classified, military, or geopolitical information.

**🔍 TTPs (per MITRE ATT&CK)**  
- **Initial Access**: Spear-phishing emails, compromised credentials  
- **Execution**: Use of malicious macros and VB scripts  
- **Persistence**: Creation of scheduled tasks and registry run keys  
- **Defense Evasion**: Obfuscated scripts and DLL side-loading  
- **C2 (Command & Control)**: HTTPS-based or DNS tunneling channels  
- **Exfiltration**: Encrypted channel uploads or staged drop points

**🛡️ Security Recommendations**  
- **Advanced Threat Detection Systems (SIEM/XDR)**  
- **Frequent Employee Awareness Training**  
- **Zero Trust Architecture + Network Segmentation**  
- **Timely Vulnerability Management and Patch Cycles**  
- **Strong Endpoint Detection & Response (EDR) Deployment**  
- **Well-Defined Incident Response and Recovery Plans**

---

## ⚠️ TASK 2: Risk Assessment Using Padlock Analogy

### 📌 Context
The client, concerned about its information system’s integrity and security, requested a detailed risk assessment using the padlock-and-fence metaphor. You are to document inherent, current, and target risk ratings and provide actionable mitigation strategies.

### 🧩 Key Elements of the Assessment

**🔐 Protected Assets Include:**  
- Customer PII (Personally Identifiable Information)  
- Financial Records  
- Intellectual Property (Proprietary software, internal R&D)  
- Network Systems & Infrastructure  
- Authentication Databases

**🧮 Risk Matrix Definition:**  
| Likelihood | Consequence | Risk Rating = L × C |
|------------|-------------|----------------------|

### 🔄 Risk Scenarios Summary (Extracted from Submitted Excel File)

| Scenario                        | Inherent Risk | Current Risk | Target Risk | Notes |
|---------------------------------|----------------|----------------|---------------|-------|
| Cyberattack via phishing        | 4 (High)       | 3 (Med)        | 2 (Low)       | Train staff, improve spam filters |
| Insider threat (employee error) | 3 (Med)        | 2 (Low)        | 1 (Very Low)  | Access control & monitoring |
| Ransomware on core servers      | 5 (Very High)  | 4 (High)       | 2 (Low)       | EDR, Immutable backups, DR plan |

**🛠️ Mitigation Summary:**  
- Install & monitor DLP (Data Loss Prevention) tools  
- Conduct regular risk assessments and audits  
- Use immutable backups and implement DRaaS (Disaster Recovery as a Service)  
- Foster a security-aware culture with simulations and gamified learning  
- Enforce Principle of Least Privilege (PoLP)

### 🧾 Report Status
Detailed XLSX report file edited and attached [here](./Risk%20Assessment-Datacom%20Task%202.xlsx).

