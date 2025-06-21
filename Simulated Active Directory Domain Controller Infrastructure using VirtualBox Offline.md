# Windows Server and Windows 10 Lab Setup Documentation

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

![VirtualBox Host-Only Network Details Window](images/gambar12.png)

Click **DHCP Server** tab then uncheck the **Enable Server** checkbox to disable DHCP


