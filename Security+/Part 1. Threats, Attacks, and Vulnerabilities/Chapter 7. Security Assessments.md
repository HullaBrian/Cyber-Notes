# Thread Hunting
- searching for cyber threats that are inside a network but remain undetected
- uses tools, techniques, and procedures (TTPs) to uncover unauthorized actors in the network
- Indicators of -
	- Indicators of attack comprise a series of actions an attacker must accomplish to perform an attack
	- Indicators of compromise are artifacts left behind by the activities of an attacker
## Intelligence Fusion
- enables a defender to identify and contextualize the threads they face in the environment using the information from thread intelligence in the Diamond Model of Intrusion Analysis
## Threat Feeds
- sources of information concerning adversaries
## Advisories and Bulletins
- published sets of information from partners, such as security vendors, industry groups, the government, information-sharing groups, and other sources of “trusted” information
## Maneuver
- the ability to move within a network, a tactic commonly used by advanced adversaries as they move toward their objectives
- A defender can counter an attacker's maneuvers by 
	- watch traffic at choke points (points where the attacker MUST go through)
	- analyze the company's own network infrastructure through the eyes of an attacker
# Vulnerability Scans
- the process of examining services on computer systems for known vulnerabilities in software
### False Positives/Negatives
### Log Reviews
### Credentialed vs. Non-Credentialed
- Non-credentialed provide a view of a true outsider on the network
- Credentialed vulnerability scans can look deeper into a host and return more accurate and critical risk information
### Intrusive vs Non-Intrusive
- Non-intrusive scans are simple scans for open ports and services
- Intrusive scans attempt to leverage potential vulnerabilities through an exploit
### Application
- Vulnerability scans assess the strength of a deployed application against the desired performance of the system when being attacked.
### Web Application
- a web application is like an invitation to explore how well it is secured
### Network
### Common Vulnerabilities and Exposures (CVE)/ Common Vulnerability Scoring System (CVSS)
<img src="https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260464016/files/f0172-01.jpg" alt="Images" width="459" height="172">
### Configuration Review
# Syslog/Security Information and Event Management (SIEM)
- Syslog stands for System Logging Protocol, and it is used in Linux to send system log and event messages to a remote server
- A syslog server just has raw logs, so a SIEM is used to collect, aggregate, and apply pattern matching
- Steps for a SIEM
	- Collect data into a series of structured tables
	- Data tables are then enriched using lookups and other joining features to provide more context
	- Analyze data to find correlations and can be used to trigger incident response actions
## Review Reports
- SIEMs primarily output alerts or reports
## Packet Capture
- continuous packet capture allows the replay of traffic
## Data Inputs
- What is important is to define the outputs desired from the SIEM and then trace the necessary inputs from firewalls, network appliances, key servers, and so on to support those determinations.
## User Behavior Analysis
- Many modern SIEMs have modules that analyze end-user behaviors, looking for anomalous behavior patterns that indicate a need for analysis.
## Sentiment Analysis
## Security Monitoring
- the process of collecting and analyzing information to detect suspicious behavior or unauthorized changes on your network and connected systems
- Security orchestration, automation, and response (SOAR) systems complete the move to full cycle automation of security processes
## Log Aggregation
- The process of combining logs together
- During the process, the log entries can be parsed, modified, and have key fields extracted or modified based on lookups or rules
## Log Collectors
- Pieces of software that function to gather data from multiple independent sources and feed it into a unified source
# Security Orchestration, Automation, and Response (SOAR)
- Security orchestration, automation, and response (SOAR) systems take SIEM data as well as data from other sources and assist in the creation of runbooks and playbooks.
- 