#Overview

This repository documents my journey following MyDFIR's YouTube series on building and configuring an Active Directory (AD) lab. The series provides an excellent step-by-step guide for learning and implementing an AD environment, and I have expanded upon the lessons to demonstrate my understanding of AD concepts and their practical applications.

#Purpose

The goal of this project is to:
  - Learn how to design, deploy, and manage an Active Directory environment.
  - Develop hands-on skills in configuring various AD services such as Group Policy, DNS, and user account management.
  - Showcase my ability to follow technical documentation, troubleshoot issues, and enhance the lab environment with additional features.

#Lab Setup

Components

The Active Directory lab includes:

Domain Controller: Windows Server configured as the central AD node.

Client Machines: Virtualized Windows and Linux clients joined to the domain.

Networking: A simulated private network with DNS and DHCP services configured.

Tools and Utilities: PowerShell, RSAT tools, and other administrative tools for managing the environment.

Software Used

Virtualization: VMware Workstation / VirtualBox / Hyper-V

Operating Systems: Windows Server 2022, Windows 10, and Linux

Additional Tools: Sysinternals Suite, Wireshark, and MyDFIR-suggested utilities

Configuration Steps

Virtual Machine Setup: Created virtual machines for the domain controller and client machines.

AD Domain Setup: Installed Active Directory Domain Services (AD DS) and promoted the server to a domain controller.

DNS Configuration: Configured DNS zones for domain name resolution.

Group Policies: Implemented policies for user and computer settings.

User and Group Management: Created and managed users, groups, and organizational units (OUs).

Additional Features: Set up File Sharing, Remote Desktop, and other services.

Enhancements

In addition to the foundational lab setup, I:

Automated routine tasks using PowerShell scripts.

Configured auditing and logging for security monitoring.

Simulated real-world scenarios such as privilege escalation and account lockouts to practice incident response.

Documented troubleshooting steps and resolutions for common AD issues.

Key Takeaways

Skills Developed

Active Directory Administration: Gained a solid understanding of AD concepts and best practices.

Scripting and Automation: Used PowerShell to simplify administrative tasks and enforce consistency.

Networking Fundamentals: Configured and troubleshot network components critical to AD.

Problem-Solving: Resolved challenges encountered during the lab setup and configuration.

Documentation

Comprehensive documentation of each step, configuration, and enhancement made to the lab environment.

Clear explanations of the purpose and functionality of each component.

How to Use This Repository

Clone the repository: git clone https://github.com/yourusername/active-directory-lab.git

Review the documentation in the docs/ folder for detailed setup instructions and configurations.

Explore the PowerShell scripts in the scripts/ folder for automation examples.

Future Plans

Expand the lab to include additional services like Certificate Services and Federation Services.

Integrate SIEM tools for advanced monitoring and analysis.

Explore hybrid environments by connecting the lab to Azure Active Directory.

Conclusion

This lab has been an invaluable learning experience, allowing me to build practical skills in Active Directory administration and related technologies. By showcasing this project, I aim to demonstrate my ability to work independently, troubleshoot complex issues, and continuously improve my technical expertise.

Contact

If you have any questions or suggestions, feel free to reach out via GitHub or LinkedIn.


