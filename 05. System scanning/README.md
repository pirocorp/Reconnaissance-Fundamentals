# Local System Scanning

System scanning aims to get **Privilege Escalation (Privesc)**, which elevates our permissions. There are many privilege escalation vectors. To understand them, you must know how the corresponding operational system (OS) works.

## Local Linux Scanning for Privilege Escalation

[Permission Management](../00.%20Introduction%20and%20Preparation/Linux%20Fundamentals/File%20System.md#permission-management) in Linux treated everything as a file.

![image](https://github.com/user-attachments/assets/b912bd61-662e-4888-9e8d-c581303db172)

The main goal is to find a way to execute commands from or as the root user. If we can execute commands, we can trigger reverse shell or C2 and escalate to the root user. Sometimes, privilege escalation is brutal since we must pivot to different users and then root.

The main thing we must look for when doing **Privilege Escalation (Privesc)** is:

- What can my user do?
  - Can I write to **root directories**?
  - Can I modify **root cronjobs**?
  - Can I overwrite something **executed by root**?
  - Can I edit **services**?
  - Can I execute **commands** as root?
  - Can I repeat the steps for different local users if I cannot attack root directly?
- **Are there any available kernel-level exploits?**

### Tools

#### [Linpeas.sh](https://linpeas.sh/)

LinPEAS is a script that searches for possible paths to escalate privileges on Linux/Unix*/MacOS hosts. The checks are explained [here](https://book.hacktricks.xyz/linux-hardening/linux-privilege-escalation-checklist).


