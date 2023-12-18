# Redundancy
Redundancy is the use of multiple, independent elements to perform a critical function, so that if one element fails, there is another that can take over the work
## Geographical Dispersal
## Disk
### Redundant Array of Inexpensive Disks (RAID) Levels
- RAID 0 (striped disks) simply spreads the data that would be kept on the one disk across several disks
	- data is split across all the drives with no redundancy offered.
- RAID 1 (mirrored disks) is the opposite of RAID 0. RAID 1 copies the data from one disk onto two or more disks
	- used to improve reliability and retrieval speed, but it is relatively expensive when compared to other RAID techniques.
- RAID 2 (bit-level error-correcting code) is not typically used, as it stripes data across the drives at the bit level as opposed to the block level
	- designed to be able to recover the loss of any single disk
- RAID 3 (byte-striped with error check) spreads the data across multiple disks at the byte level with one disk dedicated to parity bits
- RAID 4 (dedicated parity drive) stripes data across several disks but in larger stripes than in RAID 3, and it uses a single drive for parity-based error checking. 
- RAID 5 (block-striped with error check) is a commonly used method that stripes the data at the block level and spreads the parity data across the drives. 
	- Requires at least 3 drives

- Mirroring is writing data to two or more hard disk drives (HDDs) at the same time
- Striping breaks data into “chunks” that are written in succession to different disks.

- RAID 0 and 1 require atleast 2 drives
- RAID 3 and 5 require atleast 3 drives
- RAID 10(1+0) require atleast 4 drives
# Load Balancers
## NIC Teaming
## Power
## UPS
## Generator
## Dual Supply
## PDUs
- A managed power distribution unit (PDU) is a device designed to handle the electrical power for server racks
- The objective of a PDU is to efficiently convert the power, and manage the heat from the conversion, while producing a power flow that is conditioned from spikes and over/under voltage conditions
# Replication
- Having another copy of something - like a power supply
# Storage Area Network (SAN)
- A separate network optimized for storage
# VM
- VM replication is very noice
# Backup Types
- 4 types
	- Full
		- Copies ALL data
		- Takes 1 backup tape
	- Incremental
		- backs up only files that have changed since the last full or incremental backup occurred
		- To restore:
			- restore from the last full backup
			- restore from each incremental backup that has occurred since
	- Differential
		- Stores only the files that have been changed since the last full backup
		- To restore:
			- restore from the last full backup
			- restore from the most recent differential backup
	- Snapshot
		- A copy of a virtual machine at a time

- Image backups copy EVERYTHING - even deleted data and free space
# Nonpersistence
- Nonpersistence refers to system items that are not permanent and can change