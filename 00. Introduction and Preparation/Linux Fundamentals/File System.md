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

If we now search for all files with the ".conf" extension, you will find that this search produces results much faster than using find. However, this tool does not have as many filter options that we can use. So it is always worth considering whether we can use the locate command instead of the find command. It always depends on what we are looking for.

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



### Filter Contents

In the last section, we learned about the redirections we can use to redirect results from one program to another for processing. To read files, we do not necessarily have to use an editor. Two identical tools are called ```more``` and ```less```. These fundamental **pagers** allow us to scroll through the file in an interactive view. Let us have a look at some examples.


#### More

After we read the content using cat and redirected it to more, the already mentioned pager opens, and we will automatically start at the beginning of the file.

```bash
more /etc/passwd
```

With the [Q] key, we can leave this pager. We will notice that the output remains in the terminal.

![image](https://github.com/user-attachments/assets/e3736512-f2fb-4777-a87f-a03e766ee89b)


#### Less

If we look at the tool ```less```, we will notice on the man page that it contains many more features than ```more```. When closing less with the [**Q**] key, we will notice that unlike ```more```, the output we have seen does not remain in the terminal.


#### Head

Sometimes, we are only interested in specific issues at the beginning or end of the file. If we only want to get the first lines of the file, we can use the tool head. By default, head prints the first ten lines of the given file or input unless otherwise specified.


#### Tail

If we only want to see the last parts of a file or results, we can use the counterpart of ```head``` called ```tail```, which returns the last ten lines.

![image](https://github.com/user-attachments/assets/38004ae7-de42-4080-8e8b-3be3c1f1cc67)


#### Sort

They are rarely sorted depending on which results and files are dealt with. Often, sorting the desired results alphabetically or numerically is necessary to get a better overview. We can use a tool called ```sort``` for this.

![image](https://github.com/user-attachments/assets/7d8fbf02-7bd2-4677-b08a-3fe6604bbb13)


#### Grep

We will more often only search for specific results that contain patterns we have defined. One of the most used tools is ```grep```, which offers many different features. Accordingly, we can search for users with the default shell "/bin/bash" set as an example.

```bash
cat /etc/passwd | grep "/bin/bash"
```

![image](https://github.com/user-attachments/assets/c5a7e21e-befc-4cd3-9ada-46243ad10fbe)

Another possibility is to exclude specific results. For this, the option "-v" is used with grep. In the next example, we exclude all users who have disabled the standard shell with the name "/bin/false" or "/usr/bin/nologin".

```bash
cat /etc/passwd | grep -v "false\|nologin"
```

![image](https://github.com/user-attachments/assets/a74d7318-7175-4d5b-8edc-582fe3414687)


#### Cut

Specific results with different characters may be separated as delimiters. Knowing how to remove particular delimiters and show the words on a line in a specified position is handy. One of the tools that can be used for this is ```cut```. Therefore, we use the option "-d" and set the delimiter to the colon character (:) and define with the option "-f" the position in the line we want to output.


```bash
cat /etc/passwd | grep -v "false\|nologin" | cut -d":" -f1
```

![image](https://github.com/user-attachments/assets/ce332be7-d7a6-4592-8f1f-52f3ced1602b)


#### Tr

The tool ```tr``` is another possibility for replacing certain characters from a line with characters we defined. As the first option, we define which character we want to replace, and as the second option, we define the character we want to replace it with. In the following example, we replace the colon character with space.

```bash
cat /etc/passwd | grep -v "false\|nologin" | tr ":" " "
```

![image](https://github.com/user-attachments/assets/65bc9044-918b-4910-bd21-88a2fba56c7f)


#### Column

Since search results can often be unclear, the tool ```column``` is well suited to display such results in tabular form using the "-t."

```bash
cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | column -t
```

![image](https://github.com/user-attachments/assets/86e0021c-1acc-4d6e-b14a-da7ac00dd43e)


#### Awk

To sort out results as simply as possible, the (g)```awk``` programming is beneficial, as it allows us to display the first ($1) and last ($NF) results of the line.

```bash
cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}'
```

![image](https://github.com/user-attachments/assets/fead709b-df68-46c0-8896-d83b6123c6fb)


#### Sed

There will come moments when we want to change specific names in the whole file or standard input. One of the tools we can use for this is the stream editor called ```sed```. One of the most common uses of this is substituting text. Here, sed looks for patterns we have defined in the form of regular expressions (regex) and replaces them with another pattern that we have also described. Let us stick to the last results and say we want to replace the word "bin" with "HTB."

The "s" flag at the beginning stands for the substitute command. Then, we specify the pattern we want to replace. After the slash (/), we enter the pattern we want to use as a replacement in the third position. Finally, we use the "g" flag to replace all matches.

```bash
cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | sed 's/bin/HTB/g'
```

![image](https://github.com/user-attachments/assets/abe34f9b-21a2-463c-b3e5-110c0e642b7b)


#### Wc

Lastly, knowing how many successful matches we have will often be useful. To avoid counting the lines or characters manually, we can use the tool wc. With the "-l" option, we specify that only the lines are counted.

```bash
cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | wc -l
```

![image](https://github.com/user-attachments/assets/3c559589-68eb-4fdb-acc0-da5b2d2dbe96)



#### Practice

| N  | Task                                                                                                                                                       |
|----|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1. | A line with the username cry0l1t3.                                                                                                                         |
| 2. | The usernames.                                                                                                                                             |
| 3. | The username cry0l1t3 and his UID.                                                                                                                         |
| 4. | The username cry0l1t3 and his UID separated by a comma (,).                                                                                                |
| 5. | A comma separates the username cry0l1t3, his UID, and the set shell (,).                                                                                   |
| 6. | All usernames with their UID and set shells separated by a comma (,).                                                                                      |
| 7. | All usernames with their UID and set shells separated by a comma (,) exclude the ones containing no login or false.                                        |
| 8. | All usernames with their UID and set shells separated by a comma (,) exclude the ones that contain no login and count all lines of the filtered output.    |

![image](https://github.com/user-attachments/assets/df8a3da8-0917-42b2-b309-362a4d806e93)



## Regular Expressions

Regular expressions (RegEx) are an art of expression language used to search for patterns in text and files. They can be used to find and replace text, analyze data, validate input, perform searches, and more. In simple terms, they are a filter criterion that can be used to analyze and manipulate strings. RegEx is available in various programming languages and programs and is used in many different ways and functions.

A regular expression is a sequence of letters and symbols that form a search pattern. In addition, regular expressions can be created with patterns called metacharacters. Meta characters are symbols that define the search pattern but have no literal meaning. We can use regex in tools like grep, sed, and others. Regex is often implemented in web applications for the validation of user input.


### Grouping

Among other things, regex allows us to group the desired search patterns. Regex follows three different concepts, which are distinguished by the three different brackets:

#### Grouping Operators

| Operators | Description                                                                                                                                                                 |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| (a)       | The round brackets are used to group parts of a regex. Within the brackets, you can define further patterns which should be processed together.                             |
| [a-z]     | The square brackets define character classes. Inside the brackets, you can specify a list of characters to search for.                                                      |
| {1,10}    | The curly brackets are used to define quantifiers. Inside the brackets, you can specify a number or a range that indicates how often a previous pattern should be repeated. |
| \|        | Also called the OR operator and shows results when one of the two expressions matches                                                                                       |
| .*        | Also called the AND operator and displayed results only if both expressions match                                                                                           |


##### OR operator

Suppose we use the **OR** operator. The regex searches for one of the given search parameters. In the following example, we search for lines containing the word my or false. You must apply the extended regex using the -E option in grep to use these operators.

```bash
grep -E "(my|false)" /etc/passwd
```
![image](https://github.com/user-attachments/assets/ecb46984-e9d9-454a-9670-24e4fc142018)

Since one of the two search parameters always occurs in the three lines, all three lines are displayed accordingly. However, using the AND operator will get a different result for the same search parameters.


##### AND operator

What we are saying with this command is that we are looking for a line where we want to see both **my** and **false**. A simplified example would also be to use grep twice and look like this:

```bash
grep -E "(my.*false)" /etc/passwd
grep -E "my" /etc/passwd | grep -E "false"
```

![image](https://github.com/user-attachments/assets/05523b83-4585-437e-8037-7f0d5c9048c3)

Here are some optional tasks to practice regex that can help us to handle it better and more efficiently.

| Task                                                                 | Command                                                |
|----------------------------------------------------------------------|--------------------------------------------------------|
| Show all lines that do not contain the # character.                  | ```grep -E -v "#" /etc/ssh/sshd_config \| grep "\S"``` |
| Search for all lines that contain a word that starts with Permit.    | ```grep "^Permit" /etc/ssh/sshd_config             ``` |
| Search for all lines that contain a word ending with Authentication. | ```grep "Authentication$" /etc/ssh/sshd_config     ``` |
| Search for all lines containing the word Key.                        | ```grep "\bKey\b" /etc/ssh/sshd_config             ``` |
| Search for all lines beginning with Password and containing yes.     | ```grep -E "(^Password.*yes)" /etc/ssh/sshd_config ``` |
| Search for all lines that end with yes.                              | ```grep "yes$" /etc/ssh/sshd_config                ``` |



## Permission Management

Under Linux, permissions are assigned to users and groups. Each user can be a member of different groups, and membership in these groups gives the user specific permissions. Each file and directory belongs to a particular user and a specific group. So, the permissions for users and groups that define a file are also defined for the respective owners. When we create new files or directories, they belong to the group we belong to and us.

When a user wants to access the contents of a Linux directory, they must first traverse it, which means navigating to it. This requires the user to have execute permissions on the directory. Without this permission, the user cannot access the directory's contents and will be presented with a “Permission Denied" error message instead.

It is important to note that execute permissions are necessary to traverse a directory, no matter the user's level of access. Also, **execute** permissions on a directory do not allow a user to **execute** or modify any files or contents within the directory, only to traverse and access the directory's content.

To execute files within the directory, a user needs **execute** permissions on the corresponding file. To modify the contents of a directory (create, delete, or rename files and subdirectories), the user needs **write** permissions on the directory.

The whole permission system on Linux systems is based on the octal number system, and basically, there are three different types of permissions a file or directory can be assigned:

- (**r**) - Read
- (**w**) - Write
- (**x**) - Execute

![image](https://github.com/user-attachments/assets/78d2849f-d0b5-4f74-bc0c-a1642348d6bc)


