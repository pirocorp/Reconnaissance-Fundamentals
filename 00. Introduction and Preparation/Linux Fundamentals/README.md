# Linux Fundamentals

Linux is a family of open-source Unix-like operating systems based on the Linux kernel, first released by Linus Torvalds on September 17, 1991. Linux is typically packaged as a Linux distribution (distro), which includes the kernel and supporting system software and libraries, many of which are provided by the GNU Project.

Linux is available in over 600 distributions (or an operating system based on the Linux kernel and supporting software and libraries). Some of the most popular and well-known being Ubuntu, Debian, Fedora, OpenSUSE, elementary, Manjaro, Gentoo Linux, RedHat, and Linux Mint.

## Basic Commands

| Command 	| Description                                                                                             	| Example                             	|
|---------	|---------------------------------------------------------------------------------------------------------	|-------------------------------------	|
| echo    	| Output any text that we provide                                                                         	| ```echo "Hello World!"```           	|
| whoami  	| Find out what user we're currently logged in as!                                                        	| ```whoami```                        	|
| ls      	| Listing Files in Our Current Directory                                                                  	| ```ls```                            	|
| cd      	| change directory                                                                                        	| ```cd folder1```                    	|
| cat     	| Outputting the Contents of a File                                                                       	| ```cat access.log```                	|
| pwd     	| print working directory                                                                                 	| ```pwd```                           	|
| find    	| Search for file or folder                                                                               	| ```find -name note.txt```           	|
| grep    	| The grep command allows us to search the contents of files for specific values that we are looking for. 	| ```grep "THM*" access.log``` 	|


## Basic Shell Operators

| Operator 	| Description                                                                                                                                      	|
|----------	|--------------------------------------------------------------------------------------------------------------------------------------------------	|
| &        	| This operator allows you to run commands in the background of your terminal.                                                                     	|
| &&       	| This operator allows you to combine multiple commands together in one line of your terminal.                                                     	|
| >        	| This operator is a redirector - meaning that we can take the output from a command (such as using cat to output a file) and direct it elsewhere. 	|
| >>       	| This operator does the same function of the > operator but appends the output rather than replacing (meaning nothing is overwritten).            	|
