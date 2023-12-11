# Local Accounts
- Accounts stored locally on a server/workstation
- Can be assigned rights either individually or by group membership, but they will not carry over to other machines on the network
- Default local user accounts
	- `Administrator`
		- SID of `S-1-5-domain-500`
		- Cannot be deleted or locked, but can disabled or renamed
	- `Guest`
		- Disabled by default
		- Provides temporary access with limited rights
	- `SYSTEM`
		- Has FULL access to nearly everything on the system
		- Service account that doesn't have a profile to sign into
	- `Network Service`
		- Predefined local account used by the Service Control Manager (SCM) for running Windows services
		- When a service runs in the context of this account, it will present credentials to remote services
	- `Local Service`
		- Predefined local account used by the Service Control Manager (SCM) for running Windows Services
		- Configured with minimal privileges on the computer and presents anonymous credentials to the network 
# Domain Users
- Users granted rights from the domain to access external resources such as file servers, printers, intranet hosts, and other objects
- Can log into any host on the domain
- The `KRBTGT` account
	- local account built into AD
	- a common target because it gives unrestricted access to the domain
	- can be leveraged for privilege escalation and persistence
# User Naming Attributes
Security can be improved using a set of user naming attributes to help identify user objects

|   |   |
|---|---|
|`UserPrincipalName` (UPN)|This is the primary logon name for the user. By convention, the UPN uses the email address of the user.|
|`ObjectGUID`|This is a unique identifier of the user. In AD, the ObjectGUID attribute name never changes and remains unique even if the user is removed.|
|`SAMAccountName`|This is a logon name that supports the previous version of Windows clients and servers.|
|`objectSID`|The user's Security Identifier (SID). This attribute identifies a user and its group memberships during security interactions with the server.|
|`sIDHistory`|This contains previous SIDs for the user object if moved from another domain and is typically seen in migration scenarios from domain to domain. After a migration occurs, the last SID will be added to the `sIDHistory` property, and the new SID will become its `objectSID`.|

````powershell-session
Get-ADUser -Identity htb-student
````

# Domain joined vs. Non-Domain-joined Machines
- `Domain Joined`
	- Machines that allow domain users to logon
	- Hosts joined to the domain will acquire any configuration/changes necessary through the domain's Group Policy
- `Non-Domain Joined`
	- Machines not managed by domain policy
	- Profiles are not migrated to other hosts within the workgroup
	- A machine account (`NT AUTHORITY\SYSTEM` level access) in an AD environment will have most of the same rights as a standard domain user account
		- Important because if a RCE or privilege escalation vulnerability is exploited which grants `SYSTEM` privilege, then domain enumeration is easy
# Questions
- True or False; A local user account can be used to login to any domain connected host.
	- `False`
- What default user account has the SID "S-1-5-domain-500" ?
	- `Administrator`
- What account has the highest permission level possible on a Windows host
	- `SYSTEM`
- What user naming attribute is unique to the user and will remain so even if the account is deleted?
	- `ObjectGUID`