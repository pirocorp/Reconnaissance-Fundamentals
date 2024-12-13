# Local System Scanning

System scanning aims to get **Privilege Escalation (Privesc)**, which elevates our permissions. There are many privilege escalation vectors. To understand them, you must know how the corresponding operational system (OS) works.

## Linux Privilege Escalation

[Permission Management](../00.%20Introduction%20and%20Preparation/Linux%20Fundamentals/File%20System.md#permission-management) in Linux treated everything as a file.

![image](https://github.com/user-attachments/assets/b912bd61-662e-4888-9e8d-c581303db172)

The main goal is to find a way to execute commands from or as the root user. If we can execute commands, we can trigger reverse shell or C2 and escalate to the root user. Sometimes, privilege escalation is brutal since we must pivot to different users and then root.

### Tools

#### [Linpeas.sh](https://linpeas.sh/)

LinPEAS is a script that searches for possible paths to escalate privileges on Linux/Unix*/MacOS hosts. The checks are explained [here](https://book.hacktricks.xyz/linux-hardening/linux-privilege-escalation-checklist).

#### [GTFOBins](https://gtfobins.github.io/)

GTFObins is a set of Linux binaries that can be used to escalate privileges. Such binaries are often misconfigured to allow privilege escalation.

## Windows Privilege Escalation

The most privileged user in Windows is "**NT AUTHORITY\SYSTEM**", also known as the system user. This account is more potent than any admin account and runs most System-level (Windows Services) and other third-party services. Admin users can be under the "**Administrators**" or "**Domain Administrators**" groups. 

### Tools

#### [Winpeas](https://github.com/peass-ng/PEASS-ng/tree/master/winPEAS)

WinPEAS, also known as Windows privilege escalation excellent scripts, is an open-source tool created by CarlosPolop. It searches for all possible paths to escalate privileges on Windows hosts and uses a color-coded system that shows which areas require attention. The color-coded output makes it easier for the administrators to detect something.

#### [WinPwn](https://github.com/S3cur3Th1sSh1t/WinPwn)

Internal Windows Penetrationtest automation with Powershell script for recon and exploitation, including proxy support, modules for various attack/analysis function

#### [LOLBAS](https://lolbas-project.github.io/)

LOLBAS stands for Living Off the Land Binaries And Scripts, a type of activity that misuses tools and executables already there because they are part of the operating system.



