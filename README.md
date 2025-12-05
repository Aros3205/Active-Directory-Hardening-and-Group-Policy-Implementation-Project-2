# Active Directory Hardening and Group Policy Implementation Project

## Overview
This project demonstrates the installation and configuration of Active Directory Domain Services (AD DS), creation of a secure organizational structure, deployment of targeted Group Policy Objects (GPOs), and enforcement of workstation restrictions for improved security posture.

Only essential screenshots are included to maintain a clean and professional documentation format.

---

## 1. Installing Active Directory Domain Services (AD DS)

Open Server Manager → Add Roles and Features and select **Active Directory Domain Services**.

![Install AD DS](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-01%20060150.png)

---

## 2. Promoting the Server to a Domain Controller

After installation, select **Promote this server to a domain controller**, then configure a new forest and domain.

![Promote to Domain Controller](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-01%20060407.png)

---

## 3. Creating the Organizational Unit (OU) Structure

Open **Active Directory Users and Computers (ADUC)** and create OUs such as:

- Admins  
- Users  
- Servers  
- Workstations  

![OU Structure](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20011953.png)

---

## 4. Creating Users and Assigning Roles

Create standard and privileged user accounts. Place them in their respective OUs to allow role-based access control (RBAC) through GPO inheritance.

![User Creation](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20014930.png)

---

## 5. Creating and Linking Group Policy Objects (GPOs)

### 5.1 Create a New GPO
Open **Group Policy Management Console (GPMC)** → Right-click the OU → **Create a GPO**.

![Create GPO](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20020210.png)

---

### 5.2 Apply Security Filtering
Use **Security Filtering** to apply the GPO only to specific users or groups, improving precision and security.

![Security Filtering](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20020710.png)

---

## 6. Forcing GPO Updates

To immediately enforce changes on workstations and servers, use:

```
gpupdate /force
```

![GPUpdate](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20015813.png)

---

## 7. Joining a Windows Client to the Domain

From the client OS, navigate to:

Control Panel → System → Change Settings → Domain Join

![Domain Join](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20023738.png)

Reboot the workstation and log in with domain credentials.

---

## 8. Validating Group Policy Restrictions on the Client

The workstation now receives domain-level policies. The following restrictions were applied.

### 8.1 Remove “Add or Remove Programs”

![Add/Remove Programs Restricted](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20192423.png)

---

### 8.2 Control Panel Restrictions

![Control Panel Restricted](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-03%20015110.png)

---

### 8.3 Hardware and Sound Restrictions

![Hardware and Sound Restricted](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-03%20013923.png)

---

## 9. System Settings Access Restriction

The workstation is prevented from accessing system settings as defined by the applied GPO.

![System Settings Restricted](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20130846.png)

---

## Conclusion

This project demonstrates:

- Proper deployment of **Active Directory Domain Services**  
- Organizational Unit structuring for **role-based management**  
- Designing and applying **targeted Group Policies**  
- Validating **security restrictions** on a domain-joined workstation  
- Implementing foundational **AD hardening techniques**

This documentation provides a clear, enterprise-grade representation of the AD security implementation process.

