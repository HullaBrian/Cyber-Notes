# Configuration Management
- Configuration management is essential to secure the system using the specific configuration the implementation intended
- Benchmark guides come from Center for Internet Security (CIS)
## Diagrams
- network diagrams that describe physical and logical connections, to annotated diagrams that provide essential settings
## Baseline Configuration
- the starting point for all future baseline assessments.
## Standard Naming Conventions
## IP Schema
# Data Sovereignty
- Data stored in a country is subject to that country's laws
## Data Protection
- the set of policies, procedures, tools, and architectures used to ensure proper control over the data in the enterprise
- Data security refers to the actions taken in the enterprise to secure data, wherever it resides: in transit/motion, at rest, or in processing.
## Data Loss Protection (DLP)
- prevent sensitive data from leaving the network without notice
- DLP solutions are designed to protect data in transit/motion, at rest, or in processing from unauthorized use or exfiltration.
### Masking
- hiding data by substituting altered values
- A mirror of a database is created and data is modified or redacted
### Encryption
- the use of sophisticated mathematical techniques to prevent persons with unauthorized access to data from actually reading the data
#### At Rest
#### In Transit/Motion

#### In Processing
### Tokenization
- the use of a random value to take the place of a data element that has traceable meaning
- Tokenization uses a random value to take the place of a data element that has traceable meaning.
### Rights Management
- the systematic establishment of rules and order to the various rights that users can invoke over digital objects
## Geographical Considerations
- Laws in certain areas might apply to your organization if you store certain kinds of data (data on foreign citizens)
	- You might have to store data on foreign citizens only in their country
### Response and Recovery Controls
- Two elements have to be designed into the enterprise
	- Disaster Recovery (DR)
	- Business Continuity (BC)
## Secure Socket Layer (SSL) / Transport Layer Security (TLS) Inspection
- Appliances are provided encryption keys and receive encrypted traffic. They then decrypt the traffic and perform deep packet inspection. They then forward the traffic after encrypting it again
## Hashing
## API Considerations
## Site Resiliency
- Site resiliency considerations can be connected to the idea of restoration sites and their availability
- Offsite data backups are only part of the consideration - you have to have somewhere to process all that data
### Hot Sites
- fully configured environment, similar to the normal operating environment that can be operational quickly
### Warm Sites
- partially configured, usually having the peripherals and software but perhaps not the more expensive main processing computer that can be operational in a few days
### Cold Sites
- will have the basic environmental controls necessary to operate but few of the computing components necessary for processing
## Deception and Disruption
### Honeypots
- Server designed to act like a real server on a corporate network, but has fake data on it
- Honeynets are groups of honeypots
### Honeyfiles
- files that contain fake data and can trigger DLP solution alerts
### Honeynets
- A network designed to look like a corporate network
### Fake Telemetry
- synthetic network traffic designed to look like normal communications
### DNS Sinkhole
- a DNS provider that returns specific DNS requests with false results
- A DNS sinkhole is a deception and disruption technology that returns specific DNS requests with false results.
