# Simulated Active Directory Domain Controller Infrastructure using VirtualBox Offline

## 1. Windows Server Evaluation and Windows 10 Enterprise Evaluation Installation
  In the **Virtual Machine (VM)**, **select** the **Create Virtual Machine** icon (often a `+` or 'New' button depending on the VirtualBox version) to start the installation process. On the installation page. 
  **Enter** `DC-SERVER` as the **Name** for the VM.
  **Choose** the desired folder for the installation location (e.g., `F:\Virtual Box`).
  In the **ISO Image** section, **select** your Windows Server ISO file
  **Click** **'Next'** to proceed.

<img src="images/gambar1.png" width="500">

In this step, **enter** you desired **Username and Password**, then confirm the **Guest Additions** checkbox is checked. **Click next** to proceed

<img src="images/gambar2.png" width="500">

For this step, configure the **VM Base memory** to `3048 MB` and allocate `1` **CPU** click next to proceed

<img src="images/gambar3.png" width="500">

On this page, set the **Disk Size** for your virtual hard disk, **Click Next** to proceed

<img src="images/gambar4.png" width="500">

Wait for the installation to finish

<img src="images/gambar5.png" width="500">

After the installation is complete, you will be able to access the Windows Server desktop.

<img src="images/gambar6.png" width="500">
For Windows 10 installation, follow the same steps, with the following setting: 
VM Name`Client-01`
Base Memory  `2048 MB`
Processor count `1`
Virtual Storage `30GB`

<img src="images/gambar7.png" width="500">
<img src="images/gambar8.png" width="500">
<img src="images/gambar9.png" width="500">
<img src="images/gambar10.png" width="500">

## 2. Configure VirtualBox Network
On the Virtualbox Manager select `File` > `Tools` > `Network Manager`.
On the **VirtualBox Host-Only Network Details** page select `VirtualBox Host-Only Ethernet Adapter` then click the **Properties** 

<img src="images/gambar11.png" width="500">

Click **DHCP Server** tab then uncheck the **Enable Server** checkbox to disable DHCP

<img src="images/gambar12.png" width="500">

Next go to the adapter tab set the **IPv4 Address** to `192.168.56.1` and **IPv Network Mask** to `255.255.255.0`

<img src="images/gambar13.png" width="500">

Return to the main Virtual Box Manager page. For both the **Windows Server and Windows 10** go to their respective VM setting then navigate to the network section, In the network settings configure **Adapter 1** to be **NAT**

<img src="images/gambar14.png" width="500">

For Adapter 2 check the Enable Network Adapter checkbox, and set “Attached to” to **Host only Adapter**

<img src="images/gambar15.png" width="500">

## 3. Configure IP for Windows Server
To configure IP for Windows Server navigate to `Control Panel` > `Network and Internet` > `Network and Sharing Center` > `Change adapter settings`. Then select `Adapter 2` right-click and choose **Properties** and Select **Internet Protocol Verision 4**

<img src="images/gambar16.png" width="500">

After choosing **Internet Protocol Version 4 (TCP/IPv4)**, go to its properties. Check **Use the following IP address** and set the **IP address** to `192.168.56.10`, **Subnet mask** to 255.255.255.0, and **Default gateway** to `192.168.56.1`. Next, check **Use the following DNS server addresses** and configure the **Preferred DNS server** as `127.0.0.1`.

<img src="images/gambar17.png" width="500">

After configuring the IP for Windows Server, verify the configuration by opening **Command Prompt** and type **ping 192.168.56.1**. if successful, the Windows Server will receive replies from `192.168.56.1`

<img src="images/gambar18.png" width="500">

## 4. Install and Configure Active Directory Domain Services (AD DS) and DNS
To begin, open **Server Manager** from the Start menu. In *Server Manager*,select **Add Roles and Features**

<img src="images/gambar19.png" width="500">

After choosing **Add Roles and Features** the installation wizard will launch. On the **Installation Type** screen, select Role-based or feature-based installation** and click Next to proceed

<img src="images/gambar20.png" width="500">

On the **Server Selection** page, check **Select a server from the server pool**.then, select the local server and click Next to continue.

<img src="images/gambar21.png" width="500">

On the **Server roles** page, choose `Active Directory Domain Services` and `DNS Server`. Continue by clicking Next through the subsequent prompt until the installation progress begin.

<img src="images/gambar22.png" width="500">

Wait until the installation process is complete

<img src="images/gambar23.png" width="500">

Once the installation is complete, click the **flag icon** and select **Promote this server to a domain controller**

<img src="images/gambar24.png" width="500">

On the **Deployment Configuration** step in the AD DS Configuration Wizard, **select** **Add a new forest**.
**Provide a name** for your **Root domain name** Click next to continue.
 
<img src="images/gambar25.png" width="500">

On the **Domain Controller** page, provide a password **for Directory Services Restor Mode (DSRM)** Click Next through the remaining steps until the installation is complete. Finally **Restart** the Windows Server to apply the settings.
 
<img src="images/gambar26.png" width="500">

## 5. Join Domain (Client)
On the Windows 10 client, set the following IP configuration:  
***IPv4 Address:** `192.168.56.11`
    * **Subnet mask:** `255.255.255.0`
    * **Default gateway:** `192.168.56.1`
    * **Preferred DNS server:** `192.168.56.10` 
    then click Apply once configured

<img src="images/gambar27.png" width="500">

After configuring the IP address for windows 10, go to the search bar and type **System**, then open the **System** settings

<img src="images/gambar28.png" width="500">

On the **System** settings page, select **Advanced system** settings’.

<img src="images/gambar29.png" width="500">

In the **System Properties** windows, navigate to the **Computer Name** tab and click **Change** button.

<img src="images/gambar30.png" width="500">

In the ‘Computer **Name/Domain Changes** select the **Domain radio button** and Enter the Windows Server domain name,Then click **OK** to proceed

<img src="images/gambar31.png" width="500">

Enter the domain administrators username and password to join the domain.

<img src="images/gambar32.png" width="500">

If successful, a notification will confirm that the client has joined the domain, and prompted to restart Windows 10

<img src="images/gambar33.png" width="500">

## 6. Create OU (Organizational Unit) and User in Active Directory

Search **Active Directory Users and Computers** in Windows server and open the application/

<img src="images/gambar34.png" width="500">

Once **Active Directory Users and Computers** is open, navigate to domain name

<img src="images/gambar35.png" width="500">

Rigt-click on domain then select `New` > `Organizational Unit`. **Provide a name** for the OU, for example `OU-ITSupport`.. Click **OK** to create the OU

<img src="images/gambar36.png" width="500">

Right-click on the newly created **OU-ITSupport**. Select `New` > `User`.

<img src="images/gambar37.png" width="500">

Fill the in the column for the **First name**, **Lastname**, **Fullrname** and **User logon name**. Click Next to proceed. **Set** the user password and select desired password options.

<img src="images/gambar38.png" width="500">

 **Click Finish** to create the new user account 

<img src="images/gambar39.png" width="500">

## 7. Create Shared Folder on Server

On the Windows Server, **create** a new folder on the `C:\` drive and name the `ShareDocs`

<img src="images/gambar40.png" width="500">

Right click on the `ShareDocs` navigate to `Properties` > `Sharing` > `Advanced Sharing`., check **Share this Folder**
 
<img src="images/gambar41.png" width="500">

Click the **Permissions** and add the domain user who should have access.**Grant** then appropriate permissions. Ensure the **Windows 10 (Client)** has the necessary permissions to access this folder

<img src="images/gambar42.png" width="500">

### Access from Client
Login in to the **Windows 10 (Client)** using a domain user account.

<img src="images/gambar43.png" width="500">

Open File Explorer.Navigate to `\\DC-Server\ShareDocs` to verify access to the shared folder.

<img src="images/gambar44.png" width="500">

## 8. Configure Group Policy Objects (GPO)
On the Windowss Server, search for **Group Policy Management** and open it.

<img src="images/gambar45.png" width="500">

In Group Policy Management, navigate to `Forest` > `Domains` > `andrilab.local` > `OU-ITSupport` Right-click on `OU-ITSupport` and select **Create a GPO in this domain, and Link it here**. Name the new GPO ‘ITSupportPolicy’ and click **OK**

<img src="images/gambar46.png" width="500">

Right click on ‘ITSpportPolicy’ and select **Edit**. This will open the Group Policy Management Editor.

<img src="images/gambar47.png" width="500">

### Example Policy Configurations
Disable USB access:
In **Group Policy Management Editor** navigate to `Computer Configuration` > `Policies` > `Administrative Templates` > `System` > `Removable Storage Access`.
Locate and open the policy **All Removeable storage classes: Deny all access**

<img src="images/gambar48.png" width="500">

Select **Enabled** to disable USB access.

<img src="images/gambar49.png" width="500">

Disable Control Panel Access 
Navigate to `User Configuration` > `Administrative Templates` > `Control Panel`. Locate and open the policy **Prohibit access to Control Panel and PC settings**. 

<img src="images/gambar50.png" width="500">

Select Enable
If this policy enabled, clients will be unable to open Control Panel and Settings. 

<img src="images/gambar51.png" width="500">

Set Dekstop Wallpaper
Navigate to `User Configuration` > `Administrative Templates` > `Desktop` > `Desktop`. open the policy **Dekstop Wallpaper**.

<img src="images/gambar52.png" width="500">

Select enabled in the **Wallpaper name** field,  enter the network path to your wallpaper file and then click **OK**.

<img src="images/gambar53.png" width="500">

Activating GPO on the Client
On the windows 10 (Client) search and open **Commad Prompt** as administrator.

<img src="images/gambar54.png" width="500">

Type `gpupdate /force` and press **Enter** to apply the new Group Policy

<img src="images/gambar55.png" width="500">

If the commands is successful, a notification will appear confirming the policy update and then **restart** Windows 10 (Client)

<img src="images/gambar56.png" width="500">

Let see the policy has been updated if the wallpaper not show copy file wallpaper to Client (ensure it's accessible via the network path)
Try open **Control Panel** it should  show restrictions for accessing it (Optional: Test USB access if applicable

<img src="images/gambar57.png" width="500">

## 9. Basic Monitoring and Event Viewer
**Attempt to log in** to Windows 10 (Client)

<img src="images/gambar58.png" width="500">

On Windows Server,open **Event Viewer** to monitor login attempts.  
    * A successful login attempt is logged with **Event ID `4624`**.
    * A logoff event is logged with **Event ID `4634`**.
    * A failed login attempt is logged with **Event ID `4625`** 
    Monitoring these events can help identify **Unauthorized access** or **Data breach** attempts.

<img src="images/gambar59.png" width="500">

