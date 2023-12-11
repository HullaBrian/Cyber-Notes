```
Next, we have been asked to duplicate the group policy `Logon Banner`, rename it `Security Analysts Control`, and modify it to work for the new Analysts OU. We will need to make the following changes to the Policy Object:

- we will be modifying the Password policy settings for users in this group and expressly allowing users to access PowerShell and CMD since their daily duties require it.
- For computer settings, we need to ensure the Logon Banner is applied and that removable media is blocked from access.

Once done, make sure the Group Policy is applied to the `Security Analysts` OU. This will require the use of the Group Policy Management snap-in found under `Tools` in the Server Manager window. For more of a challenge, the `Copy-GPO` cmdlet in PowerShell can also be utilized.
```
![[Pasted image 20231210193755.png]]
- To move the logon banner:
	- `Copy-GPO -SourceName "Logon Banner" -TargetName "Security Analysts Control"`
- The instructions were inconsistent with naming conventions, but the command:
	- `New-GPLink -Name "Security Analysts Control" -Target "ou=Analysts,ou=IT,OU=HQ-NYC,OU=Employees,OU=Corp,dc=INLANEFREIGHT,dc=LOCAL" -LinkEnabled Yes
![[Pasted image 20231210194954.png]]
