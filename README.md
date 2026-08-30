<div align="center">
  <h1>🛡️ ALPHA CORP - Active Directory Hardening & Attack Surface Reduction</h1>
  <p><i>Securing Enterprise Identity Architecture & Mitigating Privilege Escalation via Windows Server GPOs.</i></p>

  <a href="https://mega.nz/embed/1UwGmZwB#o9NOAJR-PjWBHQpfbgFWnrcmISyntcLuLs0iVaXnS18" target="_blank">
    <img src="https://img.shields.io/badge/▶️_Watch_POC_Demo-FF0000?style=for-the-badge&logo=youtube&logoColor=white" alt="Watch Demo"/>
  </a>
  <a href="https://github.com/alpha-bet-404/mcsa-project/blob/main/Alpha%20Corp%20AD%20%26%20GPO%20Overview.pdf" download>
    <img src="https://img.shields.io/badge/📥_Architecture_PDF-0052CC?style=for-the-badge&logo=pdf&logoColor=white" alt="Download PDF"/>
  </a>
</div>

---

## 📋 Executive Summary
This project demonstrates the practical implementation of an enterprise-grade Active Directory hardening strategy for **ALPHA CORP**. Built from the ground up using Windows Server and Group Policy Objects (GPOs), the environment focuses on **Attack Surface Reduction (ASR)**, **Defense-in-Depth**, and enforcing the **Principle of Least Privilege (PoLP)** across corporate Organizational Units (IT, HR, and SALES).

The core objective is to simulate a production infrastructure hardened against common post-exploitation techniques, lateral movement, credential harvesting, and unauthorized local reconnaissance.

### 🏢 Domain Architecture & Identity Setup
| Parameter | Value | Security Focus |
| :--- | :--- | :--- |
| **Organization** | Alpha Corp | Enterprise Scope |
| **Domain Name (FQDN)** | `alpha.local` | Centralized Identity |
| **Server Infrastructure** | Windows Server 2016 | Active Directory Domain Controller (AD DC) |
| **RBAC Structure** | Segmented OUs | Isolated Access & GPO Inheritance Boundaries |

---

## 👥 Organizational Units & Security Hardening Controls

### 💻 A. IT Department (`OU=IT`)
**Assigned Identities:** `IT.JOHN`, `IT.EMMA`, `IT.MICHAEL`  
> **Credential Baseline:** Temporary default passwords (`p@ssword123`) configured with mandatory password change enforcement at initial authentication.

**Applied Hardening Controls:**
* **Credential Protection:** Enforced Account Lockout Threshold (5 invalid attempts, 5-minute lockout duration/reset window) to neutralize Password Spraying and automated Brute-Force attacks.
* **Password Policy:** Minimum length baseline enforced (8+ characters).
* **Endpoint Hardening:** 
  * Disabled **Registry Editor (`regedit.exe`)** to prevent unauthorized persistence mechanisms, security tool tampering, and SAM registry dumping.
  * Blocked USB storage and denied Read/Write access to removable media to prevent **Data Loss Prevention (DLP)** violations and BadUSB execution vectors.

---

### 📁 B. HR Department (`OU=HR`)
**Assigned Identities:** `HR.SARAH`, `HR.DAVID`  
> **Authentication Restriction:** Account logons are explicitly restricted to designated hostnames (`PC-HR`).

**Applied Hardening Controls:**
* **Credential Protection:** Enforced Account Lockout & Baseline Password Policy.
* **Host Hardening & Recon Suppression:** 
  * Completely disabled **Command Prompt (`cmd.exe`)**, **Run Command (`Win+R`)**, and **Registry Editor (`regedit.exe`)** for standard accounts to prevent local environmental reconnaissance, LOLBins execution, and script-based privilege escalation.
  * **Lateral Movement Mitigation:** Restricted user authentication exclusively to assigned workstations (`PC-HR`), containing potential compromise vectors within single endpoints.
  * **DLP Enforce:** Full block on removable media and external USB devices to stop insider threats and data exfiltration.

---

### 📊 C. SALES Department (`OU=SALES`)
**Assigned Identities:** `SALES.JAMES`, `SALES.LINDA`, `SALES.ROBERT`  
> **Credential Baseline:** Mandatory password rotation on initial logon.

**Applied Hardening Controls:**
* **Credential Protection:** Enforced Account Lockout & Baseline Password Policy.
* **Endpoint Lockdown:** 
  * Complete restriction of `cmd.exe`, `regedit.exe`, and Execution Prompts (Run Menu) to reduce attack surfaces on public/sales-facing endpoints.
  * USB Mass Storage and Removable Media access strictly blocked.

---

## ⚙️ Hardening Matrix (GPO Policy Summary)

| Security Control / Attack Vector | IT Department | HR Department | SALES Department | Threat Mitigated |
| :--- | :--- | :--- | :--- | :--- |
| **Account Lockout Threshold** | 5 Attempts / 5 Min | 5 Attempts / 5 Min | 5 Attempts / 5 Min | Password Spraying & Brute Force |
| **Min Password Length** | 8 Characters | 8 Characters | 8 Characters | Weak Credential Exploitation |
| **Disable CLI / CMD Access** | No | Yes | Yes | Local Reconnaissance & LOLBins |
| **Disable Execution Prompt (RUN)** | No | Yes | Yes | Unauthorized Binary Execution |
| **Disable Registry Editor** | Yes | Yes | Yes | Persistence & Security Tampering |
| **Block USB Mass Storage** | Yes | Yes | Yes | Insider Threat & Data Exfiltration |
| **Logon Workstation Binding** | Global Domain | Restricted (`PC-HR`) | Global Domain | Lateral Movement Across Subnets |

---

## 🧪 Security Control Validation & Audit Methodology

To simulate audit procedures and verify policy enforcement from an adversary/insider perspective:

1. **Authentication:** Log into a domain-joined endpoint using a standard user identity (e.g., `HR.SARAH`).
2. **Execution Test:** Trigger execution mechanisms (`Win + R`) and attempt to launch CLI interpreters (`cmd.exe`) or System Inspection tools (`regedit.exe`).
3. **Hardware Vector Test:** Insert an external USB mass storage controller to test driver mounting controls.
4. **Validation Result:** The OS successfully blocks execution, throwing standard restriction events:
   > *"This operation has been cancelled due to restrictions in effect on this computer."*

---
**Maintained by:** ALPHA-BET  
**Focus:** Offensive Security & Threat Detection Architecture
