# Metasploit

## Introduction to Metasploit

The **Metasploit Project** is a Ruby-based, modular penetration testing platform that enables you to write, test, and execute the exploit code. This exploit code can be custom-made by the user or taken from a database containing the latest discovered and modularized exploits. The **Metasploit Framework** includes a suite of tools that you can use to test security vulnerabilities, enumerate networks, execute attacks, and evade detection. At its core, the **Metasploit Project** is a collection of commonly used tools that provide a complete environment for penetration testing and exploit development.

![image](https://github.com/user-attachments/assets/30b2e107-fe77-4d43-8277-5e04b558864a)

The **modules** mentioned are actual exploit proof-of-concepts that have already been developed and tested in the wild and integrated within the framework to provide pen testers with easy access to different attack vectors for various platforms and services. Metasploit is not a jack of all trades but a Swiss army knife with just enough tools to get us through the most common unpatched vulnerabilities.

Its strength is that it provides a plethora of available targets and versions, all a few commands away from a successful foothold. These, combined with an exploit tailor-made for those vulnerable versions and a payload sent after the exploit, will give us actual access to the system and an easy, automated way to switch between target connections during our post-exploitation ventures.

### Metasploit Pro

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


### Metasploit Framework Console

The `msfconsole` is probably the most popular interface to the **Metasploit Framework (MSF)**. It provides an "all-in-one" centralized console and allows you efficient access to virtually all options available in the MSF. Msfconsole may seem intimidating at first, but once you learn the syntax of the commands, you will learn to appreciate the power of utilizing this interface.

The features that msfconsole generally brings are the following:
- It is the only supported way to access most of the features within **Metasploit**
- Provides a console-based interface to the **Framework**
- Contains the most features and is the most stable **MSF** interface
- Full readline support, tabbing, and command completion
- Execution of external commands in `msfconsole`

Both products mentioned above come with an extensive database of available modules for our assessments. These, combined with the use of external commands such as scanners, social engineering toolkits, and payload generators, can turn our setup into a ready-to-strike machine that will allow us to seamlessly control and manipulate different vulnerabilities in the wild with the use of sessions and jobs in the same way we would see tabs on an Internet browser.

The key term here is usability—user experience. The ease of controlling the console can improve our learning experience. Therefore, let us delve into the specifics.


### Understanding the Architecture

To fully operate any tool, we must first examine its internals. This is good practice and can offer us better insight into what will happen during our security assessments when that tool is used. It is essential not to have [wildcards that might expose you or your client to data breaches](https://blog.cobaltstrike.com/2016/09/28/cobalt-strike-rce-active-exploitation-reported/).

By default, all the base files related to the Metasploit Framework are under `/usr/share/metasploit-framework`.


#### Data, Documentation, Lib

These are the framework's base files. The Data and Lib are the functioning parts of the msfconsole interface, while the Documentation folder contains all the technical details about the project.


#### Modules

The Modules detailed above are split into separate categories in this folder. We will go into detail about these in the following sections. They are contained in the following folders:

![image](https://github.com/user-attachments/assets/b7735cad-77ed-46d2-8b9b-f9fba8cdd38d)


#### Plugins

Plugins offer the pentester more flexibility when using the msfconsole since they can easily be manually or automatically loaded to provide extra functionality and automation during our assessment.

![image](https://github.com/user-attachments/assets/4561999a-8372-448d-922d-e14640fa4f7c)


#### Scripts

Meterpreter functionality and other helpful scripts.

![image](https://github.com/user-attachments/assets/e17cb7c1-13e7-48c0-a443-6fc7512dd7ed)


#### Tools

Command-line utilities that can be called directly from the `msfconsole` menu.

![image](https://github.com/user-attachments/assets/6d675e2a-0b96-440b-99ed-fa8c69942636)


Now that we know all of these locations, it will be easy to reference them when we import new modules or create new ones from scratch.


## Introduction to MSFconsole

To start interacting with the Metasploit Framework, we need to type `msfconsole` in the terminal of our choice. Many security-oriented distributions, such as Parrot Security and Kali Linux, come with `msfconsole` preinstalled. We can launch the script using several other options, as with any other command-line tool. These range from graphical display switches/options to procedural ones.


### Preparation

Upon launching the `msfconsole`, we are met with their coined splash art and the command line prompt, and we are waiting for our first command.


#### Launching MSFconsole

![image](https://github.com/user-attachments/assets/5bec1388-0323-4dd6-92d5-a4cc1c13a3cf)

Alternatively, we can use the `-q` option, which does not display the banner.

![image](https://github.com/user-attachments/assets/16d5b7ab-0f55-47cc-9a8c-f80648df1c9d)

To better look at all the available commands, we can type the `help` command. First things first, our tools need to be sharp. One of the first things we need to do is ensure the modules that compose the framework are up to date and that any new ones available to the public can be imported.

The old way would have been to run `msfupdate` in our OS terminal (outside msfconsole). However, the `apt` package manager can currently handle the update of modules and features effortlessly.


### Installing MSF

```bash
sudo apt update && sudo apt install metasploit-framework
```

![image](https://github.com/user-attachments/assets/31c99b7a-24b8-4936-bb64-982c5b8cda53)

One of the first steps we will cover in this module is searching for a proper **exploit** for our **target**. Nevertheless, we need a detailed perspective on the target before using it. This involves the **Enumeration** process, which precedes any exploitation attempt.

During **Enumeration**, we must examine our target and identify which public-facing services are running on it. For example, is it an HTTP server? Do you know if an FTP server? An SQL Database? These **target** typologies vary substantially in the real world. We must thoroughly **scan** the target's IP address to determine what service is running and what version is installed for each service.

As we go along, we will notice that versions are the key components during the **Enumeration** process that allow us to determine whether the target is vulnerable. Unpatched versions of previously vulnerable services or outdated code in a publicly accessible platform will often be our entry point into the **target** system.


### MSF Engagement Structure

The MSF engagement structure can be divided into five main categories.

- Enumeration
- Preparation
- Exploitation
- Privilege Escalation
- Post-Exploitation

This division makes it easier for us to find and select the appropriate MSF features in a more structured way and to work with them accordingly. Each category has subcategories intended for specific purposes. These include, for example, Service Validation and Vulnerability Research.

We must familiarize ourselves with this structure. Consequently, we will examine its components to understand their relationship better.

![image](https://github.com/user-attachments/assets/570019ee-4621-42a9-995e-f8e3da54e86a)

We will review each category during the module but recommend you look over the individual components and dig deeper. Experimenting with the different functions is integral to learning a new tool or skill. Therefore, we should try everything imaginable in the following labs and analyze the results independently.


## Modules

As mentioned, Metasploit **modules** are prepared scripts with specific purposes and corresponding functions already developed and tested in the wild. The **exploit** category consists of so-called proof-of-concept (**POCs**) that can exploit existing vulnerabilities largely automatedly. Many people often think that the exploit's failure disproves the existence of the suspected vulnerability. However, this is only proof that the Metasploit exploit does not work and that the vulnerability does not exist. This is because many exploits require customization according to the target hosts to make the exploit work. Therefore, automated tools such as the Metasploit framework should only be considered a support tool and not a substitute for our manual skills.

Once in the `msfconsole`, we can select from an extensive list containing all the available Metasploit modules. Each of them is structured into folders, which will look like this:

### Syntax

```bash
<No.> <type>/<os>/<service>/<name>
794   exploit/windows/ftp/scriptftp_list
```

