# Implement and Apply Security Policies

Security is critical, so we’ll secure our domain by configuring user rights.

## Steps

1. **Create a New GPO**
   - Log into Windows Server and open **Group Policy Management (GPM)**.
   - Right-click your domain (e.g., `domain.local`) > **Create a GPO in this domain, and Link it here...**.
   - Name it `User Rights Policy` and click **OK**.

2. **Edit the User Rights Policy**
   - Right-click **User Rights Policy** under `.local` > **Edit**.

3. **Configure User Rights Assignments**
   - Navigate to **Computer Configuration** > **Policies** > **Windows Settings** > **Security Settings** > **Local Policies** > **User Rights Assignment**.
   - **Deny log on locally:**
     - Double-click **Deny log on locally**.
     - Check **Define these policy settings**.
     - Click **Add User or Group** > **Browse**.
     - Type `HR`, click **Check Names** (this populates the path to the HR group).
     - Click **OK** > **Apply** > **OK**.
   - **Allow log on through Remote Desktop Services:**
     - Double-click **Allow log on through Remote Desktop Services**.
     - Check **Define these policy settings**.
     - Click **Add User or Group** > **Browse**.
     - Type `IT`, click **Check Names** (this populates the path to the IT group).
     - Click **OK** > **Apply** > **OK**.

4. **Test the Policies**
   - **Test "Deny log on locally":**
     - Attempt to log into either the Windows Server or Enterprise VM using a user from the HR department.
     - Expected result: A message stating, *"The sign-in method you're trying to use isn't allowed..."*.
   - **Test "Allow log on through Remote Desktop Services":**
     - Log into the Enterprise VM with a non-HR user.
     - In Windows Search, type **Remote Desktop Connection** and open it.
     - Enter your Windows Server’s hostname (e.g., `WIN-XXXXX`) and click **Connect**.
     - Expected result: An error message stating, *"Remote Desktop can't connect to the remote computer for one of these reasons..."*.
   - If both tests produce these errors, the policies are configured correctly.
