
# Active Directory Hardening & Group Policy Implementation Project

## 📌 Overview  
This project demonstrates deploying Active Directory (AD DS), configuring Group Policy Objects (GPOs) for security hardening, and testing the configuration via a Windows client. Screenshots are provided via direct links to the uploaded images for clarity.

---

## 1️⃣ Installing Active Directory Domain Services (AD DS)  
Open Server Manager → Add roles and features → select AD DS role.

![AD DS Install](./mnt/data/312E07E3-6ED5-43E6-B4B0-4091D24A4B83.jpeg)

---

## 2️⃣ Promoting Server to Domain Controller  
Use the “Promote this server to a domain controller” wizard to create a new forest/domain.

![DC Promotion](./mnt/data/43643A03-E3CC-4072-AC33-3F56A72B0E08.jpeg)

---

## 3️⃣ Creating Organizational Units (OUs)  
Use Active Directory Users and Computers (ADUC) to create structure (Servers, Workstations, Admins, Users).

![OU Creation](./mnt/data/B665C7DF-2F15-4F5E-8372-B121847226A8.jpeg)

---

## 4️⃣ Creating Group Policy Objects (GPOs) & Security Hardening  

### 4.1 Disable Command Prompt (CMD) via GPO  
User Configuration → Administrative Templates → System → Prevent access to command prompt

![Disable CMD Policy Edit](./mnt/data/7CB7218B-31F6-431E-9DAC-E3CCC92D79BD.jpeg)

### 4.2 Hide Add/Remove Programs via GPO  
User Configuration → Administrative Templates → Control Panel → Programs → Hide Add/Remove Programs page

![Hide Add/Remove Programs Setting](./mnt/data/7F7A6A8C-CC99-4B06-ACBB-FF2BEEE06887.png)

### 4.3 Restrict Control Panel Access via GPO  
User Configuration → Administrative Templates → Control Panel → Various restrictions

![Control Panel Restrictions Policy](./mnt/data/E6D851C5-6B31-4515-A7A3-5B483A9D39A7.png)

### 4.4 Apply Security Filtering to GPO  
Set which users/groups the GPO applies to.

![Security Filtering Setup](./mnt/data/B4015888-165A-4F3E-A42D-B27D7D2CB53B.png)

---

## 5️⃣ Force GPO Update (gpupdate)  

Run gpupdate /force on DC and client machines to apply new policies.

![gpupdate Result](./mnt/data/2B845052-4C29-4E5F-8F80-87299158AECA.png)

---

## 6️⃣ Testing on Windows Client (Windows 8.1)  

### 6.1 Logging In With Domain Account  
Login using domain credentials to ensure client joined domain correctly.

![Windows 8 Domain Login](./mnt/data/0A7D1527-50B4-47C0-BE7E-39A40FE72773.png)

### 6.2 Verify Restricted Control Panel / System Settings  
Check whether Add/Remove Programs, Control Panel, CMD, and other restricted features are blocked.

![Restricted Control Panel Screenshot 1](./mnt/data/B18C0137-B89D-4B98-BD0C-0B3DC71495B8.png)

![Restricted Control Panel Screenshot 2](./mnt/data/96EA9B96-718A-4460-9F56-45E97168380C.png)

---

## 📂 Project Summary & Next Steps  
- AD DS installed and configured  
- Domain Controller promoted  
- OUs created and organized  
- GPOs created for security hardening (CMD disabled, Add/Remove Programs hidden, Control Panel restricted)  
- Policies applied via GPO with security filtering  
- Client tested — restrictions enforced successfully  

If you push these screenshots to your GitHub screenshots/ folder later, you can simply update the links above to the corresponding raw-GitHub URLs and your README will continue to display properly.

