# Systemd Overview
![[systemd-overview.png]]
```text
a system and service manager for Linux operating systems. When run as first process on boot (as PID 1), it acts as init system that brings up and maintains user space services. Separate instances are started for logged-in users to start their services.
```
- Location: /lib/systemd/systemd
- On *my* debian 12 system
	- /usr/sbin/init -> /lib/systemd/systemd

## Init Systems
- Init systems are the first process started during boot
- Started by the kernel during the boot process

- Init systems are used to:
	- bootstrap user space
		- <u>bootstrapping</u>: the process of loading the basic software into the memory of a computer after power-on or general reset, the kernel will load the operating system which will then take care of loading other device drivers and software as needed.
		- self-tests, loading configuration settings, loading a BIOS, resident monitors, a hypervisor, an operating system, or utility software. 
		- "the system pulls itself up by its bootstraps"
	- manage user processes

- Critics
	- Dependencies that reduce compatibility
	- Potentially bloated
	- Complexity increases attack surface

- Systemd's 3 general functions
	- A system and service manager
	- A software platform (serves as a basis for developing other software)
	- The glue between applications and the kernel (provides various interfaces that expose functionalities provided by the kernel)

- Starts processes in parallel (faster than sequential startup)
	- systemd uses sockets and d-bus to talk between processes
## Units
- Systemd provides a dependency system between various entities called "units" of 11 types
- A unit refers to any resource that the system knows how to operate on and manage
	- standardized representation of system resources that can be managed by the suite of daemons and manipulated by the provided utilities.
- Units encapsulate objects that are relevant for system boot-up and maintenance

- Unit types
	- Service
		- Start and control daemons along with the processes they consist of
	- Socket
		- Encapsulate local IPC/network sockets
	- Target
		- Useful to group units, or provide synchronization points during boot
	- Device
		- Expose kernel devices in systemd and may be used to implement device-based activation
	- Mount
		- Control mount points in the file system
	- Automount
		- provide automount capabilities, for on-demand file system mounting and parallelized boot
	- Timer
		- Useful for triggering activation of other units
	- Swap
		- Encapsulates SWAP partitions or files of the OS
	- Path
		- May be used to activate other services when file system objects change or are modified
	- Slice
		- May be used to group units which manage system processes in a hierarchical tree for resource management purposes
	- Scope
		- Manage foreign processes instead of starting them as well

- Units are named as their configuration files
# Startup Files

## Creation

## Dependencies

## Structure

# Systemd Folder

# Systemd Alternatives
## Systemv

## Xinit / init-d

# Persistence Methods
