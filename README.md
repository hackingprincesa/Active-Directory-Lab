## Overview
This project involves setting up a home lab environment using VirtualBox to simulate a small Active Directory infrastructure with two Windows 10 machines, a Kali Linux machine for penetration testing, and a Splunk machine for telemetry and log analysis. The environment was configured to simulate security attacks on an Active Directory domain, collect telemetry data, and analyze potential vulnerabilities.

## Objective

The lab aims to provide a hands-on experience in setting up a virtualized environment for cybersecurity testing and exploration. Participants will create and configure multiple virtual machines (VMs) running Windows 10, Kali Linux, Windows Server, and Ubuntu Server. The lab focuses on teaching essential skills such as network configuration, security tool installation (e.g., Splunk, Sysmon), endpoint monitoring, and conducting security tests (including brute force attacks with Crowbar). Additional objectives include joining Windows machines to an Active Directory domain, enabling Remote Desktop, and automating tasks using PowerShell scripting. Overall, the lab offers practical exposure to cybersecurity concepts, tools, and techniques in a controlled, safe environment.

## Tools:
- Oracle VM VirtualBox Manager: For creating and managing virtual machines (VMs).
- Active Directory: For centralized domain management and user authentication.
- PowerShell: For scripting and automation of tasks.
- Splunk Server: For log analysis and monitoring, and SIEM to collect and analyze system logs.
- Crowbar: For brute force attacks.
- Atomic Red Team: For simulating adversary tactics via PowerShell.
- Sysmon: For monitoring and logging system activity on Windows.
- Splunk Universal Forwarder: For collecting and forwarding log data to Splunk.

## Step-by-Step Guide:

**Phase 1: Environment Install and Configuration**

***1. Draw a diagram of the environment using a tool such as <a href="https://app.diagrams.net/">draw.io</a>***

A lab diagram helps organize and plan the setup, showing how different systems, tools, and network elements are connected. This aids in troubleshooting, understanding workflows, and ensuring everything is properly configured for experiments or security testing.

![AD Lab Diagram](https://github.com/user-attachments/assets/d0d1021c-fe93-40a5-9367-1aef43656720)

***2. Install Oracle VM VirtualBox Manager***

- Download the compatible version from <a href="https://www.virtualbox.org/">VirtualBox</a>

***3. Install Windows 10***
- Navigate to <a href="https://www.microsoft.com/en-ca/software-download/windows10ISO">Microsoft</a> to install the compatible version.
   - Select the edition
   - Select the product language
   - Select 64-bit Download
   - Once the download pop up appears, select "Create installation media (USB flash drive, DVD, or ISO file) for another PC"
   - Select "ISO file" when pop up asks "Choose which media to use"
   - Save ISO file
- In VirtualBox, click "New" to create a new VM
   - Name: choose a name for VM (I named it Windows)

        Please note: this machine will be used as our target machine
   - Folder: select where you want VM to live
   - ISO Image: select ISO image that you just downloaded
   - Check "Skip Unattended Installation" to install OS manually

  ![Screen Shot 2025-02-04 at 5 15 38 PM](https://github.com/user-attachments/assets/d123ae11-c032-4ebc-baa8-40559718ec41)
  
  - Configure VM specifications (this can vary depending on your computer's specifications):
    - Select 4000 MB RAM for base memory, 1 CPU for processors, 50 GB for virtual hard disk
    - Finish
            
- Start VM and follow the installation prompts
   - Select "I don't have a product key"
   - Select "Windows 10 Pro"
   - Accept the license terms
   - Select "Custom: Install Windows only (advanced)"
   - Select "Next" to allow Windows to install 
      
***4. Install Kali Linux***
- Download <a href="https://www.kali.org/">Kali Linux</a>
   - Select the Pre-Built Virtual Machine
   - Choose either 64-bit (preferred) or 32-bit depending on your machine
     - To verify your machines specifications, select Windows key > type "System" > select "System Information" > view "System Type"
   - Click 64-bit, then choose VirtualBox 64
- Extract Kali Linux
   If you have any trouble extracting Kali Linux, download <a href="https://www.7-zip.org/">7 Zip</a> and extract with this tool.
- Once extracted, double click on the "vbox" file so that it's automatically imported into VirtualBox

![Screen Shot 2025-02-04 at 5 40 31 PM 1](https://github.com/user-attachments/assets/589bad71-9034-4702-955e-f566caea0a4f)

- Now, go to VirtualBox and run the Kali VM by clicking "Start"
- Log in with default credentials: kali/kali

***5. Install Windows Server***
- Download <a href="https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022">Windows Server 2022</a>
   - Fill out the form
   - Select "64-bit edition" under "ISO downloads"
- Once downloaded, go to VirtualBox and select "New" to create a new VM
   - Name: choose a name for VM (I named it ADDC since we will be using this as our Active Directory Domain Controller)
   - Folder: select where you want VM to live
   - ISO Image: select ISO image that you just downloaded
   - Check "Skip Unattended Installation" to install OS manually
- Configure VM specifications (this can vary depending on your computer's specifications):   
   - Select 4000 MB RAM for base memory, 1 CPU for processors, 50 GB for virtual hard disk
   - Finish
- Start VM and follow the installation prompts
   - Select "Install Now"
   - Select "Windows Server 2022 Standard Evaluation (Desktop Experience)"
   - Accept the license terms
   - Select "Custom: Install Windows Microsoft Server Operating System only (advanced)"
   - Select "Next" to allow Windows to install
   - Once setup is completed, you will be prompted to create a password
   - Select "Finish"
- Log in with recently created password
      - Select "No" when asked "Do you want to allow your PC to be discoverable by oth PCs and devices on this network?"


***6. Install Ubuntu Server***
- Download <a href="https://ubuntu.com/server">Ubuntu Server</a>
- Once downloaded, go to VirtualBox and select "New" to create a new VM
   - Name: choose a name for VM (I named it Splunk since we will be using this as our Splunk Server)
   - Folder: select where you want VM to live
   - ISO Image: select ISO image that you just downloaded
   - Check "Skip Unattended Installation" to install OS manually
- Configure VM specifications (this can vary depending on your computer's specifications):
       - Select 8000 MB RAM for base memory, 2 CPU for processors, 100 GB for virtual hard disk
          - Splunk will require more specs as it will be ingesting data and we'll be running searches on it  
- Finish
- Start the VM
   - Select "Try or Install Ubuntu Server"
   - Follow installation prompts; leave as default
   - Fill out "Profile Setup" form, which is where you will choose your credentials
    - Once installed, select "Reboot Now"
    - Click "Enter" when "Failed unmounting" error pops up
- Once rebooted, logon with recently created credentials
    - run command: sudo apt-get update && sudo apt-get upgrade -y
         - this command will update & upgrade all of our repositories
    - Once completed, hit "Enter" 

Refer to the screenshot below, you should now have Oracle VM VirtualBox Manager installed, along with four VMs running Windows 10, Kali Linux, Windows Server, and Splunk Server.

![lab set up](https://github.com/user-attachments/assets/07ac8df9-b70f-4338-8727-55a09dd50412)


**Phase 2: Configure the Network**

***1. Setup Communications***
- In Virtual Box, navigate to Tools > Network > NAT Networks > Create
   - Refer to screenshot below for configuration details.

![NAT](https://github.com/user-attachments/assets/6a33e514-410c-4b33-b234-18148c97bb0b)

   - Click "Apply"
   - Navigate to each VM > Settings > Network
   - Refer to screenshot below for configuration details.

![NAT config](https://github.com/user-attachments/assets/90bdf6cc-0d5e-4c84-90c3-9c53c53230e9)

- Repeat the above 2 steps for each VM
   - Navigate to each VM > Settings > Network
   - Refer to screenshot above for configuration details.    
- Next, start Splunk VM
   - run: ip a
      - this will display current IP address, which will need to be updated to static IP 192.168.10.10/24
- To set a static IP on Splunk server:
   - Run: sudo nano /etc/netplan/00-installer-config.yaml
      - tab to auto-complete, should only have one file 
   - Configure:
  ```
  network: 
     ethernet:
       enp0s3:
         dhcp4: no
         addresses: [192.168.10.10/24]
         nameservers:
               addresses: [8.8.8.8]
         routes:
          - to: default
            via: 192.168.10.1
   version: 2
    ```
   - Save configuration
   - Run: sudo netplan apply
   - Run: ip a
      - This will verify if IP address persists and is set to 192.168.10.10/24   
   - Reboot
   - Verify connection by running: ping google.com
     
The steps above did not work for me as I had a different configuration file, but this turned out to be a great opportunity to troubleshoot and learn more. The configuration file on my Splunk server was 50-cloud-init.yaml, meaning our IP updates wouldn’t persist after a reboot. To resolve this, I created a custom 00-installer-config.yaml file inside /etc/netplan/ and configured it with the updated IP. This ensured the static IP would remain after a reboot instead of reverting to DHCP. I also had to back up and delete the old 50-cloud-init.yaml file. Reboot and verify IP address once done.

***2. Install Splunk***
   
- Navigate to <a href="https://www.splunk.com/">Splunk</a> download free trial of Splunk Enterprise
   - Select Linux as OS
   - Select ".deb" file
   - Save into preferred directory
- Navigate back to Splunk VM
   - Run: sudo apt-get install virtualbox
      - this will display what options are available
   - Run: sudo apt-get install virtualbox-guest-additions-iso
   - Type "y"
   - Click "Enter"
   - Once installed, run: clear
- Navigate to Devices (on the top left of the screen) > Shared Folders > Shared Folders Settings
   - Add a folder
      - Folder Path: select path where we saved our Splunk installer
      - Foler Name: leave as default (AD-Project in our case)
      - Select: Read-only, Auto-mount, and Make Permenant
      - Click "Ok" 
- In Splunk, run: sudo reboot
   - Once rebooted, log back in
   - Run: sudo adduser <your username> vboxsf
      - ex. sudo adduser username vboxsf
   - If you receive a "group vboxsf does not exist" error, we may need some additional guest installations
      - Run: sudo apt-get install virtualbox
         - This will display what options are available
      - Run: sudo apt-get install virtualbox-guest-utils
      - Run: sudo reboot
      - Run: sudo adduser username vboxsf
         - User should be added to group now
- Create a new directory called "Share"
   - Run: mkdir Share
   - Run: ls
      - Newly created directory "Share" should be listed 
- Next, mount our shared folder onto our directory called "Share"
   - Run: sudo mount -t vboxsf -o uid=1000,gid=1000 <directory name where .deb file is located> share/
      - ex. sudo mount -t vboxsf -o uid=1000,gid=1000 AD-Project share/
      - If you forget what your shared folder name is:
         - Navigate to Devices > Shared Folders > Shared Folders Settings
   - If you get an error, exit session and re-do steps
      - Run: exit
      - Error may occur because when you add your user into a new group, it may not reflect until you log out
   - Run: ls -la
      - Should now see that our "share" is now highlighted
- Change directories into that share
   - Run: cd share
   - Run: clear
   - Run: ls -la
      - This will display all the files listed in this directory, including our Splunk Installer
- To install Splunk:
   - Run: sudo dpkg -i splunk (hit tab to auto-complete)
   - Once you see "Complete", should be good to change into directory where Splunk is located onto our server
- Change directory
   - Run: cd /opt/splunk
   - Run: ls -la
      - Here you will notice that all users and groups belong to Splunk, which is a good thing as it limits the permissions to that user
- Change into user Splunk
   - Run: sudo -u splunk bash
      - Now, we are acting as user Splunk 
- Run: cd bin
   - Files listed in here are all binaries that Splunk can use
   - the one that we will use is "./splunk start"
   - Run: ./splunk start
      - This will run the installer
   - Click "q"
   - Type "y" to accept
   - Select an administrator username and password
- Once installation is completed:
   - Run: exit
      - To exit out of user Splunk 
   - Run: cd bin
   - Run: sudo ./splunk enable boot-start -user splunk
      - Whenever the VM reboots, Splunk will run with user splunk
  
***3. Configure Windows Machine***
   
- Rename the host name of machine
   - In the Start Menu search, search "PC"
   - Select "Properties"
   - Select "Rename this PC"
   - Rename to "target-PC"
   - Select "Next"
   - Select "Restart Now"
     
- Update static IP to 192.168.10.100
   - Open command prompt
   - Run: ipconfig
      - this will display current IPv4
   - Navigate to network icon at the bottom right of the window
   - Select "Open Network & Internet Settings"
   - Select "Change adapter options"
   - Right click the adapter, Ethernet
   - Select "Properties"
   - Select "Internet Protocol Version 4 (TCP/IPv4)" > "Properties"
   - Select "Use the following IP address"
   - Configure as shown below:
     
![windows static IP](https://github.com/user-attachments/assets/f1388824-1798-4019-8672-794cb4933393)

   - Run IP config to view updated IPv4

![cmnd prompt](https://github.com/user-attachments/assets/38e0c671-84ff-4246-b9e3-f668b4fc1809)

- Install Splunk Universal Forwarder on target-PC
   - Run Splunk VM (this will not work if VM is not running)
   - In the target-PC, open the browser and type 192.168.10.10:8000 blah blah fix blah blah
   - In the target-PC, visit <a href="https://www.splunk.com/">Splunk</a> and 

Install Sysmon
- In the target-PC, navigate to <a href="https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon">Sysmon Downloads</a>
- Navigate to <a href="https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml">Sysmon's Configuration File</a> on GitHub
- Click "raw"
- Save the file
- Extract the Sysmon file
- Open PowerShell as administrator
- Copy and Paste the URL of the extracted directory here
- Run .\Sysmon64.exe -i ..\sysmonconfig.xml
- Click "Agree"

Configure Splunk Unviersal Forwarder to specify what data we want to send to our Splunk Server
- Navigate to File Explorer > Local Disk (C:) > Program Files > SplunkUniversalForwarder > etc > system > local
- Open Notepad as administrator and enter the following:
- insert ss***
- Save file as 
   
***5. Configure Windows Server***

**Phase 3: Active Directory and Control Domain**

1. Setup Active Directory Domain Services on Windows Server
   
2. Windows 10 Machine Joins New Domain

**Phase 4: Brute Force Attack**

***1. Configure Network***
   
***2. Set up the Attack***
   
***3. Enable RDP***
   
***4. Attack***
   
***5. ART***

**Phase 5: Splunk Telemetry**

1. Analyze Attack with Splunk

## References & Resources:
- <a href="https://www.youtube.com/watch?v=mWqYyl89QaY&t=541s">Active Directory Project by MyDFIR</a>
- Microsoft Active Directory Documentation
- Splunk Documentation
- <a href="https://github.com/redcanaryco/atomic-red-team">Atomic Red Team GitHub</a>
- Sysmon Documentation
- Splunk Universal Forwarder Documentation
