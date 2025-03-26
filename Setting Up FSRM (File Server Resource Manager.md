# Setting Up FSRM (File Server Resource Manager)

We’ll use **File Server Resource Manager (FSRM)** to manage and classify data on our file server. This setup includes notifications to alert users when folders near capacity, helping them clean up storage and avoid full disks.

---

## Steps

### Step 1: Install FSRM on Windows Server
1. On your **Windows Server**, open **Server Manager**.  
2. Click **Manage** > **Add Roles and Features** > **Next** > **Next**.  
3. Expand **File and Storage Services** (one of the installed roles) > **File and iSCSI Services**.  
4. Check **File Server Resource Manager** and click **Add Features**.  
5. Click **Next** > **Next** > **Install**.  
6. When done, click **Close**.  
7. Open **FSRM**:  
   - If it’s not showing, right-click a blank area and select **Refresh**.

---

### Step 2: Create a Quota for the Shared Drive
1. In FSRM, go to **Quota Management**.  
2. Right-click **Quotas** > **Create Quota**.  
3. Set the **Quota Path**:  
   - Click **Browse** > **Local Disk (C:)** > **Shared**.  
4. Choose **Define custom quota properties** > **Custom Properties**.  
5. Keep **Hard Quota** selected and set the limit to `100 MB`.  
6. Add a notification:  
   - Click **Add**.  
   - Change the threshold from `85` to `80` (notifies at 80% usage).  
   - Set the description to `Disk Usage 80%`.  
   - Check **Send e-mail to the following administrators** and enter the `ITAdmin` distribution list.  
7. Click **OK** > **Yes** > **OK** until you’re back at the **Create Quota** window, then click **Create**.  
8. When prompted, create a template:  
   - Name it `SHARED` and click **OK**.  
   - It should look like this:  

   <p align="center">
      <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/QuotaTemplate.png">
   </p>

---

### Step 3: Set Up File Screening for the Shared Folder
1. In FSRM, go to **File Screening Management**.  
2. Right-click **File Screens** > **Create File Screen**.  
3. Set the **File Screen Path** to the shared folder (e.g., `C:\Shared`).  
4. Select **Define custom file screen properties** > **Custom Properties**.  
5. Check these file types to block:  
   - **Audio and Video Files**  
   - **Compressed Files**  
   - **Executable Files**  
   - **Image Files**  
   - **Web Page Files**  
   - This limits large file types to save storage space.  

   <p align="center">
      <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/fileScreeningShared.png">
   </p>

6. When prompted, create a template:  
   - Name it `SHARED` and click **OK**.

---

## All Done!
You’ve successfully configured your file server with FSRM. Great job setting up quotas and file screening!
