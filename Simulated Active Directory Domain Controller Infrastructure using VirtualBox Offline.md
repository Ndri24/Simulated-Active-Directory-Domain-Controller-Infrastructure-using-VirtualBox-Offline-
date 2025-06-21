# Simulated Active Directory Domain Controller Infrastructure using VirtualBox Offline

## 1. Windows Server Evaluation and Windows 10 Enterprise Evaluation Installation
  In the **Virtual Machine (VM)**, **select** the **'Create Virtual Machine'** icon (often a `+` or 'New' button depending on the VirtualBox version) to start the installation process. On the installation page. 
  **Enter** `DC-SERVER` as the **'Name'** for the VM.
  **Choose** the desired folder for the installation location (e.g., `F:\Virtual Box`).
  In the **'ISO Image'** section, **select** your Windows Server ISO file
  **Click** **'Next'** to proceed.

![VM Name and Operating System Configuration Page](images/gambar1.png)

In this step, **enter** you desired 'Username and Password', then confirm the **'Guest Additions'** checkbox is checked. **Click next** to proceed

![Unattended Guest OS Install Setup Page](images/gambar2.png)

For this step, configure the **'VM Base memory'** to `3048 MB` and allocate `1` **CPU** click next to proceed

![VM Hardware Configuration Page](images/gambar3.png)

On this page, set the **Disk Size** for your virtual hard disk, **Click 'Next'** to proceed

![Virtual Hard Disk Configuration Page](images/gambar4.png)

Wait for the installation to finish

![Windows Server Operating System Installation Progress](images/gambar5.png)

After the installation is complete, you will be able to access the Windows Server desktop.

![Windows Server Desktop After Installation](images/gambar6.png)

For Windows 10 installation, **follow the same steps**, with the following setting: 
**VM Name** `Client-01`
**Base Memory**  `2048 MB`, 
**Processor count** `1`
**Virtual Storage** `30GB`

![Unattended Guest OS Install Setup for Windows 10](images/gambar7.png)
![Hardware Configuration for Windows 10](images/gambar8.png)
![Virtual Hard Disk Configuration for Windows 10](images/gambar9.png)
![Windows 10 Installation Progress](images/gambar10.png)

## 2. Configure VirtualBox Network
On the Virtualbox Manager select `File` > `Tools` > `Network Manager`.
On the **'VirtualBox Host-Only Network Details'** page select `VirtualBox Host-Only Ethernet Adapter` then click the **Properties** 

![VirtualBox Host-Only Network Details Window](images/gambar11.png)

Click **DHCP Server** tab then uncheck the **Enable Server** checkbox to disable DHCP

![DHCP Server Tab](images/gambar12.png)

Next go to the adapter tab set the **IPv4 Address** to `192.168.56.1` and **IPv Network Mask** to `255.255.255.0`

![Adapter Tab Manual IP Configuration](images/gambar13.png)

Return to the main Virtual Box Manager page. For both the **Windows Server and Windows 10** go to their respective VM setting then navigate to the network section, In the network settings configure **Adapter 1** to be **NAT**

![Network Settings Adapter 1 NAT](images/gambar14.png)

For Adapter 2 check the Enable Network Adapter checkbox, and set “Attached to” to **Host only Adapter**

![Network Settings Adapter 2 Host-Only](images/gambar15.png)

## 3. Configure IP for Windows Server
To configure IP for Windows Server navigate to `Control Panel` > `Network and Internet` > `Network and Sharing Center` > `Change adapter settings`. Then select `Adapter 2` right-click and choose **Properties** and Select **Internet Protocol Verision 4**

![Network Connections Window](images/gambar16.png)

After choosing **Internet Protocol Version 4 (TCP/IPv4)**, go to its properties. Check **Use the following IP address** and set the **IP address** to `192.168.56.10`, **Subnet mask** to 255.255.255.0, and **Default gateway** to `192.168.56.1`. Next, check **Use the following DNS server addresses** and configure the **Preferred DNS server** as `127.0.0.1`.

![Internet Protocol Version 4 (TCP/IPv4) Properties](images/gambar17.png)

After configuring the IP for Windows Server, verify the configuration by opening **Command Prompt** and type **ping 192.168.56.1**. if successful, the Windows Server will receive replies from `192.168.56.1`

![Command Prompt Ping Verification](images/gambar18.png)

## 4. Install and Configure Active Directory Domain Services (AD DS) and DNS
To begin, open **Server Manager** from the Start menu. In *Server Manager*,select **Add Roles and Features**

![Server Manager Dashboard](images/gambar19.png)

After choosing **Add Roles and Features** the installation wizard will launch. On the **Installation Type** screen, select Role-based or feature-based installation** and click Next to proceed

![Add Roles and Features Wizard - Installation Type](images/gambar20.png)

On the **Server Selection** page, check **Select a server from the server pool**.then, select the local server and click Next to continue.

![Add Roles and Features Wizard - Server Selection](images/gambar21.png)

On the **Server roles** page, choose `Active Directory Domain Services` and `DNS Server`. Continue by clicking Next through the subsequent prompt until the installation progress begin.

![Add Roles and Features Wizard - Server Roles](images/gambar22.png)

Wait until the installation process is complete

![Add Roles and Features Wizard - Installation Progress](images/gambar23.png)

Once the installation is complete, click the **flag icon** and select **Promote this server to a domain controller**

![Post-deployment Configuration Notification](images/gambar24.png)

On the **'Deployment Configuration'** step in the AD DS Configuration Wizard, **select** **'Add a new forest'**.
**Provide a name** for your **'Root domain name'** Click next to continue.
 
![AD DS Configuration Wizard - Deployment Configuration](images/gambar25.png)

On the **Domain Controller** page, provide a password **for Directory Services Restor Mode (DSRM)** Click Next through the remaining steps until the installation is complete. Finally **Restart** the Windows Server to apply the settings.
 
![AD DS Configuration Wizard - Domain Controller Options](images/gambar26.png)

## 5. Join Domain (Client)
On the Windows 10 client, set the following IP configuration:  
***IPv4 Address:** `192.168.56.11`
    * **Subnet mask:** `255.255.255.0`
    * **Default gateway:** `192.168.56.1`
    * **Preferred DNS server:**`192.168.56.10` 
    then click Apply once configured

![Network IP Configuration on Windows 10 Client](images/gambar27.png)

After configuring the IP address for windows 10, go to the search bar and type **System**, then open the **System** settings

![Searching for 'System' in Windows 10 Search Bar](images/gambar28.png)

On the **System** settings page, select **Advanced system** settings’.

![System Settings with 'Advanced system settings' Highlighted](images/gambar29.png)

In the **System Properties** windows, navigate to the **Computer Name** tab and click **Change** button.

![Computer Name Tab in System Properties](images/gambar30.png)

In the ‘Computer **Name/Domain Changes** select the **Domain radio button** and Enter the Windows Server domain name,Then click **OK** to proceed

![Computer Name/Domain Changes Window](images/gambar31.png)

Enter the domain administrators username and password to join the domain.

![Windows Security Prompt for Domain Join](images/gambar32.png)

If successful, a notification will confirm that the client has joined the domain, and prompted to restart Windows 10

![Welcome to the Domain Notification](images/gambar33.png)

## 6. Create OU (Organizational Unit) and User in Active Directory

Search **Active Directory Users and Computers** in Windows server and open the application/

![Searching for Active Directory Users and Computers](images/gambar34.png)

Once **Active Directory Users and Computers** is open, navigate to domain name

![Active Directory Users and Computers - Domain Selected](images/gambar35.png)

Rigt-click on domain then select `New` > `Organizational Unit`. **Provide a name** for the OU, for example `OU-ITSupport`.. Click **OK** to create the OU

![New Object - Organizational Unit Dialog](images/gambar36.png)

Right-click on the newly created **OU-ITSupport**. Select `New` > `User`.

![New Object - User Dialog](images/gambar37.png)

Fill the in the column for the **First name**, **Lastname**, **Fullrname** and **User logon name**. Click Next to proceed. **Set** the user password and select desired password options.

![New User Password Configuration Dialog](images/gambar38.png)

 **Click Finish** to create the new user account 

![Create New User](images/gambar39.png)

## 7. Create Shared Folder on Server

On the Windows Server, **create** a new folder on the `C:\` drive and name the `ShareDocs`

![File Explorer with ShareDocs Folder](images/gambar40.png)

Right click on the `ShareDocs` navigate to `Properties` > `Sharing` > `Advanced Sharing`., check **Share this Folder**
 
![ShareDocs Properties Window - Advanced Sharing](images/gambar41.png)

Click the **Permissions** and add the domain user who should have access.**Grant** then appropriate permissions. Ensure the **Windows 10 (Client)** has the necessary permissions to access this folder

![Permissions for ShareDocs Dialog](images/gambar42.png)

### Access from Client
Login in to the **Windows 10 (Client)** using a domain user account.

![Windows 10 Login Screen with Domain Account](images/gambar43.png)

Open File Explorer.Navigate to `\\DC-Server\ShareDocs` to verify access to the shared folder.

![File Explorer Displaying Shared Folder from DC-Server](images/gambar44.png)

## 8. Configure Group Policy Objects (GPO)
On the Windowss Server, search for **Group Policy Management** and open it.

![Searching for Group Policy Management in Windows Server](images/gambar45.png)

In Group Policy Management, navigate to `Forest` > `Domains` > `andrilab.local` > `OU-ITSupport` Right-click on `OU-ITSupport` and select **Create a GPO in this domain, and Link it here**. Name the new GPO ‘ITSupportPolicy’ and click **OK**

![Context Menu for Creating a New GPO](images/gambar46.png)

Right click on ‘ITSpportPolicy’ and select **Edit**. This will open the Group Policy Management Editor.

![Context Menu for Editing a GPO](images/gambar47.png)

### Example Policy Configurations
Disable USB access:
In **Group Policy Management Editor** navigate to `Computer Configuration` > `Policies` > `Administrative Templates` > `System` > `Removable Storage Access`.
Locate and open the policy **All Removeable storage classes: Deny all access**

![Group Policy Management Editor - Removable Storage Access](images/gambar48.png)

Select **Enabled** to disable USB access.

![Properties of 'All Removable Storage classes: Deny all access' Policy](images/gambar49.png)

Disable Control Panel Access 
Navigate to `User Configuration` > `Administrative Templates` > `Control Panel`. Locate and open the policy **Prohibit access to Control Panel and PC settings**. 

![Properties of 'Prohibit access to Control Panel and PC settings' Policy](images/gambar50.png)

Select Enable
If this policy enabled, clients will be unable to open Control Panel and Settings. 
![Enabled 'Prohibit access to Control Panel and PC settings' Policy](images/gambar51.png)

Set Dekstop Wallpaper
Navigate to `User Configuration` > `Administrative Templates` > `Desktop` > `Desktop`. open the policy **Dekstop Wallpaper**.

![Group Policy Management Editor - Desktop Wallpaper Policy](images/gambar52.png)

Select enabled in the **Wallpaper name** field,  enter the network path to your wallpaper file and then click **OK**.

![Properties of 'Desktop Wallpaper' Policy](images/gambar53.png)

Activating GPO on the Client
On the windows 10 (Client) search and open **Commad Prompt** as administrator.

![Searching for Command Prompt in Windows 10](images/gambar54.png)

Type `gpupdate /force` and press **Enter** to apply the new Group Policy

![Command Prompt with gpupdate /force Command](images/gambar55.png)

If the commands is successful, a notification will appear confirming the policy update and then **restart** Windows 10 (Client)

![gpupdate Success Notification](images/gambar56.png)

Let see the policy has been updated if the wallpaper not show copy file wallpaper to Client (ensure it's accessible via the network path)
Try open **Control Panel** it should  show restrictions for accessing it (Optional: Test USB access if applicable

![Verify the GPO](images/gambar57.png)

## 9. Basic Monitoring and Event Viewer
**Attempt to log in** to Windows 10 (Client)

![Windows 10 Login Screen](images/gambar58.png)

On Windows Server,open **Event Viewer** to monitor login attempts.  
    * A successful login attempt is logged with **Event ID `4624`**.
    * A logoff event is logged with **Event ID `4634`**.
    * A failed login attempt is logged with **Event ID `4625`** 
    Monitoring these events can help identify **Unauthorized access** or **Data breach** attempts.

![Event Viewer - Security Logs](images/gambar59.png)

