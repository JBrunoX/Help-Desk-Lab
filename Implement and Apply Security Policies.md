# Implement and Apply Security Policies

Let’s secure our domain by setting up user rights to control who can log in and how.

---

## Steps

### Step 1: Create a New GPO
1. Log into your **Windows Server**.  
2. Open **Group Policy Management (GPM)**.  
3. Right-click your domain (e.g., `domain.local`) > **Create a GPO in this domain, and Link it here...**.  
4. Name it `User Rights Policy` and click **OK**.

---

### Step 2: Edit the User Rights Policy
1. Right-click **User Rights Policy** under `.local` > **Edit**.  

   <p align="center">
      <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/userRightsEdit.png">
   </p>

---

### Step 3: Configure User Rights Assignments
1. Go to **Computer Configuration** > **Policies** > **Windows Settings** > **Security Settings** > **Local Policies** > **User Rights Assignment**.  

2. **Deny log on locally**:  
   - Double-click **Deny log on locally**.  
   - Check **Define these policy settings**.  
   - Click **Add User or Group** > **Browse**.  
   - Type `HR`, click **Check Names** (this fills in the HR group path).  
   - Click **OK** > **Apply** > **OK**.

3. **Allow log on through Remote Desktop Services**:  
   - Double-click **Allow log on through Remote Desktop Services**.  
   - Check **Define these policy settings**.  
   - Click **Add User or Group** > **Browse**.  
   - Type `IT`, click **Check Names** (this fills in the IT group path).  
   - Click **OK** > **Apply** > **OK**.

   <p align="center">
      <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/remoteDeskPolicy.png">
   </p>

---

### Step 4: Test the Policies
1. **Test "Deny log on locally"**:  
   - Try logging into the Windows Server or Enterprise VM with an **HR department user**.  
   - **Expected Result**: A message says, *"The sign-in method you're trying to use isn't allowed..."*.

2. **Test "Allow log on through Remote Desktop Services"**:  
   - Log into the Enterprise VM with a **non-HR user**.  
   - In Windows Search, type **Remote Desktop Connection** and open it.  
   - Enter your Windows Server’s hostname (e.g., `WIN-XXXXX`) and click **Connect**.  
   - **Expected Result**: An error says, *"Remote Desktop can't connect to the remote computer for one of these reasons..."*.

3. **Success Check**:  
   - If both tests show these errors, your policies are working correctly!

---

## All Done!
You’ve successfully set up and applied user rights policies. Great work securing your domain!
