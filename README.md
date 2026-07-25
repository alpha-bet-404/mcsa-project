<div align="center">
  <h1>🛡️ ALPHA CORP - Active Directory Security Project</h1>
  <p><i>Securing enterprise environments through robust Windows Server and Group Policy implementations.</i></p>

  <a href="https://github.com/alpha-bet-404/mcsa-project/blob/main/Project-Mcsa.mp4" target="_blank">
    <img src="https://img.shields.io/badge/▶️_Watch_Demo-FF0000?style=for-the-badge&logo=youtube&logoColor=white" alt="Watch Demo"/>
  </a>
  <a href="https://github.com/alpha-bet-404/mcsa-project/blob/main/Alpha%20Corp%20AD%20%26%20GPO%20Overview.pdf" download>
    <img src="https://img.shields.io/badge/📥_Topology_Diagram-0052CC?style=for-the-badge&logo=pdf&logoColor=white" alt="Download PDF"/>
  </a>
</div>

---

## 📋 Project Overview
This project demonstrates the implementation of a secure Active Directory environment for **ALPHA CORP** using Windows Server and Group Policy Objects (GPOs). The primary objective is to enforce standardized security policies across three distinct departments (IT, HR, and SALES) while strictly adhering to the principle of least privilege for standard users.

### 🏢 Domain Infrastructure
| Item | Value |
| :--- | :--- |
| **Company Name** | Alpha Corp |
| **Domain Name** | `alpha.local` |
| **Server OS** | Windows Server 2019 / 2022 |
| **Admin Password** | `alpha@0` |
| **DSRM Password** | `alpha@0123` |

---

## 👥 Organizational Units & Security Policies

### 💻 A. IT Department (`OU=IT`)
**Assigned Users:**
* `IT.JOHN` 
* `IT.EMMA` 
* `IT.MICHAEL` 
> **Note:** Default password is `p@ssword123`. Users are forced to change their password at the next logon.

**Enforced Security Policies:**
1. **Account Lockout:** Threshold set to 5 invalid attempts, with a 5-minute lockout duration and counter reset.
2. **Password Policy:** Minimum length of 8 characters (Complexity requirements disabled).
3. **System Restrictions:** USB storage devices are blocked, Read/Write to removable media is denied, and the Registry Editor is disabled for standard users.

### 📁 B. HR Department (`OU=HR`)
**Assigned Users:**
* `HR.SARAH`
* `HR.DAVID`
> **Note:** Default password is `p@ssword123` (Force change at next logon). **Logon restricted exclusively to `PC-HR`.**

**Enforced Security Policies:**
1. **Account Lockout:** Same as IT (5 attempts / 5 mins).
2. **Password Policy:** Same as IT (Min 8 characters).
3. **System Restrictions:** Command Prompt (CMD), Run Command, and Registry Editor are completely disabled. USB storage and removable media access are strictly blocked.

### 📊 C. SALES Department (`OU=SALES`)
**Assigned Users:**
* `SALES.JAMES`
* `SALES.LINDA`
* `SALES.ROBERT`
> **Note:** Default password is `p@ssword123` (Force change at next logon).

**Enforced Security Policies:**
1. **Account Lockout:** Same as IT (5 attempts / 5 mins).
2. **Password Policy:** Same as IT (Min 8 characters).
3. **System Restrictions:** Command Prompt (CMD), Run Command, and Registry Editor are completely disabled. USB storage and removable media access are strictly blocked.

---

## ⚙️ Group Policy Implementation Summary

| Policy Area | IT Department | HR Department | SALES Department |
| :--- | :--- | :--- | :--- |
| **Account Lockout** | 5 Attempts / 5 Min | 5 Attempts / 5 Min | 5 Attempts / 5 Min |
| **Password Length** | Min 8 Characters | Min 8 Characters | Min 8 Characters |
| **Disable CMD** | No | Yes | Yes |
| **Disable RUN** | No | Yes | Yes |
| **Disable Registry** | Yes | Yes | Yes |
| **Block USB Access** | Yes | Yes | Yes |

---

## 🧪 Testing Methodology
To verify the active security policies, follow these steps in the environment:

1. Log in to a domain-joined machine using any standard user account (e.g., `HR.SARAH`).
2. Press `Win + R` to open the Run dialog.
3. Attempt to execute restricted tools by typing `cmd` or `regedit`.
4. Attempt to mount an external USB storage device.
5. **Expected Result:** The system should explicitly block the action with the message: *“This operation has been cancelled due to restrictions in effect on this computer.”*

---
**Developed by:** ALPHA-BET  
**Date:** July 2026
