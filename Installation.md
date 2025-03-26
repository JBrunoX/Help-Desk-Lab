# Installation Guide

## Step 1: Install VMware Workstation Pro

### **Download VMware Workstation Pro**
1. Visit [VMware's download page](https://knowledge.broadcom.com/external/article/344595/downloading-and-installing-vmware-workst.html).  
2. Scroll to **"Download VMware Workstation Pro."**  
   <p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/dd1e4c7f9b8ac541c5a1cdf466eeace5e9624bca/images/download%20VMware.png">
   </p>
3. **Sign in or create a free Broadcom account** when prompted.  

### **Choose Your Version**
<p align="center">
  <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/vmware%20version.png">
</p>

- **Windows users:** Select **"VMware Workstation Pro 17.0 for Windows."**  
- **Linux users:** Select **"VMware Workstation Pro 17.0 for Linux."**  
- If unavailable, use [this alternative link](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware%20Workstation%20Pro&freeDownloads=true) and download the latest version (could be newer than 17.0).  

### **Install VMware Workstation Pro**
1. Open the downloaded file.  
2. Follow the installation wizard.  
3. If you encounter issues, check [Broadcom's troubleshooting guide](https://knowledge.broadcom.com/external/article?articleNumber=387947).  

---

## Step 2: Download Windows Server 2025
1. Go to the [Microsoft Evaluation Center](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2025).  
2. Select the **ISO download option** in your preferred language.  
   <p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/windows2025PickLang.png">
   </p>
3. **Save the ISO file** to your computer.  

---

## Step 3: Create a Virtual Machine in VMware Workstation Pro

### **Launch VMware**
- Open VMware Workstation Pro and select **"Personal use"** to keep it free.  

### **Set Up the Virtual Machine**
1. Click **"Create a New Virtual Machine."**  
   <p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/df25d2e53a302b349877f7a65f90de16289c4079/images/createNewVM.png">
   </p>
2. Select **"Typical (recommended)"** and click **Next.**  
3. Choose **"I will install the operating system later"** and click **Next.**  
4. Set **Microsoft Windows** as the Guest OS and **Windows Server 2025** as the version, then click **Next.**  
5. Name your VM (e.g., **"WinServer2025"**) and click **Next.**  

### **Configure VM Hardware**
1. **Set disk size** (recommended: **70+ GB**, I used **80 GB**).  
2. Leave **"Split virtual disk into multiple files"** selected and click **Next.**  
3. Click **"Customize Hardware."**  
4. **Increase RAM** (recommended: **4GB (4096MB)**, I used **6GB (6144MB)** since my system has 48GB total).  
5. **Set processors:**  
   - **Number of processors:** `1`  
   - **Number of cores per processor:** `2`  
6. **Mount the Windows Server 2025 ISO:**  
   - Select **"CD/DVD (SATA)."**  
   - Choose **"Use ISO image file."**  
   - Click **"Browse,"** select the ISO file, then click **"Open."**  
   <p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/a3050e8f93eda00b510f6567602ef9d5c39a255c/images/customizeHardwireVMServer.png">
   </p>
7. Click **"Close,"** then **"Finish."**  

### **Start the Virtual Machine**
- Click **"Power on this virtual machine."**  
- **Quickly press any key** to boot from the ISO. If you miss it, you may see a **"Time Out"** or **"EFI Network"** error.  
- **If boot fails:**  
  - Right-click the VM name > **Power** > **Shut Down Guest.**  
  - Restart the VM and press any key repeatedly to enter setup.  

---

## Step 4: Install Windows Server 2025

### **Setup Process**
1. Select your **language and time format,** then click **Next.**  
2. Choose your **keyboard layout,** then click **Next.**  

### **Install Windows Server**
1. Click **"Install Now."**  
2. Check **"I agree everything will be deleted..."** and click **Next.**  
3. Choose **"Standard Evaluation (Desktop Experience)"** for a GUI, then click **Next.**  
4. Accept the license terms and click **Next.**  
5. Select your disk and click **Next.**  
6. Click **"Install."**  

### **Complete Installation**
- Wait for the process to finish.  
- Set an **administrator password** and log in.  
  <p align="center">
    <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/serverLogIn.png">
  </p>

---

## Step 5: Install Active Directory

### **Open Server Manager**
- If it's not open, search **"Server Manager"** in the Start menu.  

### **Add Active Directory Domain Services**
1. Click **"Manage"** (top-right) > **"Add Roles and Features."**  
2. Click **Next** (keep "Role-based or feature-based installation" selected).  
3. Click **Next** twice until you reach the roles list.  
4. Select **"Active Directory Domain Services."**  
5. Click **"Add Features"** when prompted.  
   <p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/adFeatureAdd.png">
   </p>
6. Keep clicking **Next** until you reach the **Install** button, then click it.  

### **Promote the Server to a Domain Controller**
1. After installation, click the **notification flag** and select **"Promote this server to a domain controller."**  
2. Select **"Add a new forest"** and enter a domain name (e.g., **HelpDeskSim.local**).  
   - The **".local"** is required.  
3. Click **Next** and wait for the wizard to load.  
4. Set a **DSRM password** (used for domain recovery).  
5. Keep clicking **Next** until you reach **"Install,"** then click it.  

### **Final Steps**
- The system will **restart** and log you out.  
- After reboot, log in with your **admin credentials.**  

---

## 🎉 **Congratulations!**
You’ve successfully installed **Windows Server 2025** with **Active Directory** in a VMware virtual machine.
