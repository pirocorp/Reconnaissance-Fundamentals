# Linux Fundamentals

Linux is a family of open-source Unix-like operating systems based on the Linux kernel, first released by Linus Torvalds on September 17, 1991. Linux is typically packaged as a Linux distribution (distro), which includes the kernel and supporting system software and libraries, many of which are provided by the GNU Project.

Linux is available in over 600 distributions (or an operating system based on the Linux kernel and supporting software and libraries). Some of the most popular and well-known are Ubuntu, Debian, Fedora, OpenSUSE, elementary, Manjaro, Gentoo Linux, RedHat, and Linux Mint.

## Philosophy

Linux follows five core principles:

- **Everything is a file** - All configuration files for the various services running on the Linux operating system are stored in one or more text files.
- **Small, single-purpose programs** - Linux offers many different tools that we will work with, which can be combined to work together.
- **Ability to chain programs together to perform complex tasks** -	Integrating and combining different tools enable us to carry out many large and complex tasks, such as processing or filtering specific data results.
- **Avoid captive user interfaces** -	Linux is designed to work mainly with the shell (or terminal), which gives the user greater control over the operating system.
- **Configuration data is stored in a text file** - An example of such a file is the `/etc/passwd` file, which stores all users registered on the system.


## Components

- **Bootloader** - Code that runs to guide the booting process and start the operating system. Kali Linux uses the GRUB Bootloader.
- **OS Kernel** - The kernel is the main component of an operating system. It manages the resources for the system's I/O devices at the hardware level.
- **Daemons** - Background services are called "**daemons**" in Linux. They ensure that key functions such as scheduling, printing, and multimedia work correctly. These small programs load after we boot or log into the computer.
- **OS Shell** - The operating system shell or the _command language interpreter_ (the command line) is the interface between the OS and the user. This interface allows the user to tell the OS what to do. The most commonly used shells are Bash, Tcsh/Csh, Ksh, Zsh, and Fish.
- **Graphics server** - This provides a graphical subsystem (server) called "X" or "X-server" that allows graphical programs to run locally or remotely on the X-windowing system.
- **Window Manager** - Also known as a graphical user interface (GUI). There are many options, including GNOME, KDE, MATE, Unity, and Cinnamon. A desktop environment usually has several applications, including file and web browsers. These allow the user to access and manage an operating system's essential and frequently accessed features and services.
- **Utilities** -	Applications or utilities are programs that perform particular functions for the user or another program.


## Linux Architecture

The Linux operating system can be broken down into layers:

- **Hardware** - Peripheral devices such as the system's RAM, hard drive, CPU, etc.
- **Kernel** - The **core of the Linux operating system**, the kernel **virtualizes and controls common computer hardware resources** like CPU, allocated memory, accessed data, and others. The kernel gives each process its own virtual resources and prevents/mitigates conflicts between different processes.
- **Shell** - A command-line interface (**CLI**), also known as a shell, where users can enter commands to execute the kernel's functions.
- **System Utility** - Makes the operating system's functionality available.


## [File System, Files and Directories](File%20System.md)

The Linux operating system is structured in a tree-like hierarchy.


## Basic Commands

### Getting Help

| Command 	| Description                                                                                             	                  | Example                             	|
|---------	|---------------------------------------------------------------------------------------------------------------------------	|-------------------------------------	|
| man    	  | The man (manual) command is an important tool that provides detailed information about Linux commands and programs. 	      | ```man grep``` 	                      |
| apropos   | Each manual page has a short description available. This tool searches the descriptions for instances of a given keyword. 	| ```apropos sudo``` 	                  |
| echo    	| Output any text that we provide                                                                         	                  | ```echo "Hello World!"```           	|
| cat     	| Outputting the Contents of a File                                                                       	                  | ```cat access.log```                	|
| grep    	| The grep command allows us to search the files' contents for specific values we are looking for.                            | ```grep "THM*" access.log``` 	        |

### System Information

| Command  | Description                                                                                                                        |
|----------|------------------------------------------------------------------------------------------------------------------------------------|
| whoami   | Displays current username.                                                                                                         |
| id       | Returns users identity                                                                                                             |
| hostname | Sets or prints the name of the current host system.                                                                                |
| uname    | Prints basic information about the operating system name and hardware.                                                             |
| pwd      | Returns working directory name.                                                                                                    |
| ifconfig | The ifconfig utility assigns or views an address to a network interface and/or configures network interface parameters.            |
| ip       | IP is a utility that shows or manipulates routing, network devices, interfaces, and tunnels.                                       |
| netstat  | Shows network status.                                                                                                              |
| ss       | Another utility to investigate sockets.                                                                                            |
| ps       | Shows process status.                                                                                                              |
| who      | Displays who is logged in.                                                                                                         |
| env      | Prints environment or sets and executes command.                                                                                   |
| lsblk    | Lists block devices.                                                                                                               |
| lsusb    | Lists USB devices                                                                                                                  |
| lsof     | Lists opened files.                                                                                                                |
| lspci    | Lists PCI devices.                                                                                                                 |


## Basic Shell Operators

| Operator 	| Description                                                                                                                                      	|
|----------	|--------------------------------------------------------------------------------------------------------------------------------------------------	|
| &        	| This operator allows you to run commands in your terminal's background.                                                                         	|
| &&       	| This operator allows you to combine multiple commands in one line of your terminal.                                                             	|
| >        	| This operator is a redirector - meaning that we can take the output from a command (such as using cat to output a file) and direct it elsewhere. 	|
| >> 	      | This operator does the same function as the > operator but appends the output rather than replacing it (meaning nothing is overwritten).         	|










