# Add Computers to the Domain

For this next step, we need either a virtual machine (VM) or a physical machine running Windows 11 Pro or Enterprise. In this simulation, we'll use the Enterprise edition, which offers a free 90-day trial.

## Steps

1. **Download Windows 11 ISO**
   - Visit [Microsoft's evaluation center](https://www.microsoft.com/en-us/evalcenter/download-windows-11-enterprise).
   - Select the ISO download in your preferred language.

2. **Create a VM**
   - Use the Windows 11 ISO you just downloaded to create a virtual machine.
   - Reminder: When logging into a Microsoft account for the first time:
     - **Do not use a student email**, as it may prevent adding the computer to the domain or link it to Azure AD instead of Windows AD.

3. **Configure Windows Server with a Static IP**
   - Return to your Windows Server VM.
   - **Steps:**
     1. Open Command Prompt:
        - Use Windows Search, type `cmd`, and press Enter.
        - Type `ipconfig` and note the **Default Gateway** for later use.
     2. Set a static IP:
        - In Windows Search, type `view network connections`.
        - Right-click your network adapter > **Properties** > Double-click **Internet Protocol Version 4 (TCP/IPv4)**.
        - Select **Use the following IP address**.
        - Enter a static IP:
          - Use the same values as your Default Gateway, but change the last octet (e.g., if Gateway is `100.10.10.1`, use `100.10.10.10`).
          - The **Subnet Mask** should auto-populate (if not, click the IP field and press Tab).
        - Under **Use the following DNS server addresses**:
          - **Preferred DNS Server**: `172.0.0.1` (loopback address).
          - **Alternate DNS Server**: `8.8.8.8` (Google's DNS).
     3. Verify the configuration:
        - In Command Prompt, type `ipconfig /all`.
        - Confirm the network addresses match what you set.
     4. Configure the Enterprise VM's DNS:
        - Set the **Preferred DNS** to the Windows Server's IP (e.g., `172.16.120.10`).
        - Set the **Alternate DNS** to `8.8.8.8`.
     5. Test connectivity:
        - In Command Prompt, type `ping <Windows Server IP>` (e.g., `ping 172.16.120.10`).
        - You should see packets sent and received with 0% loss.

4. **Add the Enterprise VM to the Domain**
   - On the Enterprise VM:
     1. Open File Explorer:
        - Right-click **This PC** > **Properties**.
        - Scroll to **Domain or workgroup** and click it.
     2. Join the domain:
        - Click **Change** > Select **Domain**.
        - Enter your domain name (e.g., the `.local` name from earlier).
        - Optionally, update the **Computer name** (e.g., `enterpriseVM`).
        - Sign in with:
          - **Username**: `administrator`.
          - **Password**: The password you set up.
        - If an error occurs:
          - Double-check your static IP and DNS settings.
          - Ensure you're not using a school email (linked to Azure AD).
        - Click **Restart now**.
     3. Verify domain membership:
        - After reboot, at the login screen, select **Other user** (bottom left).
        - Enter the username and password of an Active Directory user you created.
        - Successful login confirms the domain was joined correctly.
