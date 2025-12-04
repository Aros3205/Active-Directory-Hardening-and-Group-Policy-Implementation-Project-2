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

![Create New GPO & Link to Domain](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20011953.png)

The GPO now appears under *Group Policy Objects*:

![GPO Objects in Domain](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20023716.png)

---

### 5.2 – Disable Shut Down / Restart / Sleep / Hibernate

Edit *Disable shutdown Ability* and navigate to:

> *Computer Configuration → Policies → Administrative Templates → Start Menu and Taskbar*  

Locate *“Remove and prevent access to the Shut Down, Restart, Sleep, and Hibernate commands”*.

![Locate Shutdown Restriction Policy](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20015233.png)

![Policy Focused in Editor](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20015625.png)

Open the policy and set it to *Enabled*:

![Remove Shutdown / Restart – Enabled](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20015813.png)

Save the GPO.

---

### 5.3 – Restrict Control Panel & Add/Remove Programs

Next, I created another GPO named *Disable Add or remove programs* (or reused a dedicated hardening GPO) and edited:

> *User Configuration → Policies → Administrative Templates → Control Panel*  

Key settings include:

- *“Prohibit access to Control Panel and PC settings”* → Enabled  
- Under *Control Panel → Add or Remove Programs*:  
  - *“Remove Add or Remove Programs”* → Enabled  

![Control Panel / Programs GPO Settings](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20014052.png)

GPMC summary shows the updated policy settings:

![GPO Summary After Editing Policies](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20192423.png)

And specifically the Add/Remove Programs removal:

![Remove Add or Remove Programs – Enabled](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20192939.png)

---

## 6️⃣ Security Filtering (Targeting Users / Groups)

By default, GPOs apply to *Authenticated Users. To harden only specific users or groups, I used **Security Filtering*:

1. Select the GPO in *GPMC*  
2. Go to the *Scope* tab  
3. Under *Security Filtering*:
   - Remove Authenticated Users (if you don’t want everyone affected)
   - Click *Add…* and choose:
     - Individual user(s) like *Babafemi Raji*
     - Security groups (e.g. country-specific or department-specific groups)

*Selecting a user / group from AD:*

![Select User / Computer / Group for Filtering](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20023822.png)

*GPO after adding specific users / groups to Security Filtering:*

![GPO Security Filtering Updated](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20024217.png)

Another view of GPO + links in the domain:

![Linked GPOs / Status Overview](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20130846.png)

---

## 7️⃣ Force Group Policy Update

To make sure the new settings apply immediately, on the Domain Controller I ran:

```powershell
gpupdate /force
