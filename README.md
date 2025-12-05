# Active Directory Hardening & Group Policy Enforcement Project

## 🔒 Overview
This project demonstrates the deployment and hardening of a Windows Active Directory environment using Group Policy Objects (GPOs).  
It includes setting up a Domain Controller, designing Organizational Units (OUs), applying enterprise-grade security restrictions, and validating the results on a Windows 8.1 domain-joined client.

---

## 🧠 Skills Demonstrated
- Active Directory Domain Services (AD DS)
- Group Policy Management (GPMC)
- Windows Server Administration
- OU Design & User Provisioning
- Security Hardening (Least Privilege)
- GPO Filtering & Scope Management
- Client Domain Integration
- Troubleshooting GPO Application

---

## 1️⃣ Install AD DS

On Windows Server, AD DS and DNS were installed through:

*Server Manager → Add Roles and Features → Active Directory Domain Services*

This enabled the environment for domain controller promotion.

---

## 2️⃣ Promote Server to Domain Controller

Using the AD DS Configuration Wizard:

- Created a new forest: *rg.local*
- Installed DNS automatically
- Set Directory Services Restore Mode (DSRM) password
- Rebooted to complete the promotion

---

## 3️⃣ Create Organizational Units (OUs) & Users

To maintain a clean and scalable AD structure, I created regional OUs and sub-OUs for users and computers:

- *NIGERIA*
  - NIGERIA-Users  
  - NIGERIA-Computers
- *UK*
  - UK-Users  
  - UK-Computers
- *USA*
  - USA-Users  
  - USA-Computers

Users such as *Babafemi Raji* were created and placed into their respective OUs.

![OU Structure](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20011953.png)

---

## 4️⃣ Configure Group Policy Objects (GPOs)

Security-focused GPOs were created to enforce restrictions across standard users.

### 4.1 Disable Command Prompt  
*Path:*  
User Configuration → Administrative Templates → System → Prevent access to the command prompt

### 4.2 Hide Add/Remove Programs  
*Path:*  
User Configuration → Administrative Templates → Control Panel → Programs → Hide Add/Remove Programs page

### 4.3 Restrict Control Panel Access  
*Path:*  
User Configuration → Administrative Templates → Control Panel → Prohibit access to Control Panel and PC Settings

### 4.4 Remove Shutdown / Restart / Sleep / Hibernate Options  
*Path:*  
Computer Configuration → Administrative Templates → Start Menu and Taskbar → Remove and prevent access to Shut Down...

These restrictions ensure users cannot modify system configuration or bypass administrative controls.

---

## 5️⃣ Apply Security Filtering

Security Filtering was configured so GPOs apply only to specific targeted users rather than all authenticated users.

![Security Filtering](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20020710.png)

This ensures *least privilege* by applying restrictions only where needed.

---

## 6️⃣ Force Group Policy Update

After linking the GPOs, I ran:
