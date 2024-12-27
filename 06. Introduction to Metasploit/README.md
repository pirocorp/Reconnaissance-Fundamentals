# Introduction to Metasploit

The **Metasploit Project** is a Ruby-based, modular penetration testing platform that enables you to write, test, and execute the exploit code. This exploit code can be custom-made by the user or taken from a database containing the latest discovered and modularized exploits. The **Metasploit Framework** includes a suite of tools that you can use to test security vulnerabilities, enumerate networks, execute attacks, and evade detection. At its core, the **Metasploit Project** is a collection of commonly used tools that provide a complete environment for penetration testing and exploit development.

![image](https://github.com/user-attachments/assets/30b2e107-fe77-4d43-8277-5e04b558864a)

The **modules** mentioned are actual exploit proof-of-concepts that have already been developed and tested in the wild and integrated within the framework to provide pen testers with easy access to different attack vectors for various platforms and services. Metasploit is not a jack of all trades but a Swiss army knife with just enough tools to get us through the most common unpatched vulnerabilities.

Its strength is that it provides a plethora of available targets and versions, all a few commands away from a successful foothold. These, combined with an exploit tailor-made for those vulnerable versions and a payload sent after the exploit, will give us actual access to the system and an easy, automated way to switch between target connections during our post-exploitation ventures.

## Metasploit Pro

**Metasploit** as a product is split into two versions. The **Metasploit Pro** version is different from the **Metasploit Framework** one with some additional features:

- Task Chains
- Social Engineering
- Vulnerability Validations
- GUI
- Quick Start Wizards
- Nexpose Integration

If you're more of a command-line user and prefer the extra features, the Pro version also includes a console similar to `msfconsole`.

To have a general idea of what Metasploit Pro's newest features can achieve, check out the list below:

| Infiltrate               | Collect Data             | Remediate                 |
|--------------------------|--------------------------|---------------------------|
| Manual Exploitation      | Import and Scan Data     | Bruteforce                |
| Anti-virus Evasion       | Discovery Scans          | Task Chains               |
| IPS/IDS Evasion          | Meta-Modules             | Exploitation Workflow     |
| Proxy Pivot              | Nexpose Scan Integration | Session Rerun             |
| Post-Exploitation        |                          | Task Replay               |
| Session Clean-up         |                          | Project Sonar Integration |
| Credentials Reuse        |                          | Session Management        |
| Social Engineering       |                          | Credential Management     |
| Payload Generator        |                          | Team Collaboration        |
| Quick Pen-testing        |                          | Web Interface             |
| VPN Pivoting             |                          | Backup and Restore        |
| Vulnerability Validation |                          | Data Export               |
| Phishing Wizard          |                          | Evidence Collection       |
| Web App Testing          |                          | Reporting                 |
| Persistent Sessions      |                          | Tagging Data              |


## Metasploit Framework Console

The `msfconsole` is probably the most popular interface to the **Metasploit Framework (MSF)**. It provides an "all-in-one" centralized console and allows you efficient access to virtually all options available in the MSF. Msfconsole may seem intimidating at first, but once you learn the syntax of the commands, you will learn to appreciate the power of utilizing this interface.

The features that msfconsole generally brings are the following:
- It is the only supported way to access most of the features within **Metasploit**
- Provides a console-based interface to the **Framework**
- Contains the most features and is the most stable **MSF** interface
- Full readline support, tabbing, and command completion
- Execution of external commands in `msfconsole`

Both products mentioned above come with an extensive database of available modules for our assessments. These, combined with the use of external commands such as scanners, social engineering toolkits, and payload generators, can turn our setup into a ready-to-strike machine that will allow us to seamlessly control and manipulate different vulnerabilities in the wild with the use of sessions and jobs in the same way we would see tabs on an Internet browser.

The key term here is usability—user experience. The ease of controlling the console can improve our learning experience. Therefore, let us delve into the specifics.


## Understanding the Architecture

To fully operate any tool, we must first examine its internals. This is good practice and can offer us better insight into what will happen during our security assessments when that tool is used. It is essential not to have [wildcards that might expose you or your client to data breaches](https://blog.cobaltstrike.com/2016/09/28/cobalt-strike-rce-active-exploitation-reported/).

By default, all the base files related to the Metasploit Framework are under `/usr/share/metasploit-framework`.


### Data, Documentation, Lib

These are the framework's base files. The Data and Lib are the functioning parts of the msfconsole interface, while the Documentation folder contains all the technical details about the project.


### Modules

The Modules detailed above are split into separate categories in this folder. We will go into detail about these in the following sections. They are contained in the following folders:






