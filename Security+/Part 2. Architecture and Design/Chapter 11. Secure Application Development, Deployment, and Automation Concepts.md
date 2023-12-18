# Environments
- Environments provide isolation between functions of
	- development
	- testing
	- staging
	- production
## Development
- Meant for developing applications
- Does not need to scale
- Development needs to use the same OS type and version as used in the production environment
## Test
- Meant for testing software on a system that mirrors production as closely as possible
## Staging
- Optional environment
- commonly used when an organization has multiple production environments
- purpose of staging is to serve as a sandbox after testing, so the test system can test the next set while the current set is deployed across the enterprise.
## Production
- systems work with real data
- very few changes occur
## Quality Assurance
# Provisioning and Deprovisioning
- _Provisioning_ is the process of assigning permissions or authorities to objects.
- Deprovisioning is the removal of permissions or authorities.
- In secure coding, the practice is to provision a thread to an elevated execution permission level (for example, root) only during the time that the administrative permissions are needed
# Integrity Measurement
- Maintaining control over a codebase requires two things
	- Control over copies in such a way that people are only working on a legitimate codebase
	- Maintain a log of the changes and a method of identifying the versions
# Secure Coding Techniques
## Normalization
- the process of creating the canonical form, or simplest form, of a string before processing
## Stored Procedures
- Precompiled scripted methods of data access that are faster to execute, but are less flexible
## Obfuscation/Camouflage
- the hiding of obvious meaning from observation.
## Code Reuse and Dead Code
- For some complex functions, such as in cryptography, reuse is the preferred path. In other cases, where the lineage of a component cannot be established, the risk of use may outweigh the benefit.
- Dead code can be ok, but dead code removal tools can cause issues with security
## Server-Side vs. Client-Side Execution and Validation
- Do input validation on the server side
## Memory Management
## SDKs
- Once verified to be safe to use, SDKs and third party library help reduce risks
## Data Exposure
- the loss of control over data from a system during operations. 
# Open Web Application Security Project (OWASP)
- a nonprofit foundation dedicated to improving web-based application software security
# Software Diversity
- Different components with different software elements reduces impacts of common vulnerabilities in softwares
## Compilers
## Binaries
- Binary diversity randomizes memory layouts to defend against memory-based attacks
## Automation/Scripting
- DevOps is a combination of development and operations—in other words, a blending of tasks performed by a company’s application development and systems operations teams
# Automated Course of Action
## Continuous Monitoring
- Describes the technologies and processes employed to enable rapid detection of compliance issues and security risks
## Continuous Validation
- As code is changed in the DevOps process, the new code must be tested with the existing codebase to ensure functionality and stability
## Continuous Integration
- continuous integration allows for testing and updating even minor changes without a lot of overhead
- rather than several large updates, with many integrated and many potentially cross-purpose update elements, all squeezed into a single big package, a whole series of smaller single-purpose integrations is run
	- TLDR; bite sized updates to figure out what breaks what
## Continuous Delivery
- relies on automated testing and is an automated release process that enables the delivery of updates when they are complete, at any point of time, as opposed to a fixed release schedule
- releases are under operator control still
## Continuous Deployment
- continuous delivery on autopilot
- the release is automatic
- every change that pass all stages of your production pipeline is automatically released to customers.
# Elasticity
- something is capable of change without breaking
# Scalability
- characteristic of a software system to process higher workloads on its current resources (scale up) or on additional resources (scale out) without interruption
# Version Control
- tracking which version of a program is being worked on, whether in dev, test, or production