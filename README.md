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
1. Draw a diagram of the environment using a tool such as draw.io

A lab diagram helps organize and plan the setup, showing how different systems, tools, and network elements are connected. This aids in troubleshooting, understanding workflows, and ensuring everything is properly configured for experiments or security testing.

![AD Lab Diagram](https://github.com/user-attachments/assets/d0d1021c-fe93-40a5-9367-1aef43656720)

2. Install Oracle VM VirtualBox Manager
Download the appropiate version from https://www.virtualbox.org/virtualbox.org

3. Install Windows 10

4. Install Kali Linux

5. Install Windows Server

6. Install Ubuntu Server

Refer to the screenshot below, which shows what we've just done. You should now have Oracle VM VirtualBox Manager installed, along with four VMs running Windows 10, Kali Linux, Windows Server, and Splunk Server."

![lab set up](https://github.com/user-attachments/assets/07ac8df9-b70f-4338-8727-55a09dd50412)


**Phase 2: Configure the Network**

**Phase 3: Active Directory and Control Domain**

**Phase 4: Brute Force Attack**

**Phase 5: Splunk Telemetry**

## References & Resources:
- Microsoft Active Directory Documentation
- Splunk Documentation
- Atomic Red Team GitHub
- Sysmon Documentation
- Splunk Universal Forwarder Documentation
