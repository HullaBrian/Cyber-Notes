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

# Startup Files

## Creation

## Dependencies

## Structure

# Systemd Folder

# Systemd Alternatives
## Systemv

## Xinit / init-d

# Persistence Methods
