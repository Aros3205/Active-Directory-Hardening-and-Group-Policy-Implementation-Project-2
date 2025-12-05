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
[19:53, 12/4/2025] Aros.: them.

⸻

8️⃣ Join Windows 8.1 Client to the Domain

On the Windows 8.1 machine:
	1.	Set the DNS to point to the domain controller
	2.	Join the domain rg.local
	3.	Reboot
	4.	Log in as a domain user (e.g. RG\braji)

Client joined to domain and logged in as a domain user:
[19:53, 12/4/2025] Aros.: 9️⃣ Verify Group Policy Enforcement (Client Side)

9.1 – Control Panel & Programs

Open Control Panel and browse to Programs / Hardware and Sound to confirm that:
	•	Access to Add or Remove Programs / Programs and Features is restricted
	•	Certain options are greyed out or missing

Control Panel home for the domain user:
[19:54, 12/4/2025] Aros.: Devices and Printers screen:
[19:54, 12/4/2025] Aros.: Navigate into Programs and Hardware and Sound – your restrictions from the GPO (like hiding Add/Remove Programs) will show here:
[19:56, 12/4/2025] Aros.: 9.2 – Additional Settings / Power & UI Restrictions

Browse other Control Panel branches to see how far the GPO-based restrictions go:
[19:56, 12/4/2025] Aros.: These screens show the final user experience once all Group Policy restrictions are in place.
[19:57, 12/4/2025] Aros.: ✅ Summary

In this lab, I:
	•	Installed Active Directory Domain Services and DNS on a Windows Server
	•	Promoted the server to a Domain Controller for the rg.local domain
	•	Built a location-based OU structure and created domain user accounts
	•	Created and linked several hardening GPOs to:
	•	Remove shutdown/restart/sleep/hibernate commands
	•	Restrict access to Control Panel and Add or Remove Programs
	•	Used Security Filtering to precisely target which users / groups are affected
	•	Applied and validated the policies on a Windows 8.1 domain-joined client

This documentation plus the screenshots provides a complete story of Active Directory hardening with Group Policy, from initial setup to real end-user impact.
