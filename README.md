# Active Directory Hardening & Group Policy Enforcement Project

## 🔒 Overview  
This project demonstrates how I deployed and hardened a Windows Active Directory domain using Group Policy Objects (GPOs).  
It includes domain controller setup, OU design, user provisioning, GPO creation, security filtering, and client-side validation.  
The goal was to implement *enterprise-level security controls* using Group Policy.

---

## 🧠 Skills Demonstrated
- Active Directory Domain Services (AD DS)  
- Group Policy Management (GPMC)  
- Organizational Unit (OU) design  
- Windows Server Administration  
- User & Group Access Control  
- Security Hardening (Least Privilege, UI/feature restrictions)  
- Client Domain Integration  
- Troubleshooting Group Policy application  

---

## 🏗️ 1. Install Active Directory Domain Services (AD DS)

Using Server Manager → Add Roles and Features, I installed:

- Active Directory Domain Services  
- DNS Server  

This prepares the server for promotion to a Domain Controller.

---

## 🏰 2. Promote Server to a Domain Controller  

After installing AD DS, I promoted the server to a Domain Controller and created a new forest:

- *Domain Name:* rg.local  
- DNS and AD DS configured automatically  

---

## 🗂️ 3. Create Organizational Units (OU) and Users  

I designed a clean OU structure to separate users and computers by region:

- *NIGERIA*
  - NIGERIA-Users
  - NIGERIA-Computers
- *UK*
  - UK-Users
  - UK-Computers
- *USA*
  - USA-Users
  - USA-Computers

Then I created user accounts and placed them into the correct OU.

![OU Structure](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20011953.png)

---

## 🛡️ 4. Configure Group Policy Objects (GPOs)

### 4.1 Disable Command Prompt (CMD)

This security setting prevents users from running unauthorized scripts or commands.

*Path:*  
User Configuration → Administrative Templates → System → Prevent access to the command prompt

### 4.2 Hide “Add or Remove Programs”

*Path:*  
User Configuration → Administrative Templates → Control Panel → Programs → Hide Add/Remove Programs page

### 4.3 Restrict Control Panel Access

*Path:*  
User Configuration → Administrative Templates → Control Panel → Prohibit access to Control Panel and PC Settings

### 4.4 Remove Shutdown / Restart / Sleep / Hibernate Buttons

*Path:*  
Computer Configuration → Administrative Templates → Start Menu and Taskbar → Remove and prevent access to Shut Down…

---

## 🎯 5. Apply Security Filtering  
Security Filtering allows GPOs to apply only to specific users or groups.

Example: applying a restriction only to a standard user.

![Security Filtering](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20020710.png)

This ensures the GPO applies *only* to targeted accounts.

---

## 🔁 6. Force Group Policy Update  

To apply GPOs immediately:
This was executed on the Domain Controller and the client machine after joining the domain.

---

## 💻 7. Join Windows 8.1 Client to the Domain  

Steps:

1. Set DNS to point to the Domain Controller  
2. Join domain rg.local  
3. Reboot  
4. Log in using domain credentials  

### Domain Login Screen  
![Windows 8.1 Login](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-03%20015639.png)

---

## 🔍 8. Verify GPO Enforcement on the Client

### 8.1 Remove “Add or Remove Programs”  
GPO successfully hid the Programs & Features section.

![Remove Add/Remove Programs](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/mai…
