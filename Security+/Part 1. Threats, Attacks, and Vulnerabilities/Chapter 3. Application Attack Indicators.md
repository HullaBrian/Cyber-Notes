- Privilege Escalation
- Cross-Site Scripting
	- Due to weak user input validation, an attacker can include a script in their input
	- 3 types
		- Non-persistent XSS attack: script is executed immediately
		- Persistent XSS attack: script is stored on the server
		- DOM-based XSS attack: script is executed in the browser via the Document Object Model (DOM) process as opposed to the web server
	- **Input validation is helpful at preventing XSS attacks.**
- Injection Attacks
	- SQL injection
		- manipulates backend SQL statements
		- Stored procedures are precompiled methods implemented within a database engine. This separates SQL queries from their inputs and is WAY more secure
	- XML injection
		- attacks LDAP
	- Command injection
	- DLL Injection
		- _dynamic-link library (DLL)_: a piece of code that can add functionality to a program through the inclusion of library routines linked at runtime
		- Adding an “evil” DLL in the correct directory, or via a registry key, can result in additional functionality being incurred.
	- LDAP injection
	- Pointer/Object Dereference
		- Mistakes in the input validation can lead to errors in the pointer dereference, which may or may not trigger an error, as the location will contain data and it will be returned
- Directory Traversal
	- Adding encoded symbols for "../.." in an unvalidated input box can result in the parser resolving the encoding to the traversal code
	- Sometimes, the symbols are encoded, which makes them hard to detect
- Buffer Overflow
	- Input buffers that are supposed to be a certain size are overflowed with data, causing either crashing or RCE
	- Buffer overflows are input validation attacks, designed to take advantage of input routines that do not validate the length of inputs
- A race condition, or a Time of Check/Time of Use Attack
	- an error condition that occurs when the output of a function is dependent on the sequence or timing of the inputs
	- the impact of a race condition is usually the failure of a system in the form of a crash. 
	- Race conditions can be combated with reference counters, kernel locks, and thread synchronization
- Improper Error Handling
- Improper Input Handling
- Replay attacks
	- Replay attacks work against applications by attempting to re-create the conditions that existed the first time the sequence of events occurred. If an attacker can record a series of packets and then replay them, what was valid before may well be valid again
- Session Replay Event
	- the re-creation of this interaction after it has occurred.
- Integer Overflow
	- a programming error condition that occurs when a program attempts to store a numeric value, which is an integer, in a variable that is too small to hold it.
## Request Forgery
- a class of attack where a user performs a state-changing action on behalf of another user, typically without their knowledge

- Server-Side Request Forgery
	- Attacker sends requests to the server-side application to make HTTP requests to an arbitrary domain of the attacker's choosing
- Cross-Site Request Forgery (XSRF)
	- utilize unintended behaviors that are proper in defined use but are performed under circumstances outside the authorized use
	-  The strongest method is the use of random XSRF tokens in form submissions
## Application Programming Interface (API) Attacks
## Resource Exhaustion
## Memory Leak
## Secure Sockets Layer (SSL) Stripping
- a man in the middle attack against all SSL and early versions of TLS connections
- intercepting the initial connection request for HTTPS, redirecting it to an HTTP site, and then mediating in the middle
## Driver Manipulation
## Shimming
- a process of putting a layer of code between the driver and the OS
- a means by which malicious code can change a driver’s behavior without changing the driver itself
## Refactoring
- the process of restructuring existing computer code without changing its external behavior
## Pass the Hash
