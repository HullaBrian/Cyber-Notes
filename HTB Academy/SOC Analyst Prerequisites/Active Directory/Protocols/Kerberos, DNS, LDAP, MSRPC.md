- Active Directory uses
	- lightweight directory access protocol (LDAP)
	- Microsoft's version of Kerberos
	- DNS for authentication and communication
	- MSRPC
		- Microsoft implementation of Remote Procedure Call (RPC)
		- Interprocess communication technique used for client-server model-based applications
# Kerberos
- Authentication protocol that uses mutual authentication (both user and server verify identity)
- Stateless - uses tickets instead of transmitting passwords
- ADDS has a Kerberos Key Distribution Center (KDC)
	- Computers attempting to authenticate a user encrypts a request with the password
	- If the KDC can decrypt the request, it creates a Ticket Granting Ticket (TGT) and gives it to the user
	- User presents their TGT to a DC to request a Ticket Granting Service (TGS) ticket which is encrypted with the service's NTLM password hash
	- The client requests access to the service by presenting the TGS, which decrypts it with its password hash.
- Uses port 88
![[Kerberos Authentication.png]]
# DNS
- ADDS uses DNS to allow clients to locate Domain Controllers and for Domain Controllers that host AD to communicate amongst themselves

- Forward DNS Lookup
	- Allows the lookup of all DC IP Addresses
- Reverse DNS Lookup
	- Find DNS name of a single host using the IP
# LDAP
- Lightweight Directory Access Protocol (LDAP)
- Provides authentication against directory services (AD)
- Uses port 389, LDAP over SSL (LDAPS) uses port 636
- LDAP is how systems in the network "speak" to AD
	- LDAP session begins by connecting to an LDAP server
## AD LDAP Authentication
1. `Simple Authentication`: a username and password create a BIND request to authenticate to the LDAP server; includes anonymous, unauthenticated, and username/password authentication.
2. `SASL Authentication`: The Simple Authentication and Security Layer (SASL) uses Kerberos to bind to the LDAP server then uses that service to authenticate to LDAP
- LDAP authentication messages are sent in CLEARTEXT - use encryption
# MSRPC
- Microsoft Remote Procedure Call - an interprocess communication technique
- Windows systems uses MSRPC to access systems in AD using 4 RPC interfarces

| Interface Name 	|                                                                                                                                                                                                                                                                                                                                                                                                                                                            Description                                                                                                                                                                                                                                                                                                                                                                                                                                                            	|
|:--------------:	|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:	|
| lsarpc         	| A set of RPC calls to the Local Security Authority (LSA)  system which manages the local security policy on a computer, controls  the audit policy, and provides interactive authentication services.  LSARPC is used to perform management on domain security policies.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          	|
| netlogon       	| Netlogon is a Windows process used to authenticate users and other  services in the domain environment. It is a service that continuously  runs in the background.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                	|
| samr           	| Remote SAM (samr) provides management functionality for the domain  account database, storing information about users and groups. IT  administrators use the protocol to manage users, groups, and computers  by enabling admins to create, read, update, and delete information about  security principles. Attackers (and pentesters) can use the samr  protocol to perform reconnaissance about the internal domain using tools  such as BloodHound  to visually map out the AD network and create "attack paths" to  illustrate visually how administrative access or full domain compromise  could be achieved. Organizations can protect  against this type of reconnaissance by changing a Windows registry key  to only allow administrators to perform remote SAM queries since, by  default, all authenticated domain users can make these queries to gather  a considerable amount of information about the AD domain. 	|
| drsuapi        	| drsuapi is the Microsoft API that implements the Directory  Replication Service (DRS) Remote Protocol which is used to perform  replication-related tasks across Domain Controllers in a multi-DC  environment. Attackers can utilize drsuapi to create a copy of the Active Directory domain database  (NTDS.dit) file to retrieve password hashes for all accounts in the  domain, which can then be used to perform Pass-the-Hash attacks to  access more systems or cracked offline using a tool such as Hashcat to  obtain the cleartext password to log in to systems using remote  management protocols such as Remote Desktop (RDP) and WinRM.                                                                                                                                                                                                                                                                            	|

# Questions
- What networking port does Kerberos use?
	- `88`
- What protocol is utilized to translate names into IP addresses? (acronym)
	- `DNS`
- What protocol does RFC 4511 specify? (acronym)
	- `LDAP`