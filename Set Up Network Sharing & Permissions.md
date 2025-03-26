# Set Up Network Sharing & Permissions

Let’s create a file-sharing setup for your domain, allowing users to share files and folders with the right permissions.

---

## Steps

### Step 1: Create a Shared Folder on Windows Server
1. Log into your **Windows Server VM**.  
2. Open **File Explorer** > **This PC** > **Local Disk (C:)**.  
3. Make a new folder:  
   - Right-click > **New** > **Folder**, or press `Ctrl+N`.  
   - Name it `Shared`.

---

### Step 2: Configure Sharing Permissions
1. Right-click the `Shared` folder > **Properties**.  
2. Go to the **Sharing** tab > **Advanced Sharing**.  
3. Check **Share this folder**.  
4. Click **Permissions** > **Add**.  
5. Type `domain` in the text field, then click **Check Names**.  
6. Select **Domain Users** (this lets all domain users access the folder).  

   <p align="center">
      <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/ShardFolderDomain.png">
   </p>

7. Click **Apply** > **OK** to return to the **Shared Properties** window.

---

### Step 3: Map the Network Drive on the Enterprise VM
1. Log into a user account on your **Enterprise VM**.  
2. Open **File Explorer**, right-click **This PC** > **Map network drive**.  
3. Pick a drive letter (e.g., `S` for "Shared").  
4. Get the folder path:  
   - On the Windows Server VM, open **Command Prompt** and type `hostname`.  
   - Write down the result (e.g., `WIN-XXXXX`).  
5. On the Enterprise VM, enter the path: `\\hostname\Shared` (replace `hostname` with your server’s hostname).  
6. Click **Finish**.  
   - You should now see the shared folder as a mapped drive.

---

### Step 4: Automate Network Sharing with a GPO
Mapped drives are temporary and vanish after a reboot. Let’s use a GPO to make it permanent.

1. **Create the GPO**:  
   - On the Windows Server, open **Group Policy Management (GPM)**.  
   - Right-click **Group Policy Objects** > **New**.  
   - Name it `Mapped Drives`.  
   - Right-click the new policy > **Edit**.

2. **Set Up Drive Mapping**:  
   - Go to **User Configuration** > **Preferences** > **Windows Settings**.  
   - Right-click **Drive Maps** > **New** > **Mapped Drive**.  
   - In **Location**, enter the path from Step 3 (e.g., `\\hostname\Shared`).  
   - Set **Label as**: `SHARED`.  
   - Set **Drive Letter**: `S`.  

   <p align="center">
      <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/mapDriveProp.png">
   </p>

   - Click **Apply** > **OK**.

3. **Link the GPO**:  
   - Drag the `Mapped Drives` GPO to the **Users** OU (like you did with earlier GPOs).

4. **Verify It Works**:  
   - On the Enterprise VM, go to **This PC**.  
   - Look under **Network Locations** for the mapped drive.  
   - **If it’s not there**:  
     - Open **Command Prompt**, type `gpupdate /force`, and reboot the VM.  

5. **Result**:  
   - Users now have permanent access to the shared folder. Since it’s under **User > Preferences**, they can remove or re-add it if needed.

---

## All Done!
You’ve set up file sharing and made it permanent with a GPO. Awesome work!
