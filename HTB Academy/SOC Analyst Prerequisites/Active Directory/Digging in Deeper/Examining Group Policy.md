# Group Policy Objects (GPOs)
- A [Group Policy Object (GPO)](https://docs.microsoft.com/en-us/previous-versions/windows/desktop/policy/group-policy-objects) is a virtual collection of policy settings that can be applied to `user(s)` or `computer(s)`. Include policies such as
	- screen lock timeout
	- disabling USB ports
	- enforcing a custom domain password policy
	- installing software
	- managing applications
	- customizing remote access settings
- Unique name and is assigned a GUID
# Examples
- Establishing different password policies for service accounts, admin accounts, and standard user accounts using separate GPOs
- Preventing the use of removable media devices (such as USB devices)
- Enforcing a screensaver with a password
- Restricting access to applications that a standard user may not need, such as cmd.exe and PowerShell
- Enforcing audit and logging policies
- Blocking users from running certain types of programs and scripts
- Deploying software across a domain
- Blocking users from installing unapproved software
- Displaying a logon banner whenever a user logs into a system
- Disallowing LM hash usage in the domain
- Running scripts when computers start/shutdown or when a user logs in/out of their machine

- Password complexity
	- Passwords must be at least 7 characters long.
	- Passwords must contain characters from at least three of the following four categories:
		- Uppercase characters (A-Z)
		- Lowercase characters (a-z)
		- Numbers (0-9)
		- Special characters (e.g. !@#$%^&*()_+|~-=`{}[]:";'<>?,./)

|                   Level                  |                                                                                                                                                                                                                                                                                                                                                                        Description                                                                                                                                                                                                                                                                                                                                                                       |
|:----------------------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| Local Group Policy                       | The policies are defined directly to the host locally outside the  domain. Any setting here will be overwritten if a similar setting is  defined at a higher level.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Site Policy                              | Any policies specific to the Enterprise Site that the host resides  in. Remember that enterprise environments can span large campuses and  even across countries. So it stands to reason that a site might have its  own policies to follow that could differentiate it from the rest of the  organization. Access Control policies are a great example of this. Say a  specific building or site performs secret or restricted  research and requires a higher level of authentication for access to  resources. You could specify those settings at the site level and ensure  they are linked so as not to be overwritten by domain policy. This is  also a great way to perform actions like printer and share mapping for  users in specific sites. |
| Domain-wide Policy                       | Any settings you wish to have applied across the domain as a whole.  For example, setting the password policy complexity level, configuring a  Desktop background for all users, and setting a Notice of Use and  Consent to Monitor banner at the login screen.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Organizational Unit (OU)                 | These settings would affect users and computers who belong to  specific OUs. You would want to place any unique settings here that are  role-specific. For example, the mapping of a particular share drive that  can only be accessed by HR, access to specific resources like printers,  or the ability for IT admins to utilize PowerShell and command-prompt.                                                                                                                                                                                                                                                                                                                                                                                        |
| Any OU Policies nested within other OU's | Settings at this level would reflect special permissions for objects  within nested OUs. For example, providing Security Analysts a specific  set of Applocker policy settings that differ from the standard IT  Applocker settings.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

# GPO Order of Precedence
![[gpo_levels.png]]
- The `Enforced` option to enforce settings in a specific GPO. If this option is set, policy settings in GPOs linked to lower OUs `CANNOT` override the settings
# Group Policy Refresh Frequency
- Group Policy refreshes are
	- 90 minutes +/- 30 for users and computers
	- 5 minutes for a domain controller
- When a new GPO is created and linked, it could take up to 2 hours (120 minutes)
- The interval can be changed under
	- `Computer Configuration --> Policies --> Administrative Templates --> System --> Group Policy` - select `Set Group Policy refresh interval for computers`
# Questions
- Computer settings for Group Policies are gathered and applied at a <___> minute interval? (answer is a number, fill in the blank )
	- `90`
- True or False: A policy applied to a user at the domain level would be overwritten by a policy at the site level.
	- `False`
- What Group Policy Object is created when the domain is created?
	- `Default Domain Policy`