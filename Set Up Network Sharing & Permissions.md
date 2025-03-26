# Set Up Network Sharing & Permissions

Next, we’ll set up our file-sharing structure to enable sharing files and folders across our domain, ensuring proper permissions are applied.

## Steps

1. **Create a Shared Folder on Windows Server**
   - Log into your Windows Server VM.
   - Open **File Explorer** > **This PC** > **Local Disk (C:)**.
   - Create a new folder:
     - Right-click > **New** > **Folder**, or use the shortcut `Ctrl+N`.
     - Name it `Shared`.

2. **Configure Sharing Permissions**
   - Right-click the `Shared` folder > **Properties**.
   - Go to the **Sharing** tab > **Advanced Sharing**.
   - Check **Share this folder**.
   - Click **Permissions** > **Add**.
   - In the text field, type `domain`, then click **Check Names**.
   - Select **Domain Users** (this allows all domain users to access the folder).

<p align="center">
   <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/ShardFolderDomain.png">
</p>

   - Click **Apply** and **OK** to return to the **Shared Properties** window.

3. **Map the Network Drive on the Enterprise VM**
   - Log into a user account on your Enterprise VM.
   - Open **File Explorer**, right-click **This PC** > **Map network drive**.
   - Choose a drive letter (e.g., `S` to match "Shared").
   - Find the folder path:
     - On the Windows Server VM, open Command Prompt and type `hostname`.
     - Note the output (e.g., `WIN-XXXXX`).
   - Back on the Enterprise VM, enter the path: `\\hostname\Shared` (replace `hostname` with your server’s hostname).



   - Click **Finish**. You should now have access to the shared folder.

4. **Automate Network Sharing with a GPO**
   - Mapped drives are temporary and disappear after a reboot. For a permanent solution, use a GPO to automate this.
   - **Steps:**
     1. On the Windows Server, open **Group Policy Management (GPM)**.
        - Right-click **Group Policy Objects** > **New**.
        - Name it `Mapped Drives`.
        - Right-click the new policy > **Edit**.
     2. Configure the drive mapping:
        - Navigate to **User Configuration** > **Preferences** > **Windows Settings** > right-click **Drive Maps** > **New** > **Mapped Drive**.
        - In the **Location** field, enter the path used earlier (e.g., `\\hostname\Shared`).
        - Set **Label as**: `SHARED`.
        - Set **Drive Letter**: `S`.

<p align="center">
   <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/mapDriveProp.png">
</p>

 - Click **Apply** > **OK**.
  3. Apply the GPO:
      - Drag the `Mapped Drives` GPO to the **Users** OU (like previous GPOs).
    4. Verify the GPO:
      - On the Enterprise VM, go to **This PC**.
      - Check under **Network Locations** for the mapped drive.
      - If it’s not visible:
         - Open Command Prompt, type `gpupdate /force`, and reboot the machine.
  5. **Result**: Users now have permanent access to the shared folder. Since it’s under **User > Preferences**, they can optionally remove or re-add it.
