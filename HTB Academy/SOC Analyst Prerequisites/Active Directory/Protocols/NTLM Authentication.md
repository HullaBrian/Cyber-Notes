| Hash/Protocol 	|                Cryptographic technique               	| Mutual Authentication 	|           Message Type          	|               Trusted Third Party               	|
|:-------------:	|:----------------------------------------------------:	|:---------------------:	|:-------------------------------:	|:-----------------------------------------------:	|
| NTLM          	| Symmetric key cryptography                           	| No                    	| Random number                   	| Domain Controller                               	|
| NTLMv1        	| Symmetric key cryptography                           	| No                    	| MD4 hash, random number         	| Domain Controller                               	|
| NTLMv2        	| Symmetric key cryptography                           	| No                    	| MD4 hash, random number         	| Domain Controller                               	|
| Kerberos      	| Symmetric key cryptography & asymmetric cryptography 	| Yes                   	| Encrypted ticket using DES, MD5 	| Domain Controller/Key Distribution Center (KDC) 	|

# LM
- `LAN Manager` (LM or LANMAN)
- A hashing algorithm that is disabled by default due to security weaknesses
# NTHash (NTLM)
- NT LAN Manager (NTLM) hashes are present on modern windows systems
- Challenge-response authentication protocol that uses 3 messages to authenticate:
	- Client sends a `NEGOTIATE_MESSAGE` to the server
	- Server responds with a `CHALLENGE_MESSAGE` to verify the client identity
	- Client responds with an `AUTHENTICATE_MESSAGE`
- Hashes are stored in local SAM database or the NTDS.DIT database file on a DC
- Two hashed password values to choose from
	- LM Hash
	- NT Hash - `MD4(UTF-16-LE(passsword))`
![[NTLM Authentication Request.png]]
- Even though NT hashes are stronger than LM Hashes, they can still be brute forced in a reasonable amount of time: ~3 hours
- NT hashes take the form of `b4b9b02e6f09a9bd760f388b67351e2b`
- NTLM hashes look like: `Rachel:500:aad3c435b514a4eeaad3b935b51304fe:e46b9e548fa0d122de7f59fb6d48eaa2:::`
	- `Rachel` is the username
	- `500` is the Relative Identifier (RID) - 500 is the RID for the administrator account
	- `aad3c435b514a4eeaad3b935b51304fe` is the LM hash
	- `e46b9e548fa0d122de7f59fb6d48eaa2` is the NT hash.
# NTLMv1 (Net-NTLMv1)
- Challenge/response between a server and client using the NT Hash.
- NTMLv1 uses the NT AND LM hash, which makes it easier to crack offline
- Used for network authentication
- Server sends an 8-byte random number (challenge), client return 24-byte response
- Hashes CANNOT be used for pass-the-hash attacks
- NTLMv1 hash looks like:
`u4-netntlm::kNS:338d08f8e26de93300000000000000000000000000000000:9526fb8c23a90751cdd619b6cea564742e1e4bf33006ba41:cb8086049ec4736c
# NTLMv2 (Net-NTLMv2)
- A much more secure version of NTMLv1
- Hardened against spoofing attacks that NTLMv1 is susceptible to
- NTLMv2 hash looks like: `admin::N46iSNekpT:08ca45b7d7ea58ee:88dcbe4446168966a153a0064958dac6:5c7830315c7830310000000000000b45c67103d07d7b95acd12ffa11230e0000000052920b85f78d013c31cdb3b92f5d765c783030`
# Domain Cached Credentials (MSCache2)
- Hosts save the last 10 hashes for any domain users that successfully log into the machine in the `HKEY_LOCAL_MACHINE\SECURITY\Cache` registry key
- VERY hard to crack
- Example: `$DCC2$10240#bjones#e4e938d12fe5974dc42a90120bd9c90f`
- Cannot be used in pass the hash attacks
# Questions
-  What Hashing protocol is capable of symmetric and asymmetric cryptography? 
	- `Kerberos`
- NTLM uses three messages to authenticate; Negotiate, Challenge, and <__>. What is the missing message? (fill in the blank)
	- `Authenticate`
- How many hashes does the Domain Cached Credentials mechanism save to a host by default?
	- `10`
