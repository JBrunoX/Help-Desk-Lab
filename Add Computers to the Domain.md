# Add Computers to the Domain

To proceed, we’ll need a virtual machine (VM) or physical machine running **Windows 11 Pro** or **Enterprise**. For this guide, we’ll install the **Enterprise edition**, which includes a free 90-day trial.

---

## Steps

### Step 1: Download Windows 11 ISO
1. Go to [Microsoft's Evaluation Center](https://www.microsoft.com/en-us/evalcenter/download-windows-11-enterprise).  
2. Pick the **ISO download** in your preferred language.

---

### Step 2: Create a VM
1. Use the **Windows 11 ISO** you downloaded to set up a virtual machine.  
2. **Important:** When logging into a Microsoft account for the first time:  
   - **Avoid using a student email** or **any email tied to Azure**. These can prevent joining the domain or link it to Azure AD instead of Windows AD.

---

### Step 3: Configure Windows Server with a Static IP
Return to your **Windows Server VM** and follow these steps:

1. **Open Command Prompt**:  
   - In Windows Search, type `cmd` and press **Enter**.  
   - Type `ipconfig` and write down the **Default Gateway** for later.

   <p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/defaultGatewayIPconfig.png">
   </p>

2. **Set a Static IP**:  
   - In Windows Search, type `view network connections`.  
   - Right-click your **network adapter** > **Properties**.  
   - Double-click **Internet Protocol Version 4 (TCP/IPv4)**.  
   - Check **Use the following IP address**.  
   - Enter these details:  
     - **IP Address**: Match your Default Gateway but change the last number (e.g., if Gateway is `100.10.10.1`, use `100.10.10.10`).  
     - **Subnet Mask**: Should fill in automatically (if not, click the IP field and press Tab).  
   - Under **Use the following DNS server addresses**:  
     - **Preferred DNS Server**: `172.0.0.1` (loopback address).  
     - **Alternate DNS Server**: `8.8.8.8` (Google’s DNS).  

3. **Verify the Configuration**:  
   - In Command Prompt, type `ipconfig /all`.  
   - Check that the network addresses match what you entered.

4. **Configure the Enterprise VM’s DNS**:  
   - On the Enterprise VM, set:  
     - **Preferred DNS**: The Windows Server’s IP (e.g., `172.16.120.10`).  
     - **Alternate DNS**: `8.8.8.8`.

   <p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/IPv4%20Properties.png">
   </p>

5. **Test Connectivity**:  
   - In Command Prompt, type `ping <Windows Server IP>` (e.g., `ping 172.16.120.10`).  
   - Look for packets sent and received with **0% loss**.

---

### Step 4: Add the Enterprise VM to the Domain
On the **Enterprise VM**, follow these steps:

1. **Open System Properties**:  
   - Open File Explorer.  
   - Right-click **This PC** > **Properties**.

   <p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/pcProp.png">
   </p>

2. **Join the Domain**:  
   - Scroll to **Domain or workgroup** and click it.  
   - If prompted, sign in with:  
     - **Username**: `administrator`  
     - **Password**: The password you set earlier  
   - Click **Change** > Select **Domain**.  
   - Enter your domain name (e.g., the `.local` name from before).  
   - (Optional) Update the **Computer name** (e.g., `enterpriseVM`).  

   <p align="center">
     <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/domainSettingsJoin.png">
   </p>

   - If prompted again, sign in with:  
     - **Username**: `administrator`  
     - **Password**: The password you set earlier  
   - **If you get an error**:  
     - Recheck your static IP and DNS settings.  
     - Confirm you’re not using a school email (linked to Azure AD).  
   - Click **Restart now**.

3. **Verify Domain Membership**:  
   - After reboot, at the login screen, click **Other user** (bottom left).  
   - Enter the **username** and **password** of an Active Directory user you created.  
   - If you log in successfully, the domain join worked!

---

## All Done!
You’ve successfully added your Windows 11 Enterprise VM to the domain. Great work!
