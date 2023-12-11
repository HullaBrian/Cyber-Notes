- CIA Triad
	- Confidentiality
	- Integrity
	- Availability
![[CIA-triad-diag.png]]
# General AD Hardening Measures
- The [Microsoft Local Administrator Password Solution (LAPS)](https://www.microsoft.com/en-us/download/details.aspx?id=46899) is used to randomize and rotate local administrator passwords on Windows hosts and prevent lateral movement.
## LAPS
- A tool that automatically rotates passwords on a time interval
## Audit Policy Settings (Logging and Monitoring)
- Have logging/monitoring that looks at events
	- adding users or computers
	- modifying an object
	- changing an account password
	- accessing a system in an unauthorized or non-standard way
	- password spraying or Kerberos attacks
## Group Policy Security Settings
- Group Policy Objects (GPOs) are virtual collections of policy settings that can be applied to specific users, groups, and computers at the OU level
	- `Account Policies` manage how user accounts interact with the domain
		- password policy
		- account lockout policy
		- Kerberos-related settings (lifetime Kerberos tickets)
	- `Local Policies` apply to a specific computer
		- include the security event audit policy, user rights assignments, and specific security settings
	- `Software Restriction Policies` control what software can be run on a host
	- `Application Control Policies` control which applications can be run by certain users/groups.
		- Admins use AppLocker to restrict access to certain types of applications and files
	- `Advanced Audit Policy Configuration`
		- used to audit activities like file access/modification, account logon/logoff, policy changes, privilege usage, and more
## Update Management (SCCM/WSUS)
- Windows Server Update Service (WSUS) can be installed on a Windows Server and can minimize the task of patching windows systems.
- System Center Configuration Manager (SCCM) is a paid solution that brings more features
## Group Managed Service Accounts (gMSA)
- an account managed by the domain that offers a higher level of security than other types of service accounts for use with non-interactive applications, services, processes, and tasks that are run automatically but require credentials to run
- allows for credentials to be used across multiple hosts.
## Security Groups
- Help ensure you can assign granular permissions to users en masse instead of individually managing each user.
- Offer an easy way to assign access/permissions to network resources
## Account Separation
- Admins MUST have two separate accounts
	- One for day to day
	- Second for any administrative tasks they must perform
## Password Complexity Policies + Passphrases + 2FA
- standard complexity rules (>=12 characters, 3 out of 4 of uppercase, lowercase, number, and special character)
	- passwords should be COMPLEX
- Multi-factor authentication (MFA) for Remote Desktop Access it a good idea
## Limiting Domain Admin Account Usage
- Domain Admin accounts should only be used to log in to Domain Controllers, not personal workstations, jump hosts, web servers, etc
## Periodically Auditing and Removing Stale Users and Objects
- An organization should periodically audit Active Directory and remove or disable any unused accounts
## Auditing Permissions and Access
- Organizations should periodically perform access control audits to ensure that users only have the level of access required for their day-to-day work
## Audit Policies and Logging
- [Audit Policy Recommendations](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/plan/security-best-practices/audit-policy-recommendations)
- Visibility is a must - organizations can achieve this through logging and detection of anomalous activity
## Using Restricted Groups
- [Restricted Groups](https://social.technet.microsoft.com/wiki/contents/articles/20402.active-directory-group-policy-restricted-groups.aspx) allow for administrators to configure group membership via Group Policy
- Example: controlling membership in the local administrator's group on all hosts in the domain
## Limiting Server Roles
- It is important not to install additional roles on sensitive hosts, such as installing the Internet Information Server (IIS) role on a Domain Controller.
## Limiting Local Admin and RDP Rights
- Organizations should control which users have local admin rights on which computers
- If many users can RDP to one or many machines, this increases the risk of sensitive data exposure or potential privilege escalation attacks
# Questions
- Confidentiality, <<u>___</u>>, and Availability are the pillars of the CIA Triad. What term is missing? (fill in the blank)
	- `Integrity`
- What security policies can block certain users from running all executables?
	- `Application Control Policies`