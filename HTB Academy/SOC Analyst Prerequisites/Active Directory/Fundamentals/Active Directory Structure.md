# Introduction
- Active Directory, is a directory service for Windows network environments
	- Distributed, hierarchical structure that allows centralized management of an organization's resources (users, computers, groups, network devices and file shares, group policies, servers and workstations, and trusts)
	- Provides authentication AND authorization
- Active Directory Domain Services (AD DS) is a directory service
	- provides a way to store directory data and make it available to users and administrators <u>on the same network</u>
	- Stores information
		- usernames + passwords
	- Manages rights needed for authorized users to access stored information

**<u>AD is a database accessible to ALL users within the domain, regardless of privilege level</u>**
- A basic AD user account with no added privileges can enumerate most AD objects, including
	- Domain computers, users, and group information
	- Organizational Units (OUs)
	- Default Domain Policy
	- Functional Domain Levels
	- Password Policy
	- Group Policy Objects (GPOs)
	- Domain Trusts
	- Access Control Lists (ACLs)
# Structure
- AD is arranged in a hierarchical tree structure - a forest at the top contains 1 or more domains, which can have nested subdomains
	- A <u>forest</u> is the security boundary containing only objects under administrative control. It may contain multiple domains (with nested subdomains)
	- A <u>domain</u> is a structure that contains accessible objects (users, computers, groups).
		- Built in Organization Units (OUs)
			- Domain Controllers
			- Users
			- Computers
- Basic AD structure:
```shell-session
INLANEFREIGHT.LOCAL/
├── ADMIN.INLANEFREIGHT.LOCAL
│   ├── GPOs
│   └── OU
│       └── EMPLOYEES
│           ├── COMPUTERS
│           │   └── FILE01
│           ├── GROUPS
│           │   └── HQ Staff
│           └── USERS
│               └── barbara.jones
├── CORP.INLANEFREIGHT.LOCAL
└── DEV.INLANEFREIGHT.LOCAL
```
- Root domain: `INLANEFREIGHT.LOCAL`
- Subdomains:
	- `ADMIN.INLANEFREIGHT.LOCAL`
	- `CORP.INLANEFREIGHT.LOCAL`
	- `DEV.INLANEFREIGHT.LOCAL`
![[ad_forests.png]]
![[ilflog2.png]]
- 2 forests with a trust relationship (users in either forest can access the others resources)
	- `INLANEFREIGHT.LOCAL`
	- `FREIGHTLOGISTICS.LOCAL`
- Child domains in of a forest don't necessarily have trusts with the child domains in the other forest
# Questions
- What Active Directory structure can contain one or more domains?
	- `forest`
- True or False; It can be common to see multiple domains linked together by trust relationships?
	- `True`
- Active Directory provides authentication and <____> within a Windows domain environment.
	- `authorization`