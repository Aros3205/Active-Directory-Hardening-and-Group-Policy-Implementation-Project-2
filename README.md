
# Active Directory Hardening & Group Policy Implementation (Lab Project)

## 📌 Overview

In this lab, I designed and implemented an on-premises *Active Directory* environment and applied *Group Policy* for security hardening. The project covers:

- Installing and configuring *Active Directory Domain Services (AD DS)* and DNS  
- Promoting a Windows Server to a *Domain Controller*  
- Designing *Organizational Units (OUs)* and creating users  
- Building hardening *Group Policy Objects (GPOs)*:
  - Disable Shut Down / Restart / Sleep / Hibernate
  - Restrict Control Panel and Add/Remove Programs
  - Limit what standard users can change
- Using *Security Filtering* to target specific users / groups  
- Testing the policies on a *Windows 8.1 domain-joined client*

All steps below include screenshots taken directly from the lab.

---

## 1️⃣ Lab Topology & Virtual Networking

The lab is built in a virtualized environment with:

- 1 x Windows Server (Domain Controller)
- 1 x Windows 8.1 client
- NAT + internal networking to support domain communication and internet

*VirtualBox / hypervisor network configuration (example):*

![Virtual Network / Adapter Setup](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%20(71).png)

![VM Network Details](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%20(72).png)

---

## 2️⃣ Install AD DS & DNS on Windows Server

Using *Server Manager → Add roles and features*, the following roles are installed:

- *Active Directory Domain Services*
- *DNS Server*

![Server Manager – Roles Installed](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-11-29%20122151.png)

This prepares the server to be promoted to a domain controller.

---

## 3️⃣ Promote the Server to a Domain Controller

After AD DS is installed:

1. In *Server Manager*, click the notification flag
2. Choose *Promote this server to a domain controller*
3. Create a *new forest*, for example: rg.local
4. Configure DSRM password
5. Complete the wizard and reboot

Once the server restarts as a DC, we can open the AD / GPO consoles.

*Opening AD / GPO consoles from Server Manager:*

![Server Manager – Tools menu](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-01%20060248.png)

*Group Policy Management Console (GPMC) showing the new domain:*

![GPMC – Domain and Default GPOs](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-01%20060407.png)

---

## 4️⃣ Create Organizational Units (OUs) & Users

Using *Active Directory Users and Computers (ADUC)*, I created a logical OU structure. For example:

- *NIGERIA*
  - NIGERIA-Users
  - NIGERIA-Computers
- *UK*
  - UK-Users
  - UK-Computers
- *USA*
  - USA-Users
  - USA-Computers

Then I created user accounts like *Babafemi Raji* and placed them into the appropriate OU.

OU and object structure appear throughout GPMC:

![Domain and OU Structure in GPMC / ADUC](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20011800.png)

---

## 5️⃣ Create Security Hardening GPOs

All Group Policies were created and managed in *Group Policy Management*.

---

### 5.1 – Create & Link a New GPO

1. In *GPMC, right-click the **domain* (rg.local)  
2. Select *Create a GPO in this domain, and Link it here…*  
3. Name it something clear, e.g. *Disable shutdown Ability*

![Create New GPO & Link to Domain](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Impl…

📝 Notes
	•	All image links use GitHub raw URLs.
	•	If you move images into a different folder, update the /screenshots/ part of the paths.
	•	If a particular screenshot doesn’t visually match the step, you can simply swap its filename with another from your list — the URL pattern stays the same.
