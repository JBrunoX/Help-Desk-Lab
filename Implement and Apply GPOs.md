# Implement and Apply GPOs

Let’s put the Group Policy Objects (GPOs) we created earlier into action.

---

## Steps

### Step 1: Access Group Policy Management
1. Log back into your **Windows Server**.  
2. Open **Group Policy Management**.  
3. We’ll start by restricting Control Panel access for our users.

---

### Step 2: Link GPOs to Organizational Units (OUs)
1. In the left pane, go to **Group Policy Objects**.  
2. Find **Restrict Control Panel**, then click and drag it to **USA** > **Users**.  
   - This works because it’s a **User Configuration** policy.  
3. Repeat for these policies:  
   - **Desktop Wallpaper**  
   - **Disable USB**  
   - **Password**  
   - **Drive Mapping**  
   - **Note:** Drag each policy to the right OU based on its configuration type (User or Computer).  
4. When done, your left pane should look similar to this (minus a few policies we’ll add later):  

   <p align="center">
      <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/GPO%20clickDrag.png">
   </p>

---

### Step 3: Move the Computer to the Correct OU and Test Policies
When we added the computer to the domain, it landed in the generic **Computers** container. Let’s move it to the **Computers** OU under **USA** and test the policies.

1. **Open Active Directory Users and Computers**:  
   - Go to **Builtin** > **Computers**.  
   - Find your Enterprise computer (e.g., `enterpriseVM`).  

2. **Move the Computer**:  
   - Right-click it > **Move**.  
   - Select **USA** > **Computers** > **OK**.  
   - Check **USA** > **Computers** to confirm it’s there.  
   - If it’s not showing, right-click a blank space and hit **Refresh**.

3. **Add a Description**:  
   - Right-click the computer > **Properties**.  
   - Type a description (e.g., `Shared Desktop`) and click **OK**.

4. **Test the Restrict Control Panel Policy**:  
   - Log into a user account on your **Enterprise VM**.  
   - Try opening the Control Panel:  
     - Search for **Control Panel** in the Windows search bar.  
   - **Expected Result:**

   <p align="center">
      <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/deniedControlPanel.png">
   </p>

5. **If the Policy Doesn’t Apply Yet**:  
   - GPOs update every 90 minutes (with a random 30-minute offset).  
   - To apply it now:  
     - On the Enterprise VM, open **Command Prompt**.  
     - Type `gpupdate /force` and wait for it to finish.  
   - Retest the Control Panel access.

6. **Test the Other Policies**:  
   - Check that **Desktop Wallpaper**, **Disable USB**, **Password**, and **Drive Mapping** work as expected.

---

## All Done!
You’ve successfully linked and applied your GPOs. Nice job!
