- Difference between groups and OUS: groups are primarily for assigning permissions to access resources while OUs delegate administrative tasks to users (resetting passwords)
# Types of Groups
- Groups are used to place objects into management units that provide ease of administration
- Two fundamental characteristics of groups
	- type
		- defines the group's purpose
	- scope
		- shows how the group can be used within the domain or forest
- Two main types of group
	- security
		- primarily for ease of assigning permissions and rights to a collection of users instead of one at a time
	- distribution
		- used by email applications to distribute messages to group members
		- function like mailing lists and allow for auto-adding emails in the "To" field
		- Cannot be used to assign permissions to resources in a domain environment
# Group Scopes
There are 3 different group scopes that can be assigned:

- Domain Local Group
	- can only be used to manage permissions to domain resources in the domain where it was created
	- cannot be used in other domains but CAN contain users from OTHER domains
	- can be nested into other local groups but NOT within global groups
- Global Group
	- used to grant access to resources in another domain
	- can only contain accounts from the domain where it was created
	- can be added to both other global groups and local groups
- Universal Group
	- used to manage resources distributed across multiple domains and can be given permissions to any object within the same forest
	- available to all domains and can contain users from any domain

```
It is recommended that administrators maintain other groups (such as global groups) as members of universal groups because global group membership within universal groups is less likely to change than individual user membership in global groups. Replication is only triggered at the individual domain level when a user is removed from a global group. If individual users and computers (instead of global groups) are maintained within universal groups, it will trigger forest-wide replication each time a change is made
```

```powershell-session
PS C:\htb> Get-ADGroup  -Filter * |select samaccountname,groupscope

samaccountname                           groupscope
--------------                           ----------
Administrators                          DomainLocal
Users                                   DomainLocal
Guests                                  DomainLocal
Print Operators                         DomainLocal
Backup Operators                        DomainLocal
Replicator                              DomainLocal
Remote Desktop Users                    DomainLocal
Network Configuration Operators         DomainLocal
Distributed COM Users                   DomainLocal
IIS_IUSRS                               DomainLocal
Cryptographic Operators                 DomainLocal
Event Log Readers                       DomainLocal
Certificate Service DCOM Access         DomainLocal
RDS Remote Access Servers               DomainLocal
RDS Endpoint Servers                    DomainLocal
RDS Management Servers                  DomainLocal
Hyper-V Administrators                  DomainLocal
Access Control Assistance Operators     DomainLocal
Remote Management Users                 DomainLocal
Storage Replica Administrators          DomainLocal
Domain Computers                             Global
Domain Controllers                           Global
Schema Admins                             Universal
Enterprise Admins                         Universal
Cert Publishers                         DomainLocal
Domain Admins                                Global
Domain Users                                 Global
Domain Guests                                Global
```
- A Global Group can only be converted to a Universal Group if it is NOT part of another Global Group.
- A Domain Local Group can only be converted to a Universal Group if the Domain Local Group does NOT contain any other Domain Local Groups as members.
- A Universal Group can be converted to a Domain Local Group without any restrictions.
- A Universal Group can only be converted to a Global Group if it does NOT contain any other Universal Groups as members.

## Built-in vs. Custom Groups
- Built-in groups
	- Domain Admins
		- global security group
		- can only contain certain accounts from its own domain
## Important Group Attributes
- cn (command name): the name of the group
- member: which user, group, and contact objects are members of the group
- groupType: integer that specifies the group type and scope
- memberOf: listing of any groups that contain the group as a member (nested group membership)
- objectSid: the SID of the group
# Questions
- What group type is best utilized for assigning permissions and right to users?
	- `security`
- True or False; A "Global Group" can only contain accounts from the domain where it was created.
	- `True`
- Can a Universal group be converted to a Domain Local group? (yes or no)
	- `yes`