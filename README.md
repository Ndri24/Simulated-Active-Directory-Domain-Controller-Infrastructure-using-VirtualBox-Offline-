# Simulated-Active-Directory-Domain-Controller-Infrastructure-using-VirtualBox-Offline-
This project is a local Active Directory lab simulated in VirtualBox using Windows Server and Windows 10 virtual machines. It demonstrates AD DS setup, DNS, OU and user management, shared folder configuration, GPO enforcement, RSAT usage, and basic system monitoring all in an offline environment suitable for IT Support and Cybersecurity practice.

## Overview

This project is a local Active Directory lab simulated in VirtualBox using Windows Server and Windows 10 virtual machines. It demonstrates AD DS setup, DNS, OU and user management, shared folder configuration, GPO enforcement, RSAT usage, and basic system monitoring all in an offline environment suitable for IT Support and Cybersecurity practice.

**Technologies Used:**
* Windows Server 2019 Standard Evaluation
* Windows 10 Enterprise Evaluation
* Oracle VirtualBox 7.0
* Active Directory Domain Services (AD DS)
* Domain Name System (DNS)
* Group Policy Management (GPM)

**Lab Architecture:**
The lab consists of two virtual machines:
* **DC-SERVER:** A Windows Server 2019 VM acting as the Domain Controller and DNS server.
* **CLIENT-01:** A Windows 10 VM joined to the `andrilab.local` domain.
Both VMs are connected via a VirtualBox Host-Only network for internal communication and a NAT network for internet access on the server.

## Skills Demonstrated

Through this project, I have demonstrated proficiency in:
* Virtual Machine installation and configuration (VirtualBox).
* Active Directory Domain Services (AD DS) deployment and promotion.
* DNS server configuration and integration with AD.
* Domain joining for client machines.
* Organizational Unit (OU) and User account creation in Active Directory.
* Network shared folder creation and permission management.
* Group Policy Object (GPO) creation, linking, and enforcement for security settings (USB access, Control Panel restrictions) and user experience (desktop wallpaper).
* Basic system monitoring using Event Viewer for user login/logout activities.

## Challenges and Solutions

During the setup process, I encountered a few challenges:
* **Challenge 1: DNS Resolution Issues during Domain Join.**
    * **Solution:** Ensured the Windows 10 client's preferred DNS server was correctly set to the IP address of the Domain Controller (`192.168.56.10`). Initially, I had set it to the gateway, which prevented proper domain resolution.
* **Challenge 2: GPO Not Applying Immediately.**
    * **Solution:** Learned the importance of running `gpupdate /force` on the client machine and restarting it to ensure immediate application of new Group Policy settings. Also verified network access to the GPO files.

## Future Enhancements

Potential future developments for this lab include:
* Implementing a DHCP server role on the Windows Server.
* Deploying software via Group Policy.
* Configuring user roaming profiles.
* Integrating a basic file server with Distributed File System (DFS).
* Automating user creation using PowerShell scripts.
