# Installation

## Step 1: Install VMware Workstation Pro

- **Download VMware Workstation Pro:**
  - Visit [VMware's download page](https://knowledge.broadcom.com/external/article/344595/downloading-and-installing-vmware-workst.html).
  - Scroll to "Download VMware Workstation Pro."
  - Login or create a free Broadcom account when prompted.
- **Choose Your Version:**
  - For Windows users: Select "VMware Workstation Pro 17.0 for Windows."
  - For Linux users: Select "VMware Workstation Pro 17.0 for Linux."
  - If you don’t see these options, use this [alternate link](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware%20Workstation%20Pro&freeDownloads=true), pick the latest release, agree to the Terms and Conditions, and click the download icon on the right.
- **Install It:**
  - Once downloaded, open the file and follow the installation wizard.
  - If you encounter issues, refer to this [Broadcom troubleshooting article](https://knowledge.broadcom.com/external/article?articleNumber=387947).

---

## Step 2: Download Windows Server 2025

- Go to the [Microsoft Evaluation Center](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2025).
- Select the ISO download option in your preferred language.
- Save the file to your computer.

---

## Step 3: Create a Virtual Machine in VMware Workstation Pro

- **Open VMware:**
  - Launch VMware Workstation Pro and select "Personal use" to keep it free.
- **Set Up the VM:**
  1. Click "Create a New Virtual Machine."
  2. Choose "I will install the operating system later" and click Next.
  3. For the Guest Operating System, select "Windows Server 2025" as the Version, then click Next.
  4. Name your virtual machine (e.g., "WinServer2025") and click Next.
  5. Set the disk size:
     - Recommend at least 60 GB. (I used 80 GB since I had extra space.)
     - Click Next.
- **Customize Settings:**
  1. At "Ready to Create Virtual Machine," click "Customize Hardware."
  2. Adjust memory:
     - The default is 2 GB (2048 MB). I recommend increasing it to 4 GB (4096 MB).
     - I used 6 GB (6144 MB) since my system has 48 GB total.
  3. Adjust processors:
     - Change "Number of processors" to 2.
     - Leave "Number of cores per processor" at 1.
  4. Add the ISO:
     - Click "CD/DVD (SATA)," select "Use ISO image file," then click "Browse."
     - Choose the Windows Server 2025 ISO you downloaded, then click "Open."
  5. Click "Close," then "Finish."
- **Start the VM:**
  - Select "Power on this virtual machine."
  - Quickly press any key repeatedly to boot from the ISO. (If you miss it, you’ll see a "Time Out" or "EFI Network" error.)
  - **If You Miss the Boot:**
    - Right-click your VM name on the left, select "Power" > "Shut Down Guest."
    - Restart the VM and try again, spamming a key to load the setup.

---

## Step 4: Install Windows Server 2025

- **Initial Setup:**
  - Select your language and time format, then click Next.
  - Choose your keyboard layout, then click Next.
- **Install the OS:**
  1. Click "Install Now."
  2. Check "I agree everything will be deleted..." and click Next.
  3. Select "Standard Evaluation (Desktop Experience)" for a GUI, then click Next.
  4. Accept the license terms and click Next.
  5. Choose your disk, click Next, then click "Install."
- **Wait and Finish:**
  - The installation will take some time. Once complete, set a password and log in.

---

## Step 5: Install Active Directory

- **Open Server Manager:**
  - If it’s not already open, click the search bar at the bottom, type "Server Manager," and select it.
- **Add Roles:**
  1. In the top right, click "Manage" > "Add Roles and Features."
  2. Click Next (keep "Role-based or feature-based installation" selected).
  3. Click Next twice more to reach the roles list.
  4. Check "Active Directory Domain Services," then click "Add Features" when prompted.
  5. Keep clicking Next until you see "Install," then click it.
- **Promote to Domain Controller:**
  1. After installation, click the notification flag and select "Promote this server to a domain controller."
  2. Choose "Add a new forest" and enter a domain name (e.g., "HelpDeskSim.local"). The ".local" is required.
  3. Click Next and wait for the wizard to load.
  4. Set a DSRM password (this is your domain recovery password).
  5. Keep clicking Next until you reach "Install," then click it.
- **Final Notes:**
  - The system will restart and log you out. Once it’s back up, log in with your password.

---

**Congratulations!** You’ve successfully installed Windows Server 2025 with Active Directory in a virtual machine.
