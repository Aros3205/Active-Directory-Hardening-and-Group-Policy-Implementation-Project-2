# Active Directory Hardening & Group Policy Implementation Project

## 📌 Overview
This project demonstrates the deployment of an on-premises **Active Directory Domain Services (AD DS)** environment and the implementation of **Group Policy Objects (GPO)** to harden Windows domain systems.  
It includes:

- AD DS Installation  
- Domain Controller promotion  
- Creating and applying security GPOs  
- Restricting system functionality via Group Policy  
- Testing GPO enforcement on a Windows 8.1 client  

All steps include properly aligned screenshots for clarity.

---

# 1️⃣ Installing Active Directory Domain Services (AD DS)

Open **Server Manager → Add roles and features** and install the AD DS role.

### Screenshot – Selecting AD DS in Server Manager  
![AD DS Install](screenshots/<PUT_CORRECT_FILENAME_HERE>)

After installation, promote the server to a domain controller.

---

# 2️⃣ Promoting the Server to a Domain Controller

Run the promotion wizard and create a new forest/domain (e.g., *lab.local*).

### Screenshot – Deployment Configuration  
![DC Promotion](screenshots/<PUT_CORRECT_FILENAME_HERE>)

After completion, the server reboots as a Domain Controller.

---

# 3️⃣ Creating Organizational Units (OUs)

Launch **Active Directory Users and Computers (ADUC)** and create OUs for organizing domain objects:

- _Servers_  
- _Workstations_  
- _Admins_  
- _Users_  

### Screenshot – OU Structure  
![OU Structure](screenshots/<PUT_CORRECT_FILENAME_HERE>)

---

# 4️⃣ Creating Group Policy Objects (GPOs)

Open **Group Policy Management Console (GPMC)** and create new GPOs for hardening.

## 4.1 Disable Command Prompt (CMD)

Navigate to:

**User Configuration → Administrative Templates → System → Prevent access to the command prompt**

### Screenshot – GPO Editor (Disable CMD)  
![Disable CMD Policy](screenshots/<PUT_CORRECT_FILENAME_HERE>)

Link the GPO to the appropriate OU.

### Screenshot – GPO Linked  
![GPO Linked](screenshots/<PUT_CORRECT_FILENAME_HERE>)

---

## 4.2 Disable Access to “Add or Remove Programs”

Navigate to:

**User Configuration → Administrative Templates → Control Panel → Programs**

Enable **“Hide Add/Remove Programs page”**.

### Screenshot – Hide Add/Remove Programs  
![Hide Programs Policy](screenshots/<PUT_CORRECT_FILENAME_HERE>)

---

## 4.3 Restrict Access to Specific Control Panel Items

Navigate to:

**User Configuration → Administrative Templates → Control Panel**

Configure **“Prohibit access to Control Panel”** or limit visible items.

### Screenshot – Control Panel GPO  
![Control Panel Restrictions](screenshots/<PUT_CORRECT_FILENAME_HERE>)

---

# 5️⃣ Configuring Security Filtering

To apply a GPO only to specific users or groups:

1. Select the GPO  
2. Go to **Scope**  
3. Under **Security Filtering** → *Add*  
4. Choose the user or group

### Screenshot – Security Filtering Dialog  
![Security Filtering](screenshots/<PUT_CORRECT_FILENAME_HERE>)

### Screenshot – Object Picker  
![Object Picker](screenshots/<PUT_CORRECT_FILENAME_HERE>)

---

# 6️⃣ Forcing Group Policy Updates

On the Domain Controller and client machines, run:
