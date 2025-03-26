# Implement and Apply GPOs

Now we will put the GPOs we previously created into effect.

## Steps

1. **Access Group Policy Management**
   - Log back into Windows Server.
   - Open **Group Policy Management**.
   - Let’s start by restricting Control Panel access for our Users.

2. **Link GPOs to Organizational Units (OUs)**
   - In the left pane, navigate to **Group Policy Objects** > **Restrict Control Panel**.
   - Click and drag this policy to **USA** > **Users** (since it was created using User Configuration).
   - Repeat for the other policies:
     - **Desktop Wallpaper**
     - **Disable USB**
     - **Password**
     - **Drive Mapping**
   - **Note**: Drag each policy to the appropriate OU based on its configuration type (User or Computer).
   - By the end your left pane just look similar to this except for a few policies that wwe will add later.

<p align="center">
   <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/GPO%20clickDrag.png">
</p>

4. **Move the Computer to the Correct OU and Test Policies**
   - When we added our computer to the domain, it was placed in the generic **Computers** container. We need to move it to the **Computers** OU.
   - **Steps:**
     1. Open **Active Directory Users and Computers**.
        - Go to **Builtin** > **Computers**.
        - Locate the Enterprise computer (e.g., `enterpriseVM`).
     2. Move the computer:
        - Right-click it > **Move** > **USA** > **Computers** > **OK**.
        - Navigate to **USA** > **Computers** to verify it’s there.
        - If it’s not visible, right-click a blank space and select **Refresh**.
     3. Add a description:
        - Right-click the computer > **Properties**.
        - Enter a description (e.g., `Shared Desktop`).
     4. Test the **Restrict Control Panel** policy:
        - Log into a User account on your Enterprise VM.
        - Attempt to access the Control Panel.
           - Search for Control Panel in the Windows search. 
        - Expected result: A pop-up stating, *"This operation has been cancelled due to restrictions in effect..."*.

<p align="center">
   <img src="https://github.com/JBrunoX/Help-Desk-Lab/blob/main/images/deniedControlPanel.png">
</p>

   6. If the policy doesn’t apply yet:
        - GPOs refresh every 90 minutes by default (with a random 30-minute offset).
        - To force an immediate update:
          - Open Command Prompt on the Enterprise VM.
          - Type `gpupdate /force` and wait for it to complete successfully.
        - Retest access to the Control Panel.
     7. Test the remaining policies:
        - Verify **Desktop Wallpaper**, **Disable USB**, **Password**, and **Drive Mapping** as needed.
