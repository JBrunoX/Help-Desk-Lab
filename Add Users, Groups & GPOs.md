# Populate Active Directory with Groups, Users, and GPOs

## Step 1: Open Active Directory Users and Computers
- Log back into Windows.
- In the search bar, type "Active Directory Users and Computers" and click it when it appears.

---

## Step 2: Create Organizational Units (OUs)
- **Create Top-Level OUs:**
  1. On the left, right-click your domain name.
  2. Select "New" > "Organizational Unit."
<p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/new%20OU.png">
</p>

  3. Name it "USA" and click OK.
  4. Repeat this process to create two more OUs: "Europe" and "Asia."
     - **Note:** We’ll only populate the "USA" OU for this simulation.
- **Add Sub-OUs to USA:**
  1. Right-click the "USA" OU.
  2. Select "New" > "Organizational Unit."
  3. Name it "Computers" and click OK.
  4. Repeat to create two more OUs under "USA": one called "Users" and another called "Servers."

---

## Step 3: Create Groups (Departments)
- **Add Security and Distribution Groups:**
  1. Right-click the "Users" container in the left pane.
  2. Select "New" > "Group."
<p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/new%20Group.png">
</p>
 

  3. Name it "IT," set Group Scope to "Global," and Group Type to "Security." Click OK.
  4. Create another group named "DL - ITAdmins," set Group Scope to "Global," and Group Type to "Distribution." Click OK.
- **Repeat for Other Departments:**
  - Create three more groups with Global scope and Security type:
    - "Accounting"
    - "Sales"
    - "HR"

---

## Step 4: Create Users
- **Add New Users:**
  1. Right-click the "Users" container in the left pane.
  2. Select "New" > "User."
  3. Fill in all fields (e.g., First Name, Last Name, User logon Name), click Next, set a password, and click OK.

<p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/newUser.png">
</p>

  4. Repeat this process three more times to create a total of four users.
- **Assign Users to Groups:**
  - For each user:
    1. Right-click the user, select "Add to a group."
    2. Type the group name (e.g., "IT," "Accounting," "Sales," or "HR") and click OK.
    - Assign each user to a different department group.

---

## Step 5: Create Group Policy Objects (GPOs)
**Note:** These policies can be applied at the `.local` domain level with exclusions, but for simplicity, we’ll apply them to the "USA" OU since that’s our focus.

- **Open Group Policy Management:**
  - In the Windows search bar, type "Group Policy Management" and click it.
<p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/openGPM.png">
</p>

### Password Policy
1. Navigate to: Forest > Domains > .local < right-click "Group Policy Objects."

<p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/newGPO.png">
</p>

2. Select "New," name it "Password Policy," and click OK.
3. Right-click "Password Policy" under Group Policy Objects and click "Edit."

<p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/editPolicy.png">
</p>

4. Go to: Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy.
5. Configure these settings:
   - **Enforce password history:** Set to 24.
   - **Minimum password length:** Set to 12.
   - **Password must meet complexity requirements:** Enable.
   - **Maximum password age:** Set to 90 days (this auto-sets Minimum password age to 30 days).
6. Click Apply, then OK.

### Password Lockout Policy
1. Right-click "Group Policy Objects," select "New," name it "Password Lockout Policy," and click OK.
2. Right-click "Password Lockout Policy" and click "Edit."
3. Go to: Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy.
4. Configure these settings:
   - **Account lockout duration:** Set to 30 minutes.
   - **Account lockout threshold:** Set to 5 invalid logon attempts.
   - **Allow Administrator account lockout:** Disable.
   - **Reset account lockout counter after:** Set to 30 minutes.
5. Click Apply, then OK.

### Drive Map Policy
1. Right-click "Group Policy Objects," select "New," name it "Drive Mapping Policy," and click OK.
2. Right-click "Drive Mapping Policy" and click "Edit."
3. Go to: User Configuration > Preferences > Windows Settings > right-click "Drive Maps."
4. Select "New" > "Mapped Drive."
5. Configure:
   - **Location:** Enter `\\servername\foldername`.
   - **Drive Letter:** Choose one (e.g., I picked "E").
6. Click Apply, then OK.

### Default Wallpaper Policy
1. Right-click "Group Policy Objects," select "New," name it "Default Wallpaper Policy," and click OK.
2. Right-click "Default Wallpaper Policy" and click "Edit."
3. Go to: User Configuration > Policies > Administrative Templates > Desktop > Desktop.
4. Right-click "Desktop Wallpaper" on the right, then click "Edit."
5. Configure:
   - **Enabled:** Select.
   - **Wallpaper Name:** Enter "Default" (or your preferred name).
   - **Wallpaper Style:** Choose "Fill."
6. Click Apply, then OK.

### Restrict Access to Control Panel Policy
1. Right-click "Group Policy Objects," select "New," name it "Restrict Control Panel," and click OK.
2. Right-click "Restrict Control Panel" and click "Edit."
3. Go to: User Configuration > Policies > Administrative Templates > Control Panel.
4. Right-click "Prohibit access to Control Panel and PC settings" and click "Edit."
5. Select "Enabled," then click Apply and OK.

### Disable USB Storage Policy
1. Right-click "Group Policy Objects," select "New," name it "Disable USB Devices," and click OK.
2. Right-click "Disable USB Devices" and click "Edit."
3. Go to: Computer Configuration > Policies > Administrative Templates > System > Removable Storage Access.
4. Right-click "All Removable Storage classes: Deny all access" and click "Edit."
5. Select "Enabled," then click Apply and OK.

---

**Congratulations!** You’ve populated your domain with OUs, groups, and users and applied GPOs to the USA OU.

**Your Group Policy Objects OU should look similar to the image below, except for the User Rights Policy, Mapped Drives, and Printer Deployment Policy. Those will be added soon, so don't worry.

<p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/GPO%20creations.png">
</p>
