# Active Directory Hardening & Group Policy Project

## 📌 Overview  
This project shows the setup of Active Directory Domain Services (AD DS), creation of security-hardened Group Policy Objects (GPOs), and validation on a Windows client environment.

---

## 1️⃣ Install AD DS  
- Open Server Manager → Add Roles and Features → select “Active Directory Domain Services”

![AD DS Install](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/312E07E3-6ED5-43E6-B4B0-4091D24A4B83.jpeg)

---

## 2️⃣ Promote to Domain Controller  
- Use the “Promote this server to a domain controller” wizard to create a new forest/domain.

![DC Promotion](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/43643A03-E3CC-4072-AC33-3F56A72B0E08.jpeg)

---

## 3️⃣ Create Organizational Units (OUs)  
- In Active Directory Users & Computers (ADUC), create OUs such as Servers, Workstations, Admins, Users.

![OU Structure](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/B665C7DF-2F15-4F5E-8372-B121847226A8.jpeg)

---

## 4️⃣ Configure Group Policy Objects (GPOs)

### 4.1 Disable Command Prompt (CMD)  
User Configuration → Administrative Templates → System → Prevent access to the command prompt

![Disable CMD Policy](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/7CB7218B-31F6-431E-9DAC-E3CCC92D79BD.jpeg)

Link the GPO to the appropriate OU.

---

### 4.2 Hide Add/Remove Programs  
User Configuration → Administrative Templates → Control Panel → Programs → “Hide Add/Remove Programs page”

![Hide Add/Remove Programs Setting](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/7F7A6A8C-CC99-4B06-ACBB-FF2BEEE06887.png)

---

### 4.3 Restrict Control Panel Access  
User Configuration → Administrative Templates → Control Panel → Restrict access to control panel/settings

![Control Panel Restrictions Policy](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/E6D851C5-6B31-4515-A7A3-5B483A9D39A7.png)

---

## 5️⃣ Apply Security Filtering  
- Use Security Filtering in GPMC to specify which users/groups the GPO applies to.

![Security Filtering Setup](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/B4015888-165A-4F3E-A42D-B27D7D2CB53B.png)

---

## 6️⃣ Force GPO Update (gpupdate)  
- Run `gpupdate /force` on Domain Controller and on client machines to apply policies.

![gpupdate Result](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/2B845052-4C29-4E5F-8F80-87299158AECA.png)

---

## 7️⃣ Test on Windows 8.1 Client

### 7.1 Log in with Domain Credentials  

![Windows 8 Domain Login](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/0A7D1527-50B4-47C0-BE7E-39A40FE72773.png)

### 7.2 Verify Restricted Control Panel / System Settings  
Attempt to open Control Panel, Add/Remove Programs, cmd.exe, and other restricted tools — they should be blocked.

![Restricted Control Panel – Example 1](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/B18C0137-B89D-4B98-BD0C-0B3DC71495B8.png)  
![Restricted Control Panel – Example 2](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/screenshots/96EA9B96-718A-4460-9F56-45E97168380C.png)

---

## ✅ Summary  
- AD DS installed & configured  
- Domain Controller promoted  
- OUs created for structured management  
- GPOs built and applied (CMD blocked, Add/Remove Programs hidden, Control Panel restricted)  
- Security Filtering applied to target specific users/groups  
- Client tested — GPO restrictions successfully enforced  

---

## 📎 Notes  
- These image URLs use GitHub’s “raw” links, which reliably display images hosted in your repository.  
- If you rename or move screenshots, update the URLs accordingly.  
- For future screenshots, upload them to the same `screenshots/` folder to maintain link consistency.
