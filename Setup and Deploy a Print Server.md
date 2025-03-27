# Setup and Deploy a Print Server

Let’s add a print server to our domain and deploy it to users using Group Policy.

---

## Steps

### Step 1: Install and Configure the Print Server
1. On your **Windows Server**, open **Server Manager**.  
2. Click **Manage** (top right) > **Add Roles and Features** > **Next**.  
3. Keep **Role-based or feature-based installation** selected > **Next** > **Next**.  
4. Check **Print and Document Services** > **Add Features**.  
5. Click **Next** until you see **Install**, then click **Install**.  
6. When finished, click **Close**.  
7. Go to **Tools** (top right) > **Print Management**.  
8. Expand **Print Servers** > **hostname (local)** > right-click **Printers** > **Add Printer**.  

   <p align="center">
      <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/addPrinter.png">
   </p>

   - **If you get an error**: Ensure the Print Spooler is running:  
     - Press `Win + R`, type `services.msc`, and press **Enter**.  
     - Find **Print Spooler**, double-click it, and check **Service status** says **Running**.  
     - If it’s **Stopped**, click **Start**.  
     - Or, in Command Prompt, type `Get-Service -Name Spooler`. If stopped, type `Start-Service -Name Spooler`.

9. In the **Add Printer** wizard:  
   - Select **Add a new printer using an existing port**.  
   - Choose **Local Port** from the dropdown (if your printer is plugged in) > **Next**.  
   - Pick **Use an existing printer driver on the computer** > **Next**.  
   - Name your printer something clear (e.g., `OfficePrinter`).  
   - Add details:  
     - **Location**: `Main Office`  
     - **Comment**: `This is the printer in the main office`  
   - Click **Next** until you see **Print a test page**, then test it to confirm it works.  
10. Right-click the printer name > **Properties** > **Sharing** tab.  
    - Check **List in the directory** > **Apply** > **OK**.

---

### Step 2: Add the Printer to the Domain
1. Open **Active Directory Users and Computers**.  
2. Right-click **USA** > **New** > **Organizational Unit**.  
3. Name it `Printers` > **OK**.  
4. Right-click the **Printers OU** > **New** > **Group**.  
5. Name it after your printer (e.g., `OfficePrinter`).  
6. Add a description: `This deploys OfficePrinter` > **Apply** > **OK**.  

   <p align="center">
      <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/officePrinter.png">
   </p>

---

### Step 3: Create a GPO to Deploy the Printer
1. Open **Group Policy Management (GPM)**.  
2. Right-click **Group Policy Objects** > **New**.  
3. Name it `Printer Deployment Policy` > **OK**.  
4. Right-click **Printer Deployment Policy** > **Edit**.  
5. Go to **User Configuration** > **Preferences** > **Control Panel Settings** > **Printers**.  
6. Right-click **Printers** > **New** > **Shared Printer**.  
7. Next to **Share path**, click the three dots (`…`), find your printer in the search results, and click **OK**.  
8. Go to the **Common** tab:  
   - Check **Item-level targeting** > click **Targeting**.  
   - Click **New Item** > **Security Group**.  
   - Click the three dots (`…`) next to the Group box, type your printer group name (e.g., `OfficePrinter`), and click **OK**.  
9. Ensure **Action** is set to **Update** > **Apply** > **OK**.  

   <p align="center">
      <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/ofice%20printer%20targeting.png">
   </p>

10. Drag the **Printer Deployment Policy** GPO to the **Users** OU.

---

### Step 4: Verify the Printer Deployment
1. Log into a user account on your **Enterprise VM**.  
2. Open **Command Prompt** and type `gpresult /r`.  
   - Look under **Applied Group Policy Objects** for `Printer Deployment Policy`.  
   - **If it’s not there**: Type `gpupdate /force`, then reboot the VM.  
3. After reboot, run `gpresult /r` again to confirm it’s applied.  
4. Open **Settings** > **Printers & Scanners**.  
   - Wait for settings to update if needed.  
   - Check that your printer (e.g., `OfficePrinter`) is listed.

---

## All Done!
You’ve set up a print server and deployed it to users with a GPO. Awesome work!
