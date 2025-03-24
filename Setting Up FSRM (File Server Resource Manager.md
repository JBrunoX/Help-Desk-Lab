# Setting Up FSRM (File Server Resource Manager)

FSRM will be used to manage and classify data stored on our file server. We’ll set up notifications to alert users when folders are nearing capacity, encouraging them to clean up storage and prevent full disks.

## Steps

1. **Install FSRM on Windows Server**
   - On the Windows Server, open **Server Manager**.
   - Click **Manage** > **Add Roles and Features** > **Next** > **Next**.
   - Expand **File and Storage Services** (_ of _ installed) > **File and iSCSI Services**.
   - Check **File Server Resource Manager** and click **Add Features**.
   - Click **Next** > **Next** > **Install**.
   - After installation, click **Close**.
   - Open **FSRM** (if it’s not visible, right-click a blank area and select **Refresh**).

2. **Create a Quota for the Shared Drive**
   - In FSRM, go to **Quota Management** > right-click **Quotas** > **Create Quota**.
   - Set the **Quota Path** to the shared drive:
     - Click **Browse** > **Local Disk (C:)** > **Shared**.
   - Click **Define custom quota properties** > **Custom Properties**.
   - Keep **Hard Quota** selected and set the limit to `10 GB`.
   - Configure notification:
     - Click **Add**, change the threshold from `85` to `80` (notifies at 80% usage).
     - Set the description to `Disk Usage 80%`.
     - Check **Send e-mail to the following administrators** to notify the `ITAdmin` distribution list.
   - Click **OK** > **Yes** > **OK** until back at the **Create Quota** window, then click **Create**.
   - When prompted, create a template:
     - Name it `SHARED` and click **OK**.

3. **Set Up File Screening for the Shared Folder**
   - In FSRM, go to **File Screening Management** > right-click **File Screens** > **Create File Screen**.
   - Set the **File Screen Path** to the shared folder (e.g., `C:\Shared`).
   - Select **Define custom file screen properties** > **Custom Properties**.
   - Check the following file types to block:
     - **Audio and Video Files**
     - **Compressed Files**
     - **Executable Files**
     - **Image Files**
     - **Web Page Files**
   - This restricts large file types to minimize storage usage.
   - When prompted, create a template:
     - Name it `SHARED` and click **OK**.
