# Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2
# Active Directory Hardening and Group Policy Implementation (Project 2)

A comprehensive deployment and hardening of Active Directory Domain Services (AD DS) including domain configuration, workstation onboarding, Group Policy creation, security baselining, and enforcement across multiple Windows systems.

---

## 🏗️ **1. Installing Active Directory Domain Services (AD DS)**  
Windows Server was prepared by installing the AD DS Server Role.

![AD DS Installation](screenshots/Screenshot%20(71).png)

---

## 🏛️ **2. Promoting Server to Domain Controller**  
After the AD DS role installation, the server was promoted to a Domain Controller and a new forest was created.

![Domain Controller Promotion](screenshots/Screenshot%20(72).png)

---

## 🖥️ **3. Joining Windows Client Machines to the Domain**  
Multiple Windows clients were successfully joined to the domain.

![Client Join](screenshots/Screenshot%20(73).png)

---

## 🛡️ **4. Group Policy Objects (GPO) Creation & Enforcement**  
Security and configuration Group Policies were created, including:

- Password & account lockout policies  
- Firewall enforcement  
- RDP security  
- User privileges  
- Baseline security templates  

![GPO Configuration](screenshots/Screenshot%20(74).png)

---

## 🔐 **5. Security Hardening & Best Practices**  
The project implements:

- Least privilege access  
- NTLM hardening  
- SMB signing  
- Audit & logging policies  
- Restricted groups  
- Application whitelisting  

![Security Policies](screenshots/Screenshot%20(75)%20-%20Copy.png)

---

## 🧪 **6. Verification & Testing**

Testing included:

- GPO replication  
- Client enforcement  
- Login restrictions  
- Folder redirection  
- Security baseline compliance  

![Testing 1](screenshots/Screenshot%20(75).png)
![Testing 2](screenshots/Screenshot%20(76)%20-%20Copy%20-%20Copy.png)
![Testing 3](screenshots/Screenshot%20(76)%20-%20Copy.png)

---

## 📁 **Project File Structure**
/
├── README.md
├── screenshots/
│ ├── placeholder.txt
│ ├── Screenshot (71).png
│ ├── Screenshot (72).png
│ ├── Screenshot (73).png
│ ├── Screenshot (74).png
│ ├── Screenshot (75).png
│ ├── Screenshot (75) - Copy.png
│ ├── Screenshot (76) - Copy.png
│ ├── Screenshot (76) - Copy - Copy.png
│ └── Screenshot (77).png

yaml
Copy code

---

## ✅ **Project Completed Successfully**
This project simulates a realistic enterprise environment with:

- Domain Controller setup  
- Workstation onboarding  
- Group Policy automation  
- Security baselining  
- Windows Server hardening  
