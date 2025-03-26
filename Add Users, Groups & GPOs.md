# Set Up Active Directory with Groups, Users, and Group Policies

## Step 1: Open Active Directory Users and Computers
1. Log in to your Windows system.
2. In the search bar, type **"Active Directory Users and Computers"**.
3. Click the app when it appears in the search results.

---

## Step 2: Create Organizational Units (OUs)
Organizational Units help you organize your domain. Here’s how to set them up:

### Create Top-Level OUs
1. In the left pane, right-click your **domain name**.
2. Choose **New** > **Organizational Unit**.
3. Type **"USA"** as the name and click **OK**.
4. Repeat steps 1–3 to create two more OUs: **"Europe"** and **"Asia"**.  
   - **Note:** For this guide, we’ll only add items to the "USA" OU.

<p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/new%20OU.png">
</p>

### Add Sub-OUs Under "USA"
1. Right-click the **"USA" OU**.
2. Choose **New** > **Organizational Unit**.
3. Name it **"Computers"** and click **OK**.
4. Repeat steps 1–3 to create two more sub-OUs under "USA":  
   - **"Users"**  
   - **"Servers"**

---

## Step 3: Create Groups for Departments
Groups let you manage users by department. You’ll create both security and distribution groups.

### Add Security and Distribution Groups
1. In the left pane, right-click the **"Users" container**.
2. Choose **New** > **Group**.
3. Name it **"IT"**, set **Group Scope** to "Global", and **Group Type** to "Security". Click **OK**.
4. Create another group named **"DL - ITAdmins"**, set **Group Scope** to "Global", and **Group Type** to "Distribution". Click **OK**.

<p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/new%20Group.png">
</p>

### Add More Department Groups
Repeat the process to create three additional groups with **Global scope** and **Security type**:  
- **"Accounting"**  
- **"Sales"**  
- **"HR"**

---

## Step 4: Create Users
Now, add users and assign them to department groups.

### Add New Users
1. Right-click the **"Users" container** in the left pane.
2. Choose **New** > **User**.
3. Enter the user’s details (e.g., First Name, Last Name, User Logon Name), click **Next**, set a password, and click **OK**.

<p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/newUser.png">
</p>

4. Repeat steps 1–3 to create **four users total**.

### Assign Users to Groups
For each user:  
1. Right-click the user and select **"Add to a group"**.  
2. Type a group name (e.g., "IT", "Accounting", "Sales", or "HR") and click **OK**.  
   - Assign each user to a different department group.

---

## Step 5: Create Group Policy Objects (GPOs)
GPOs control settings for users and computers. For simplicity, we’ll apply these to the "USA" OU.

### Open Group Policy Management
1. In the Windows search bar, type **"Group Policy Management"**.
2. Click the app when it appears.

<p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/openGPM.png">
</p>

### Policy 1: Password Policy
1. Go to: **Forest > Domains > .local**, then right-click **"Group Policy Objects"**.
2. Select **New**, name it **"Password Policy"**, and click **OK**.
3. Right-click **"Password Policy"** and choose **"Edit"**.

<p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/editPolicy.png">
</p>

4. Navigate to: **Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy**.
5. Set these options:  
   - **Enforce password history:** 24  
   - **Minimum password length:** 12  
   - **Password must meet complexity requirements:** Enable  
   - **Maximum password age:** 90 days (this sets Minimum age to 30 days automatically)  
6. Click **Apply**, then **OK**.

### Policy 2: Password Lockout Policy
1. Right-click **"Group Policy Objects"**, select **New**, name it **"Password Lockout Policy"**, and click **OK**.
2. Right-click **"Password Lockout Policy"** and choose **"Edit"**.
3. Go to: **Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy**.
4. Set these options:  
   - **Account lockout duration:** 30 minutes  
   - **Account lockout threshold:** 5 invalid attempts  
   - **Allow Administrator account lockout:** Disable  
   - **Reset account lockout counter after:** 30 minutes  
5. Click **Apply**, then **OK**.

### Policy 3: Drive Mapping Policy
1. Right-click **"Group Policy Objects"**, select **New**, name it **"Drive Mapping Policy"**, and click **OK**.
2. Right-click **"Drive Mapping Policy"** and choose **"Edit"**.
3. Go to: **User Configuration > Preferences > Windows Settings**, then right-click **"Drive Maps"**.
4. Choose **New > Mapped Drive**.
5. Set:  
   - **Location:** `\\servername\foldername`  
   - **Drive Letter:** Pick one (e.g., "E")  
6. Click **Apply**, then **OK**.

### Policy 4: Default Wallpaper Policy
1. Right-click **"Group Policy Objects"**, select **New**, name it **"Default Wallpaper Policy"**, and click **OK**.
2. Right-click **"Default Wallpaper Policy"** and choose **"Edit"**.
3. Go to: **User Configuration > Policies > Administrative Templates > Desktop > Desktop**.
4. Right-click **"Desktop Wallpaper"**, then click **"Edit"**.
5. Set:  
   - **Enabled:** Check  
   - **Wallpaper Name:** "Default" (or your choice)  
   - **Wallpaper Style:** "Fill"  
6. Click **Apply**, then **OK**.

### Policy 5: Restrict Control Panel Access
1. Right-click **"Group Policy Objects"**, select **New**, name it **"Restrict Control Panel"**, and click **OK**.
2. Right-click **"Restrict Control Panel"** and choose **"Edit"**.
3. Go to: **User Configuration > Policies > Administrative Templates > Control Panel**.
4. Right-click **"Prohibit access to Control Panel and PC settings"** and click **"Edit"**.
5. Select **Enabled**, then click **Apply** and **OK**.

### Policy 6: Disable USB Storage
1. Right-click **"Group Policy Objects"**, select **New**, name it **"Disable USB Devices"**, and click **OK**.
2. Right-click **"Disable USB Devices"** and choose **"Edit"**.
3. Go to: **Computer Configuration > Policies > Administrative Templates > System > Removable Storage Access**.
4. Right-click **"All Removable Storage classes: Deny all access"** and click **"Edit"**.
5. Select **Enabled**, then click **Apply** and **OK**.

---

## All Done!
You’ve successfully set up your domain with OUs, groups, users, and applied GPOs to the "USA" OU. Your **Group Policy Objects** folder should look similar to this (minus a few policies we’ll add later):

<p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/GPO%20creations.png">
</p>

**Great job!** You’re ready to move on to the next steps when you’re ready.
