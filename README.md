# Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2
# Active Directory Hardening and Group Policy Implementation (Project 2)

## 📘 Overview

This project walks through the deployment and hardening of an **Active Directory Domain Services (AD DS)** environment, including:

- Installing and configuring a Domain Controller  
- Joining Windows client machines to the domain  
- Creating and enforcing Group Policy Objects (GPOs)  
- Applying security baselines and hardening settings  
- Verifying that policies are applied and effective using testing and log review  

Screenshots are included throughout, using **direct links** to this repository’s image files.

---

## 🧱 0. Lab Environment & Prerequisites

This project assumes the following lab setup:

- **1× Windows Server** (acting as Domain Controller)  
- **1× or more Windows client machines** (Windows 10/11)  
- All systems are on the same **virtual network** (e.g., in VirtualBox, VMware, Hyper-V, or a cloud lab)

High-level prerequisites:

1. Static IP configured on the server  
2. Proper hostname for the future Domain Controller (e.g. `DC01`)  
3. Local administrator access on all machines  
4. Internet or ISO access for installing features/updates  

---

## 1️⃣ Installing Active Directory Domain Services (AD DS)

The first step is to install the **AD DS role** on the Windows Server.

### Step-by-Step

1. Log on to the server with a local Administrator account.  
2. Open **Server Manager**.  
3. Click **“Add roles and features”**.  
4. Choose **Role-based or feature-based installation**.  
5. Select the local server (e.g. `DC01`).  
6. Under **Server Roles**, check **Active Directory Domain Services**.  
7. Accept any required features and continue.  
8. Click **Install**, then wait for the installation to complete.

### Related Screenshot(s)

**AD DS installation wizard and role selection**:

![AD DS Role Installation](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%20(71).png)

> This screenshot typically shows the **Server Manager – Add Roles and Features** wizard with **Active Directory Domain Services** checked.

If you captured another screen during the same process (e.g. confirmation page):

![AD DS Install Progress](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%20(72).png)

---

## 2️⃣ Promoting the Server to a Domain Controller

Once AD DS is installed, promote the server to a **Domain Controller (DC)** and create a new forest/domain.

### Step-by-Step

1. In **Server Manager**, click the yellow flag notification:  
   - **“Promote this server to a domain controller”**.  
2. Select **Add a new forest** and specify a root domain name, e.g.:
   - `corp.local` or `lab.local`.
3. Set a **Directory Services Restore Mode (DSRM)** password.  
4. Review and configure DNS and NetBIOS name (use defaults unless you have a design).  
5. Review paths for database, log files, and SYSVOL (defaults are fine in a lab).  
6. Run **prerequisite check** and ensure there are no blocking errors.  
7. Click **Install**, and the server will reboot as a Domain Controller.

### Related Screenshot(s)

**Domain Controller promotion wizard**:

![Domain Controller Promotion](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%20(73).png)

> Typically shows the **Deployment Configuration** page where a new forest/domain is defined.

**Post-promotion status / DC role confirmation**:

![DC Promotion Summary](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%20(74).png)

---

## 3️⃣ Joining Windows Client Machines to the Domain

With the Domain Controller up, the next step is to join one or more Windows clients to the new domain.

### Step-by-Step

On each Windows client:

1. Configure the client’s **DNS server** to point to the Domain Controller’s IP.  
2. Open **System Properties**:
   - Right-click **This PC → Properties → Advanced system settings → Computer Name** tab.  
3. Click **Change…** and select **Domain**.  
4. Enter your domain name (`corp.local`, etc).  
5. Provide domain credentials (e.g. `CORP\Administrator`).  
6. After the “Welcome to the domain” message, reboot the client.  
7. Log on using a domain account to confirm the join.

### Related Screenshot(s)

**Client join to domain dialog / success**:

![Client Domain Join – 1](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20011800.png)

![Client Domain Join – 2](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20011953.png)

> These screenshots typically show the **domain join dialog** and **successful join confirmation**.

---

## 4️⃣ Creating Organizational Units (OUs) and User Accounts

To organize objects and prepare for GPO scoping, create OUs and user accounts.

### Step-by-Step

1. On the Domain Controller, open **Active Directory Users and Computers (ADUC)**.  
2. Right-click the domain (e.g. `corp.local`) → **New → Organizational Unit**.  
3. Create OUs such as:
   - `Servers`
   - `Workstations`
   - `Users`
   - `Admins`
4. Within `Users` or `Admins`, right-click → **New → User** to create test and admin accounts.  
5. Configure strong passwords according to your password policy.

### Related Screenshot(s)

**OUs and users in ADUC**:

![OU and User Structure](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20013900.png)

![User Properties / ADUC View](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20013941.png)

---

## 5️⃣ Group Policy Objects (GPO) Creation & Baseline Configuration

Use Group Policy to centrally enforce configuration and security settings across the domain.

### Example GPOs Implemented

- Password and **account lockout** policies  
- **Windows Firewall** settings  
- **Remote Desktop (RDP)** security  
- User rights & **privilege hardening**  
- Baseline hardening templates (e.g., CIS-like controls for lab)  

### Step-by-Step (Typical Flow)

1. Open **Group Policy Management** on the DC.  
2. Right-click **Group Policy Objects** → **New…** to create a new GPO:
   - e.g. `Baseline – Workstations`, `Baseline – Servers`, `RDP Hardening`, etc.  
3. Right-click the domain or OU (e.g. `Workstations`) → **Link an Existing GPO…** and select the new GPO.  
4. Edit the GPO:
   - **Computer Configuration → Policies → Windows Settings → Security Settings** for password, lockout, firewall, RDP, etc.  
   - Configure settings like:
     - Minimum password length  
     - Maximum password age  
     - Account lockout threshold  
     - Allow RDP only for certain groups  

### Related Screenshot(s)

**GPMC – GPO list / configuration**:

![GPO Configuration – 1](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20014008.png)

![GPO Configuration – 2](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20014052.png)

![GPO Link to OU / Domain](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20014652.png)

---

## 6️⃣ Security Hardening & Best Practices

This project focuses heavily on **hardening controls**, applied via GPO and AD configuration.

### 6.1 Least Privilege Access

- Separate **admin accounts** from standard user accounts  
- Restrict membership of privileged groups (e.g. `Domain Admins`, `Server Operators`)  
- Enforce that daily use happens with low-privilege accounts

**Example Screenshot – Restricted Group / User Rights**:

![Least Privilege / User Rights](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20014930.png)

---

### 6.2 NTLM Hardening

- Reduce or block NTLM usage where possible  
- Configure policies to **deny NTLM** to servers/workstations, except where strictly required  
- Prefer Kerberos in an AD environment  

**Example Screenshot – NTLM Policy Settings**:

![NTLM Hardening Policies](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20015233.png)

---

### 6.3 SMB Signing

- Require **SMB signing** on servers and clients to protect against relay attacks  
- Use GPO:
  - `Microsoft network client: Digitally sign communications (always)`  
  - `Microsoft network server: Digitally sign communications (always)`

**Example Screenshot – SMB Signing GPO**:

![SMB Signing Settings](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20015625.png)

---

### 6.4 Audit & Logging Policies

- Enable **Advanced Audit Policy**:
  - Logon events  
  - Account logon and management  
  - Object access  
  - Directory service access  
- Centralize logs using a SIEM or log collector (in a real environment).

**Example Screenshot – Audit Policy Configuration**:

![Audit Policy Configuration](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20015813.png)

---

### 6.5 Restricted Groups

- Use **Restricted Groups** in GPO to **enforce**:
  - Which users are allowed in local `Administrators`  
  - Which users are in Domain Admin–like groups  
- This prevents privilege creep and unauthorized elevation.

**Example Screenshot – Restricted Groups GPO**:

![Restricted Groups Settings](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20020210.png)

---

### 6.6 Application Whitelisting (AppLocker-style)

- Use GPO to implement basic **application control**:
  - Allow only signed or whitelisted executables  
  - Block unauthorized scripts and binaries  
- In a full production scenario, use AppLocker or WDAC with careful testing.

**Example Screenshot – Application Control / Whitelisting**:

![Application Whitelisting Policy](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20020710.png)

---

## 7️⃣ Verification & Testing

After configuring policies, it’s critical to confirm that GPOs are **actually applied** and behaving as expected.

### 7.1 On the Domain Controller / Clients

1. Run `gpupdate /force` on both the DC and clients.  
2. Use `gpresult /r` (or `gpresult /h report.html`) to verify which GPOs are applied.  
3. Test login behaviors:
   - Incorrect passwords triggering lockout  
   - RDP access restricted to specific groups  
   - Blocked applications when launching unauthorized executables  

### Related Screenshot(s)

**GPO Result / Policy Application Views**:

![Testing – Policy Result 1](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20021938.png)

![Testing – Policy Result 2](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20022133.png)

---

### 7.2 Event Logs & Security Monitoring

1. Open **Event Viewer** on the client or DC.  
2. Review:
   - **Security** logs (logon attempts, account lockouts)  
   - **System** and **Application** logs for GPO or service issues  
3. Confirm that:
   - Account lockouts are logged  
   - Logon failures/successes are recorded  
   - Any AppLocker/whitelisting events appear as expected  

**Example Screenshot – Event Viewer / Security Logs**:

![Security Events / Testing 1](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20023716.png)

![Security Events / Testing 2](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20023738.png)

![Security Events / Testing 3](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20023822.png)

---

## 8️⃣ Example Final Views & Dashboard Screens

Some additional screenshots you may want to keep in the documentation as “final state” views:

- GPO summary and final state  
- ADUC with OUs and users fully populated  
- Client system information showing domain membership  
- Additional configuration dialogs and test results  

**Additional Screenshots:**

![Final View – 1](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20024217.png)

![Final View – 2](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20130846.png)

![Final View – 3](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20192423.png)

![Final View – 4](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20192614.png)

![Final View – 5](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20192939.png)

![Final View – 6](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20193915.png)

![Final View – 7](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-02%20194028.png)

![Final View – 8](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-03%20012849.png)

![Final View – 9](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-03%20013712.png)

![Final View – 10](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-03%20013923.png)

![Final View – 11](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-03%20015031.png)

![Final View – 12](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-03%20015110.png)

![Final View – 13](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-03%20015140.png)

![Final View – 14](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-03%20015639.png)

![Final View – 15](https://raw.githubusercontent.com/Aros3205/Active-Directory-Hardening-and-Group-Policy-Implementation-Project-2/main/Screenshot%202025-12-03%20015744.png)

---

## 📂 Project File Structure (Example)

```text
/
├── README.md
├── Screenshot (71).png
├── Screenshot (72).png
├── Screenshot (73).png
├── Screenshot (74).png
├── Screenshot (75).png
├── Screenshot (75) - Copy.png
├── Screenshot (76).png
├── Screenshot (76) - Copy.png
├── Screenshot (76) - Copy - Copy.png
├── Screenshot (77).png
├── Screenshot 2025-11-29 122151.png
├── Screenshot 2025-12-01 055529.png
├── Screenshot 2025-12-01 055931.png
├── Screenshot 2025-12-01 060150.png
├── Screenshot 2025-12-01 060248.png
├── Screenshot 2025-12-01 060407.png
├── Screenshot 2025-12-02 011800.png
├── Screenshot 2025-12-02 011953.png
├── Screenshot 2025-12-02 013900.png
├── Screenshot 2025-12-02 013941.png
├── Screenshot 2025-12-02 014008.png
├── Screenshot 2025-12-02 014052.png
├── Screenshot 2025-12-02 014652.png
├── Screenshot 2025-12-02 014930.png
├── Screenshot 2025-12-02 015233.png
├── Screenshot 2025-12-02 015625.png
├── Screenshot 2025-12-02 015813.png
├── Screenshot 2025-12-02 020210.png
├── Screenshot 2025-12-02 020710.png
├── Screenshot 2025-12-02 021938.png
├── Screenshot 2025-12-02 022133.png
├── Screenshot 2025-12-02 023716.png
├── Screenshot 2025-12-02 023738.png
├── Screenshot 2025-12-02 023822.png
├── Screenshot 2025-12-02 024217.png
├── Screenshot 2025-12-02 130846.png
├── Screenshot 2025-12-02 192423.png
├── Screenshot 2025-12-02 192614.png
├── Screenshot 2025-12-02 192939.png
├── Screenshot 2025-12-02 193915.png
├── Screenshot 2025-12-02 194028.png
├── Screenshot 2025-12-03 012849.png
├── Screenshot 2025-12-03 013712.png
├── Screenshot 2025-12-03 013923.png
├── Screenshot 2025-12-03 015031.png
├── Screenshot 2025-12-03 015110.png
├── Screenshot 2025-12-03 015140.png
├── Screenshot 2025-12-03 015639.png
└── Screenshot 2025-12-03 015744.png
