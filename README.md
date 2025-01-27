## Overview
This project involves setting up a home lab environment using VirtualBox to simulate a small Active Directory infrastructure with two Windows 10 machines, a Kali Linux machine for penetration testing, and a Splunk machine for telemetry and log analysis. The environment was configured to simulate security attacks on an Active Directory domain, collect telemetry data, and analyze potential vulnerabilities.

**Lab Configuration:**
- VirtualBox Version: [Your Version]
- Operating Systems:
  - Windows 10 (Target Machine) – Vulnerable machine for attack simulation.
  - Windows 10 (Domain Controller) – Promoted to Active Directory Domain Controller.
  - Kali Linux – Penetration testing and attack simulation.
  - Splunk – Log and telemetry collection.

**Key Components:**
- Active Directory (AD) Domain Controller (DC)
- User and Organizational Unit (OU) management
- Static IP configurations for network communication
- Sysmon and Splunk Universal Forwarder for advanced telemetry collection
- Security testing tools such as Atomic Red Team, Crowbar, and PowerShell.
 
## Environment Setup

**1.1 Virtual Machine Configuration**

Windows 10 (Target Machine):
  - Installed Windows 10 and configured a static IP.
  - This machine acts as the target for penetration testing.

Windows 10 (Domain Controller):
  - Installed Windows 10 and promoted it to a Domain Controller using Active Directory Domain Services (AD DS).
  - Configured a static IP.
  - The machine acts as the Domain Controller for the lab.

Kali Linux:
  - Installed Kali Linux as the penetration testing machine.
  - Used tools like Crowbar for brute-force attacks and Atomic Red Team for simulating adversary techniques.

Splunk:
  - Installed Splunk for collecting logs and telemetry data.
  - Configured Splunk to capture security-related events from the Active Directory Domain Controller and the target machine.

1.2 Network Configuration
All machines were assigned static IPs to ensure reliable communication within the isolated lab network.

 ## Active Directory Domain Setup
 
**2.1 Domain Controller Configuration**
- Windows 10 (Domain Controller) was promoted to a Domain Controller:
  - Installed Active Directory Domain Services (AD DS).
  - Promoted the machine to a domain controller for the domain: lab.local.
  - Configured DNS for the domain and ensured DNS resolution was functioning between machines.

**2.2 Organizational Units (OUs) & User Management**

- Created several Organizational Units (OUs) within Active Directory:
  - Users OU: To store user accounts.
  - Admins OU: For administrative user accounts and groups.
- Users were created with appropriate roles and permissions.
- Password policies were configured as part of the Active Directory security hardening process.
- Example of tasks completed:
  - Created users: E.g., john.doe, jane.smith, etc.
  - Reset user passwords for testing purposes.
  - Disabled accounts for test scenarios.
  - Granted permissions to other servers to join the domain.

**2.3 Domain Controller Testing**
- Successfully joined the target machine to the domain (lab.local).
- Ensured replication of AD information across all domain controllers.
- Verified Group Policy Objects (GPOs) were applied correctly.
 
 ## Penetration Testing
 
**3.1 Simulating a Brute Force Attack (Crowbar on Kali Linux)**
- Crowbar was used to simulate a brute-force attack on a user account on the Windows 10 Target Machine.
  - The attack targeted the Windows login using common password lists.
  - Successfully gained access to the target machine after multiple attempts.

**3.2 Telemetry Collection in Splunk**
- The Splunk server was configured to receive logs and telemetry data from:
  - Windows Event Logs on the Domain Controller.
  - Security logs for failed login attempts, account lockouts, and successful authentication.
  - Kali Linux logs for penetration testing activities (such as brute-force attempts).
- Splunk dashboards were created to visualize:
  - Authentication failures and successes.
  - User account lockouts.
  - Attack attempts (e.g., brute force) against the domain.

**3.3 Atomic Red Team Execution (PowerShell Attacks)**
- Installed and configured Atomic Red Team on the Domain Controller for attack simulation.
- PowerShell-based attacks were executed to simulate various adversary tactics:
  - Privilege escalation via exploiting misconfigured permissions.
  - Persistence mechanisms.
  - Command and Control (C2) communication testing.

**3.4 Telemetry on Kali Linux**
- The Kali Linux machine executed simulated attacks using Atomic Red Team tools.
- The telemetry from the executed attacks (e.g., PowerShell exploitation) was captured in Splunk.

## Sysmon and Splunk Universal Forwarder Setup

**4.1 Installing Sysmon**
- Sysmon (System Monitor) was installed on both the ADDC (Domain Controller) and the Target Machine to provide enhanced monitoring and detailed event logging.
  - Sysmon captures detailed event data such as process creation, network connections, file creation timestamps, and more.
  - Sysmon Configuration File was customized to ensure that relevant events (such as suspicious PowerShell execution and process injections) were captured.

**4.2 Installing Splunk Universal Forwarder**
The Splunk Universal Forwarder was installed on both the ADDC and Target Machine to forward Sysmon logs to the Splunk instance for centralized log analysis.
Configured forwarding of logs, including Sysmon data, Windows Event Logs, and security events.
Ensured that both machines were correctly sending telemetry data to the Splunk server for analysis.

**4.3 Configuration and Testing**
Logs from Sysmon and Splunk Universal Forwarder were monitored in Splunk:
Created custom Splunk queries to analyze Sysmon logs for signs of unusual or malicious behavior, such as:
PowerShell command execution.
Network connections to suspicious external IPs.
Process creations that are out of the ordinary (e.g., by known malicious tools).
Successfully analyzed and visualized Sysmon logs alongside Windows Event Logs to get a full picture of activities on both the Domain Controller and Target machine.

## Lab Security Insights & Results

**5.1 Security Observations**
The Brute Force Attack simulated using Crowbar successfully targeted weak or easily guessable passwords on user accounts. This highlights the importance of strong password policies.
PowerShell-based attacks from Atomic Red Team demonstrated the need for:
Proper Group Policy enforcement.
Privilege escalation protections.
Audit logging to track malicious activities.
Sysmon significantly enhanced visibility into system-level activities, providing detailed insights into processes and network activities.

**5.2 Telemetry Analysis**
The Splunk dashboards provided clear insights into the attack behavior, including:
Failed login attempts.
Account lockouts due to brute-force attempts.
PowerShell activity associated with the execution of Atomic Red Team tests.
Sysmon logs were invaluable for detecting advanced attack techniques, such as lateral movement or PowerShell abuse.
Splunk Universal Forwarder ensured continuous log forwarding from all machines, providing a comprehensive view of the system activity.

##Conclusion
This project demonstrated the setup and security testing of an Active Directory environment using VirtualBox. The penetration testing simulated common attack techniques and helped identify weaknesses in user account management and Active Directory security. The Sysmon and Splunk Universal Forwarder setup enhanced the ability to monitor, collect, and analyze telemetry data. The Splunk dashboards proved invaluable in detecting and analyzing malicious activities.

**Key Takeaways:**
Always use strong password policies and MFA to protect user accounts.
Regularly monitor Windows Event Logs, Sysmon logs, and Splunk to identify suspicious activities.
Use tools like Atomic Red Team to simulate real-world attacks and test your defenses.
Implement Group Policy Objects (GPOs) to enforce security best practices across your domain.

## Future Enhancements
Expand Telemetry:
Include additional tools like OSQuery or Zeek for enhanced visibility into system behavior.

Simulate Advanced Attacks:
Implement lateral movement techniques, including Pass-the-Hash and Kerberos ticket attacks.

Integrate SIEM Systems:
Further enhance Splunk by integrating additional SIEM features or testing with a Blue Team for detection response.

## Files & Tools Used

**Operating Systems:**
- Windows 10 ISO (for Domain Controller and Target Machine).
- Kali Linux ISO (for Penetration Testing).
- Splunk (for log analysis).

**Tools:**
- Crowbar (for Brute Force Attack).
- Atomic Red Team (for simulating attack techniques via PowerShell).
- Sysmon (for system monitoring).
- Splunk Universal Forwarder (for log forwarding).
- VirtualBox (for virtualization).

## References & Resources
- Microsoft Active Directory Documentation
- Splunk Documentation
- Atomic Red Team GitHub
- Sysmon Documentation
- Splunk Universal Forwarder Documentation
