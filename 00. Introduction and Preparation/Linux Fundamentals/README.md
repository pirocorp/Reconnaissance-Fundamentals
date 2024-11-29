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


## File System Hierarchy

The Linux operating system is structured in a tree-like hierarchy and is documented in the [Filesystem Hierarchy Standard (FHS)](https://www.pathname.com/fhs/). Linux is structured with the following standard top-level directories:

| Path   | Description                                                                                                                                                                                                                                                                                                  |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /      | The top-level directory is the root filesystem. It contains all of the files required to boot the operating system before other filesystems are mounted and the files required to boot the other filesystems. After boot, all other filesystems are mounted at standard mount points as root subdirectories. |
| /bin   | Contains essential command binaries.                                                                                                                                                                                                                                                                         |
| /boot  | Consists of the static bootloader, kernel executable, and files required to boot the Linux OS.                                                                                                                                                                                                               |
| /dev   | Contains device files to facilitate access to every hardware device attached to the system.                                                                                                                                                                                                                  |
| /etc   | Local system configuration files. Configuration files for installed applications may be saved here as well.                                                                                                                                                                                                  |
| /home  | Each user on the system has a subdirectory here for storage.                                                                                                                                                                                                                                                 |
| /lib   | Shared library files that are required for system boot.                                                                                                                                                                                                                                                      |
| /media | External removable devices such as USB drives are mounted here.                                                                                                                                                                                                                                        |
| /mnt   | Temporary mount point for regular filesystems.                                                                                                                                                                                                                                                               |
| /opt   | Optional files, such as third-party tools, can be saved here.                                                                                                                                                                                                                                                |
| /root  | The home directory for the root user.                                                                                                                                                                                                                                                                        |
| /sbin  | This directory contains executables for system administration (binary system files).                                                                                                                                                                                                                    |
| /tmp   | The operating system and many programs use this directory to store temporary files. This directory is generally cleared upon system boot and may be deleted at other times without warning.                                                                                                                  |
| /usr   | Contains executables, libraries, man files, etc.                                                                                                                                                                                                                                                             |
| /var   | This directory contains variable data files such as log files, email inboxes, web application-related files, cron files, and more.                                                                                                                                                                           |


## Basic Commands

### Getting Help

| Command 	| Description                                                                                             	                  | Example                             	|
|---------	|---------------------------------------------------------------------------------------------------------------------------	|-------------------------------------	|
| man    	  | The man (manual) command is an important tool that provides detailed information about Linux commands and programs. 	      | ```man grep``` 	                      |
| apropos   | Each manual page has a short description available. This tool searches the descriptions for instances of a given keyword. 	| ```apropos sudo``` 	                  |



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


### Files and Directories

#### Directory Navigation

| Command 	| Description                                                                                             	                  | Example                             	|
|---------	|---------------------------------------------------------------------------------------------------------------------------	|-------------------------------------	|
| pwd       | Returns working directory name.                                                                                             | ```pwd```                             |
| ls      	| Listing Files / Folders in Our Current Directory                                                                  	        | ```ls -l```                          	|
| cd      	| change directory                                                                                        	                  | ```cd folder1```                    	|


Example: ```ls -l``` 

![image](https://github.com/user-attachments/assets/fdaed98c-defb-444d-a047-663cc76a2dc6)

| Column Content | Description                                                                      |
|----------------|----------------------------------------------------------------------------------|
| `drwxr-xr-x`   | Type and permissions                                                             |
| 2              | Number of hard links to the file/directory                                       |
| root           | Owner of the file/directory                                                      |
| root           | Group owner of the file/directory                                                |
| 4096           | Size of the file or the number of blocks used to store the directory information |
| Aug  3  2021   | Date and time                                                                    |
| bin            | Directory name                                                                   |


Example: ```ls -la```

However, we will only see some things in this folder. A directory can also have hidden files that start with a dot at the beginning of its name (e.g., `.bashrc` or `.bash_history`). Therefore, we need to use the command ```ls -la``` to list all files of a directory:

![image](https://github.com/user-attachments/assets/bc16e4d0-437c-4c8c-a473-119fb3ddabc1)


#### Create, Move, Remove Directories and Files

| Command 	| Description                                                                                             	                  | Example                             	             |
|---------	|---------------------------------------------------------------------------------------------------------------------------	|--------------------------------------------------  |
| touch    	| Create an empty file                                                                                    	                  | ```touch <name>```                  	             |
| mkdir    	| create a directory                                                                                      	                  | ```mkdir <name>```                  	             |
| tree    	| Print directory tree                                                                                    	                  | ```tree .```           	                           |
| mv      	| Move / Rename file                                                                                      	                  | ```mv <file/directory> <renamed file/directory>``` |
| rm      	| Remove the current directory/file                                                                        	                  | ```rm filename``` or ```rm -r directory```         |


Example: We may want to have specific directories in the directory. The command `mkdir` has an option marked `-p` to add parent directories.

```bash
mkdir -p Storage/local/user/documents
tree .
```

![image](https://github.com/user-attachments/assets/e70c4f15-d776-4c54-a862-0e150822d49e)

Example: Let's rename the file info.txt to information.txt and move it to the directory Storage.

```bash
mv ./info.txt ./Storage/information.txt
```

![image](https://github.com/user-attachments/assets/cb8362e9-8bd7-4edc-bf3b-da0ea13a2e2d)


#### Editing Files

There are several ways to edit a file. The most common text editors are ```Vi``` and ```Vim```. More rarely, there is the ```Nano``` editor. 

Example: ```nano notes.txt```


#### Find Files and Directories

Finding the files and folders we need is crucial. Once we have gained access to a Linux-based system, we will need to find configuration files, scripts created by users or the administrator, and other files and folders. We do not have to manually browse through every folder and check when it was modified for the last time. There are some tools we can use to make this work easier.


##### Which

One of the standard tools is ```which```. This tool returns the path to the file or link that should be executed. This allows us to determine if specific programs, like ```cURL```, ```netcat```, ```wget```, ```python```, ```gcc```, are available on the operating system. 


##### Find

Another handy tool is ```find```. This tool finds files and folders and contains a function to filter the results. We can use filter parameters like the file size or the date. We can also specify whether we only search for files or folders.

![image](https://github.com/user-attachments/assets/be3d9782-f1d2-441b-bc96-21f98ff5b953)

Let us look at the options we used in the previous command.

| Option               | Description                                                                                                                                                                                                                                                                    |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -type f              | Hereby, we define the type of the searched object. In this case, 'f' stands for 'file'.                                                                                                                                                                                        |
| -name *.conf         | With '-name', we indicate the file name we seek. The asterisk (*) stands for 'all' files with the '.conf' extension.                                                                                                                                                           |
| -user root           | This option filters all files whose owner is the root user.                                                                                                                                                                                                                    |
| -size +20k           | We can filter all the located files and specify that we only want to see those larger than 20 KiB.                                                                                                                                                                             |
| -newermt 2020-03-03  | With this option, we set the date. Only files newer than the specified date will be presented.                                                                                                                                                                                 |
| -exec ls -al {} \\;  | This option executes the specified command, using the curly brackets as placeholders for each result. The backslash escapes the next character from being interpreted by the shell because otherwise, the semicolon would terminate the command and not reach the redirection. |
| 2>/dev/null          | This is a STDERR redirection to the 'null device', which we will return to in the next section. This redirection ensures that no errors are displayed in the terminal. This redirection must not be an option of the 'find' command.                                           |



##### Locate

It will take a lot of time to search the whole system for our files and directories and perform many different searches. The command ```locate``` offers us a quicker way to search through the system. In contrast to the ```find``` command, ```locate``` works with a local database that contains all information about existing files and folders. We can update this database with the following command.

```bash
sudo updatedb
```

If we now search for all files with the ".conf" extension, you will find that this search produces results much faster than using find. However, this tool does not have as many filter options that we can use. So it is always worth considering whether we can use the locate command or instead use the find command. It always depends on what we are looking for.

![image](https://github.com/user-attachments/assets/6c2716e8-abe6-4d14-8354-be79cf60748e)



#### File Descriptors and Redirections

##### File Descriptors

A file descriptor (FD) in Unix/Linux operating systems indicates a connection the kernel maintains to perform Input/Output (I/O) operations. In Windows-based operating systems, it is called filehandle. It is the connection (generally to a file) from the operating system that performs I/O operations (Input/output of bytes). By default, the first three file descriptors in Linux are:


- Data Stream for Input - STDIN – 0
- Data Stream for Output - STDOUT – 1
- Data Stream for Output that relates to an error occurring. - STDERR – 2


##### STDIN and STDOUT

Let us see an example with ```cat```. When running ```cat```, we give the running program our standard input (STDIN — FD 0), marked green, wherein, in this case, "SOME INPUT" is. As soon as we confirm our input with [ENTER], it is returned to the terminal as standard output (STDOUT — FD 1), marked red.

![image](https://github.com/user-attachments/assets/d0e77a2d-1cd8-4693-b5af-dd3694d0b9dc)


##### STDOUT and STDERR

In the following example, using the ``find `` command, we will see the standard output (STDOUT — FD 1) marked in green and the standard error (STDERR — FD 2) marked in red.

```bash
find /etc/ -name shadow
```

![image](https://github.com/user-attachments/assets/3d77acd7-35a8-410c-b488-19f9119ac41b)


In this case, the error is marked and displayed with "Permission denied." We can check this by redirecting the file descriptor for the mistakes (FD 2 - STDERR) to "/dev/null." This way, we redirect the resulting errors to the "null device," which discards all data.

```bash
find /etc/ -name shadow 2>/dev/null
```

![image](https://github.com/user-attachments/assets/b17ad65e-e770-48cf-9609-6fdd2291c7a6)



| Command 	| Description                                                                                             	                  | Example                             	|
|---------	|---------------------------------------------------------------------------------------------------------------------------	|-------------------------------------	|
| echo    	| Output any text that we provide                                                                         	                  | ```echo "Hello World!"```           	|
| cat     	| Outputting the Contents of a File                                                                       	                  | ```cat access.log```                	|
| grep    	| The grep command allows us to search the files' contents for specific values we are looking for.                            | ```grep "THM*" access.log``` 	        |



## Basic Shell Operators

| Operator 	| Description                                                                                                                                      	|
|----------	|--------------------------------------------------------------------------------------------------------------------------------------------------	|
| &        	| This operator allows you to run commands in your terminal's background.                                                                         	|
| &&       	| This operator allows you to combine multiple commands in one line of your terminal.                                                             	|
| >        	| This operator is a redirector - meaning that we can take the output from a command (such as using cat to output a file) and direct it elsewhere. 	|
| >> 	      | This operator does the same function as the > operator but appends the output rather than replacing it (meaning nothing is overwritten).         	|










