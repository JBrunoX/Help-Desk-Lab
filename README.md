###### Installation Steps:
1. Install VMware Workstation Pro
	- Go to [vmware](https://knowledge.broadcom.com/external/article/344595/downloading-and-installing-vmware-workst.html) and scroll down to 'Download VMware Workstation Pro'. You will then be prompted to either login or create a Broadcom account (don't worry its free). 
	- If your current computer in use is Windows click the Windows version of VMware Workstation Pro 17.0. If your on Linux then choose the Linux version. If you don't see any of these click this [link](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware%20Workstation%20Pro&freeDownloads=true). After that click the latest release available. Agree to the Terms and Conditions and click the download icon at the right of the screen. Once the download is done, click it and simply follow the instillation wizard. Refer to this [article](https://knowledge.broadcom.com/external/article?articleNumber=387947) by Broadcom if you run into any issues. 
2. Download Windows Server 2025
	- Go to [Microsoft Evaluation Center](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2025) and choose the ISO download in your respective language.
3. Create a virtual machine for Windows Server 2025 using VMware Workstation Pro.
	- Open VMware and choose 'Personal use' to remain free.
	- Install operating system from: Here choose "I will install the operation system later" and click next.
	- Guest Operating System: Leave 1 enabled and choose Windows Server 2025 for Version then click next.
	- Virtual Machine Name: Click next.
	- Disk Size: Adjust Maximum disk size according to your machines disk space. I would recommended at least 60 GB for our setup. I have some room to spare so I bumped mine up to 80GB. Click next.
	- Ready to Create Virtual Machine: Click customize settings and adjust memory based on your machine. I have 48 GB of memory so I bumped mine to 6 GB which is 6144 MB. I recommended bumping yours from 2 GB to 4 GB which is 4096 MB. Now we go to Processors and change our Number of processors from 1 to 2. Leave Number of cores per processor at 1. Now we will install our ISO file. Click CD/DVD (SATA) and choose Use ISO image. Click browse and select the ISO file we downloaded earlier. Click close then finish.
	- Now it's time to power up our newly created virtual machine! Select Startup this guest operating system and spam any key to load up Windows Server Setup. If you do not spam a key you will get a screen saying "Time Out" and "EFI Network". If this happens go to the left of your window and right click on your VM name. Choose Power then Shut Down Guest. Your VM will shut down and you may start it back up and get to spamming.
4. Install Windows Server 2025
	- Choose your language and time format then click next. Select your keyboard layout then click next.
	- Choose install Windows Server and check "I agree everything will be deleted..." then click next.
	- Choose Standard Evaluation (Desktop Experience) so we can have a GUI. Click next and accept the license terms.
	- Choose your disk, click next and then click install. Now we wait for it to finish installing.
	- Enter your password and your in!
5. Install Active Directory
	- Open Server Manager if not already open. You can do this by clicking the search bar on the bottom of your screen and then begin typing "Server Manager" then clicking it when you see it pop up.
	- On the top right click Manage < Add Roles and Features and click next. Keep role-based selected and click next, next again. 
	- Check Active Directory Domain Services and then add features. Now keep clicking next until it says install then click install. Once installed select Promote this server to a domain controller. Now select Add a new forest and name your domain (i.e HelpDeskSim.local). You must add .local at the end. Click next and wait for the wizard to load the next page. Enter a password for DSRM. This will be the password for our domain. Now keep clicking next until you reach install then click install. Note this will log you out. 

Congrats! You have just installed Windows Active Directory within a virtual machine. 
