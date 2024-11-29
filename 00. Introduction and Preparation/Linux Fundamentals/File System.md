# File System

The Linux file system is structured in a tree-like hierarchy and is documented in the [Filesystem Hierarchy Standard (FHS)](https://www.pathname.com/fhs/).

## File System Hierarchy

Linux is structured with the following standard top-level directories:

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



## Working with Files and Directories

### Directory Navigation

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


### Create, Move, Remove Directories and Files

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


### Editing Files

There are several ways to edit a file. The most common text editors are ```Vi``` and ```Vim```. More rarely, there is the ```Nano``` editor. 

Example: ```nano notes.txt```


### Find Files and Directories

Finding the files and folders we need is crucial. Once we have gained access to a Linux-based system, we will need to find configuration files, scripts created by users or the administrator, and other files and folders. We do not have to manually browse through every folder and check when it was modified for the last time. There are some tools we can use to make this work easier.


#### Which

One of the standard tools is ```which```. This tool returns the path to the file or link that should be executed. This allows us to determine if specific programs, like ```cURL```, ```netcat```, ```wget```, ```python```, ```gcc```, are available on the operating system. 


#### Find

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



#### Locate

It will take a lot of time to search the whole system for our files and directories and perform many different searches. The command ```locate``` offers us a quicker way to search through the system. In contrast to the ```find``` command, ```locate``` works with a local database that contains all information about existing files and folders. We can update this database with the following command.

```bash
sudo updatedb
```

If we now search for all files with the ".conf" extension, you will find that this search produces results much faster than using find. However, this tool does not have as many filter options that we can use. So it is always worth considering whether we can use the locate command or instead use the find command. It always depends on what we are looking for.

![image](https://github.com/user-attachments/assets/6c2716e8-abe6-4d14-8354-be79cf60748e)



### File Descriptors and Redirections

#### File Descriptors

A file descriptor (FD) in Unix/Linux operating systems indicates a connection the kernel maintains to perform Input/Output (I/O) operations. In Windows-based operating systems, it is called filehandle. It is the connection (generally to a file) from the operating system that performs I/O operations (Input/output of bytes). By default, the first three file descriptors in Linux are:


- Data Stream for Input - STDIN – 0
- Data Stream for Output - STDOUT – 1
- Data Stream for Output that relates to an error occurring. - STDERR – 2


#### STDIN and STDOUT

Let us see an example with ```cat```. When running ```cat```, we give the running program our standard input (STDIN — FD 0), marked green, wherein, in this case, "SOME INPUT" is. As soon as we confirm our input with [ENTER], it is returned to the terminal as standard output (STDOUT — FD 1), marked red.

![image](https://github.com/user-attachments/assets/d0e77a2d-1cd8-4693-b5af-dd3694d0b9dc)


#### STDOUT and STDERR

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


#### Redirect STDOUT to a File

Now we can see that all errors (STDERR) previously presented with "Permission denied" are no longer displayed. The only result we see now is the standard output (STDOUT), which we can also redirect to a file with the name results.txt that will only contain standard output without the standard errors.

```bash
find /etc/ -name shadow 2>/dev/null > results.txt
```

![image](https://github.com/user-attachments/assets/6598a20b-17fd-47bc-98ae-3a242f2b329d)


#### Redirect STDOUT and STDERR to Separate Files

We should have noticed that we did not use a number before the last example's greater-than sign (>). That is because we redirected all the standard errors to the "null device" before, and the only output we get is the standard output (FD 1 - STDOUT). To make this more precise, we will redirect standard error (FD 2 - STDERR) and standard output (FD 1 - STDOUT) to different files.

```bash
find /etc/ -name shadow 2> stderr.txt 1> stdout.txt
```

![image](https://github.com/user-attachments/assets/5ff81167-11f8-4726-8592-b0ae668efaa5)


#### Redirect STDIN

As we have already seen, combining the file descriptors can redirect errors and output with greater-than-character (>). This also works with the lower-than sign (<). However, the lower-than sign serves as standard input (FD 0 - STDIN). These characters can be seen as "direction" in the form of an arrow that tells us "from where" and "where to" the data should be redirected. We use the cat command to use the contents of the file "stdout.txt" as STDIN.

```bash
cat < stdout.txt
```

![image](https://github.com/user-attachments/assets/3649a9f9-fd81-494e-92e4-0013432f37bb)


#### Redirect STDOUT and Append to a File

When we use the greater-than sign (>) to redirect our STDOUT, a new file is automatically created if it does not already exist. If this file exists, it will be overwritten without asking for confirmation. If we want to append STDOUT to our existing file, we can use the double greater-than sign (>>).

```bash
find /etc/ -name passwd >> stdout.txt 2>/dev/null
```

![image](https://github.com/user-attachments/assets/ec1111bc-f9e4-4b9b-bf88-64e70ae00964)


#### Redirect STDIN Stream to a File

We can also use the double lower-than characters (<<) to add our standard input through a stream. We can use the so-called End-Of-File (EOF) function of a Linux system file, which defines the input's end. In the next example, we will use the cat command to read our streaming input through the stream and direct it to a file called "stream.txt."

```bash
cat << EOF > stream.txt
```

![image](https://github.com/user-attachments/assets/8277eeff-8882-4ddb-83ff-feea9d1cac8f)


#### Pipes

Another way to redirect STDOUT is to use pipes (|). These are useful when we want to use the STDOUT from one program to be processed by another. One of the most commonly used tools is grep, which we will use in the following example. Grep is used to filter STDOUT according to the pattern we define. In the following example, we use the find command to search for all files in the "/etc/" directory with a ".conf" extension. Any errors are redirected to the "null device" (/dev/null). We filter out the results using ```grep``` and specify that only the lines containing the pattern "systemd" should be displayed.

![image](https://github.com/user-attachments/assets/097431da-752c-4283-b4e1-d9ca886facd1)


The redirections work, not only once. We can use the obtained results to redirect them to another program. For the following example, we will use wc, which should count the total number of obtained results.

![image](https://github.com/user-attachments/assets/72d0bc9c-9187-4949-974d-3834abedaa49)







