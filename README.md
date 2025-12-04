[18:17, 12/4/2025] Mr Tolu.🇺🇸: # Active Directory Hardening & Group Policy Project

## 📌 Overview  
This project demonstrates how to:

- Install and configure *Active Directory Domain Services (AD DS)*
- Promote a Windows Server to a *Domain Controller*
- Create and organize *Organizational Units (OUs)* and domain users
- Implement *security-hardening Group Policy Objects (GPOs)*:
  - Disable shutdown / restart options
  - Block *Command Prompt (CMD)*
  - Hide / restrict *Add or Remove Programs*
  - Restrict access to *Control Panel*
- Apply *Security Filtering* to target specific users/groups
- Test and verify policies on a *Windows 8.1* domain client

---

## 1️⃣ Install AD DS  

From *Server Manager*:

> Add Roles and Features → Select *Active Directory Domain Services*

![AD DS Install](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/Screenshot%20(71).png)

---

## 2️⃣ Promote Server to Domain Controller  

After installing the AD DS role, promote the server:

> Click *“Promote this server to a domain controller”* → Create a new forest/domain (e.g. rg.local)

![Promote to Domain Controller](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/Screenshot%20(72).png)

---

## 3️⃣ Create Organizational Units (OUs) and Users  

Open *Active Directory Users and Computers (ADUC)* and design the OU structure:

- Create OUs for locations (e.g. *NIGERIA, **UK, **USA*)
- Inside each, create sub-OUs for *Users* and *Computers*
- Create domain users (e.g. Babafemi Raji) in the appropriate OU

![OU Structure and Users](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/Screenshot%20(73).png)

---

## 4️⃣ Open Group Policy Management  

From *Server Manager* → *Tools* → *Group Policy Management*:

- Confirm the *Forest* and *Domain*
- Review the default GPOs (Default Domain Policy, Default Domain Controllers Policy)

![Group Policy Management Console](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/Screenshot%20(74).png)

---

## 5️⃣ Create Security-Hardening GPOs  

### 5.1 Disable Shut Down / Restart / Sleep / Hibernate  

Create a GPO (e.g. *“Disable Shutdown Ability”*) and edit:

> Computer Configuration → Policies → Administrative Templates →  
> Start Menu and Taskbar →  
> *Remove and prevent access to the Shut Down, Restart, Sleep, and Hibernate commands* → *Enabled*

![Disable Shutdown Policy](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/Screenshot%20(75).png)

---

### 5.2 Disable Command Prompt (CMD)  

Create or edit a GPO (e.g. *“Disable Access to CMD”*):

> User Configuration → Policies → Administrative Templates → System →  
> *Prevent access to the command prompt* → *Enabled*

![Disable CMD Policy](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/Screenshot%20(76).png)

---

### 5.3 Disable / Hide Add or Remove Programs  

Create a GPO (e.g. *“Disable Add or Remove Programs”*):

> User Configuration → Policies → Administrative Templates →  
> Control Panel → Add or Remove Programs →  
> *Remove Add or Remove Programs* → *Enabled*

![Disable Add or Remove Programs](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/Screenshot%20(77).png)

---

### 5.4 Restrict Control Panel Access  

To block access to Control Panel:

> User Configuration → Policies → Administrative Templates → Control Panel →  
> *Prohibit access to Control Panel and PC settings* → *Enabled*

![Restric…
[18:17, 12/4/2025] Mr Tolu.🇺🇸: This ensures all new settings are applied immediately.
[18:18, 12/4/2025] Mr Tolu.🇺🇸: 8️⃣ Test on Windows 8.1 Domain Client

8.1 Log in as a Domain User

On the Windows 8.1 machine joined to the domain (rg.local), log in with a domain user (e.g. Babafemi Raji).
[18:18, 12/4/2025] Mr Tolu.🇺🇸: 8.2 Verify Control Panel / Programs Restrictions

Try to:
	•	Open Control Panel
	•	Access Programs and Features / Add or Remove Programs
	•	Shut down / restart from the start menu
	•	Open cmd.exe

They should now be blocked or hidden according to the applied GPOs.
[18:19, 12/4/2025] Mr Tolu.🇺🇸: Summary
	•	AD DS successfully installed and configured
	•	Server promoted to a Domain Controller
	•	Structured OUs and domain users created
	•	GPOs built to:
	•	Disable shutdown/restart options
	•	Block Command Prompt
	•	Hide Add/Remove Programs
	•	Restrict Control Panel access
	•	Security Filtering limits impact to intended users/groups
	•	Policies verified from a Windows 8.1 domain client

⸻

📝 Notes
	•	All image links use GitHub raw URLs.
	•	If you move images into a different folder, update the /screenshots/ part of the paths.
	•	If a particular screenshot doesn’t visually match the step, you can simply swap its filename with another from your list — the URL pattern stays the same.
