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
1. Draw a diagram of the environment using a tool such as <a href="https://app.diagrams.net/">draw.io</a>

A lab diagram helps organize and plan the setup, showing how different systems, tools, and network elements are connected. This aids in troubleshooting, understanding workflows, and ensuring everything is properly configured for experiments or security testing.

![AD Lab Diagram](https://github.com/user-attachments/assets/d0d1021c-fe93-40a5-9367-1aef43656720)

2. Install Oracle VM VirtualBox Manager
Download the appropiate version from <a href="https://www.virtualbox.org/">VirtualBox</a>

3. Install Windows 10
   - Navigate to <a href="https://www.microsoft.com/en-ca/software-download/windows10ISO">Microsoft</a> to install the compatible version.
   - In VirtualBox, click "Add" to create a new VM and follow the installation prompts.
      
5. Install Kali Linux
   - Download <a href="https://www.kali.org/><Kali Linux</a> 
   - Extract Kali Linux
        If you have any trouble extracting Kali Linux, download <a href="https://www.7-zip.org/">7 Zip</a> and extract with this tool.
   - Import Kali Linux into VirtualBox
   - Run the VM

7. Install Windows Server
   - Download <a href="https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022">Windows Server 2022</a>
   - Download 64-bit version
   - 

9. Install Ubuntu Server

Refer to the screenshot below, you should now have Oracle VM VirtualBox Manager installed, along with four VMs running Windows 10, Kali Linux, Windows Server, and Splunk Server."

![lab set up](https://github.com/user-attachments/assets/07ac8df9-b70f-4338-8727-55a09dd50412)


**Phase 2: Configure the Network**
1. Setup Communications
   - In Virtual Box, navigate to Tools > Network > NAT Networks > Create
   - Refer to screenshot below for configuration details.

![NAT](https://github.com/user-attachments/assets/6a33e514-410c-4b33-b234-18148c97bb0b)

   - Click "Apply"
   - Navigate to each VM > Settings > Network
   - Refer to screenshot below for configuration details.

![NAT config](https://github.com/user-attachments/assets/90bdf6cc-0d5e-4c84-90c3-9c53c53230e9)

   - Repeat the above 2 steps for each VM, except for Splunk.
   - Next, run Splunk VM and type sudo nano /etc/netplan/00-installer-config.yaml

2. Install Splunk
   - Navigate to <a href="https://www.splunk.com/">Splunk</a> download free trial of Splunk Enterprise
   - Navigate back to Splunk and run sudo apt-get install virtualbox-guest-additions-iso

  
3. Configure Windows Machine
   
4. Configure Windows Server 

**Phase 3: Active Directory and Control Domain**

1. Setup Active Directory Domain Services on Windows Server
   
2. Windows 10 Machine Joins New Domain

**Phase 4: Brute Force Attack**

1. Configure Network
   
2. Set up the Attack
   
3. Enable RDP
   
4. Attack
   
5. ART

**Phase 5: Splunk Telemetry**

1. Analyze Attack with Splunk

## References & Resources:
- Microsoft Active Directory Documentation
- Splunk Documentation
- <a href="https://github.com/redcanaryco/atomic-red-team">Atomic Red Team GitHub</a>
- Sysmon Documentation
- Splunk Universal Forwarder Documentation
