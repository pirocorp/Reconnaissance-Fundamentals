# Active Reconnaissance

**Active Reconnaissance** involves gathering detailed information about the **target**, including **port**, **service**, **version**, and more. **Active Reconnaissance** is also called **scanning** or **enumeration** since each technique actively generates traffic (in the form of packets), and the results depend on the output. Every scanner sends specifically crafted packets, which can determine the desired results based on their responses. 

**Active Reconnaissance** is usually the next step after passive Reconnaissance. The idea here is to collect **more detailed information about the target**. Using that detailed information is essential for finding vulnerabilities.

## Techniques

### Port Scanning

**Port scanning** is one of the main enumeration techniques used in every engagement. **Port scanning** is usually done with [nmap](https://www.kali.org/tools/nmap/). Port scanning sends packets to different ports and, based on the output, determines if the port is open, closed, or filtrated. While open and closed states are self-explanatory, filtrated means that the port is behind a firewall, and the scanner cannot determine its state.

**Port scanners** like [nmap](https://www.kali.org/tools/nmap/) can send packets on both transport layers (**TCP**, **UDP**) and have extended functionality. They can determine the running services on the opened ports with the flags given. If [nmap](https://www.kali.org/tools/nmap/) fails to enumerate service and version, the port must be manually enumerated with [netcat(nc)](https://www.kali.org/tools/netcat/). 


### Service Enumeration

Open ports mean that services are hosted and listening on those ports. Each service runs its software, which has a version and possible vulnerabilities. Ensuring every service on the targeted host is included, including as many details as possible, is essential. This can be done with [nc]((https://www.kali.org/tools/netcat/)) or specific services (like [BurpSuite](https://www.kali.org/tools/burpsuite/))

The most commonly encountered services are:

- FTP (21)
- HTTP/S (80, 443)
- SSH (22)
- HTTP/S Proxy (8080, 8443)
- SMTP (25)

#### Enumerating FTP

**FTP** is a service for file sharing. Check for the **FTP Version** and **FTP Configuration** (**Is anonymous login allowed**).

If the version is updated and the anonymous login is disabled, keep FTP in your backpack. You can **access FTP with compromised credentials** that are valid for the service.

#### Enumerating SSH

When SSH is enumerated, it is genuinely a skipped service since SSH is designed to be secure by default. You can obtain the service version and guess the OS version from the OS version.

#### Enumerating SMTP

When **SMTP is enumerating**, the target is to obtain the **service version**, **server name**, and **valid commands**.

#### Enumerating HTTP/S

Most often, ports **80** and **443** are opened. These are HTTP/S ports. Web applications are a whole new domain with various specific (for web) vulnerabilities.

#### Directory Listings

**Directory listings** refer to a feature provided by web servers that displays a list of files and subdirectories within a specific directory when no default file (like index.html) is present. While this feature can be helpful to for legitimate administrative purposes, if not adequately secured, it can inadvertently expose the server's file structure to attackers.

## Tools

### Discover

[Discover](https://github.com/leebaird/discover) - Custom bash scripts automate penetration testing tasks, including recon, scanning, enumeration, and malicious payload creation using Metasploit. For use with Kali Linux.

### Maltego

[Maltego](https://www.maltego.com/) is an all-in-one platform for open-source intelligence (OSINT) and cyber investigations.

### Nmap

[Nmap](Nmap.md) is applicable for network exploration or security auditing. It supports ping scanning (determining which hosts are up), many port scanning techniques, version detection (determining service protocols and application versions listening behind ports), and TCP/IP fingerprinting (remote host OS or device identification). Nmap also offers flexible target and port specification, decoy/stealth scanning, sunRPC scanning, and more. Most Unix and Windows platforms are supported in GUI and command line modes. Several popular handheld devices, including the Sharp Zaurus and the iPAQ, are also supported.

### Netcat (NC)

[Netcat(NC)](https://www.kali.org/tools/netcat/) is a simple Unix utility that reads and writes data across network connections using TCP or UDP protocol. It is designed to be a reliable "back-end" tool that other programs and scripts can use directly or quickly. At the same time, it is a feature-rich network debugging and exploration tool since it can create almost any connection you need and has several interesting built-in capabilities.

### Ncat

[Ncat](https://www.kali.org/tools/ncat-w32/) is a feature-packed networking utility that reads and writes data across networks from the command line. It was written for the Nmap Project as a much-improved reimplementation of the venerable Netcat. Ncat uses TCP and UDP for communication and is designed to be a reliable back-end tool that instantly provides network connectivity to other applications and users. It will not only work with IPv4 and IPv6 but provides the user with a virtually limitless number of potential uses.

Among Ncat’s many features are the ability to chain Ncats together, redirect both TCP and UDP ports to other sites, SSL support, and proxy connections via SOCKS4 or HTTP (CONNECT method) proxies (with optional proxy authentication as well). Some general principles apply to most applications, allowing you to instantly add networking support to software that would typically never support it.

### Nikto

[Nikto](https://www.kali.org/tools/nikto/) is a pluggable web server and CGI scanner written in Perl. It uses RFP's LibWhisker to perform fast security or informational checks.

Features:
- Easily updatable CSV format checks database
- Output reports in plain text or HTML
- Available HTTP versions automatic switching
- Generic as well as specific server software checks
- SSL support (through libnet-ssleay-perl)
- Proxy support (with authentication)
- Cookies support


### Nuclei

[Nuclei](https://www.kali.org/tools/nuclei/) sends requests across targets based on a template, leading to zero false positives and providing fast scanning on many hosts. Nuclei offers scanning for various protocols, including TCP, DNS, HTTP, File, etc. With powerful and flexible templating, Nuclei can model all kinds of security checks.

### Gobuster

[Gobuster](https://www.kali.org/tools/gobuster/) is a tool for brute-forcing URIs (directories and files) in websites, DNS subdomains (with wildcard support), Virtual Host names on target web servers, Open Amazon S3 buckets, Open Google Cloud buckets, and TFTP servers.

Examples:

In the command below, ```-u``` states the website we're scanning, and ```-w``` takes a list of words to iterate through to find hidden.

```bash
gobuster -u http://fakebank.com -w wordlist.txt dir
```



### DIRB

[DIRB](https://www.kali.org/tools/dirb/) is a Web Content Scanner that looks for existing (hidden) Web Objects. Launching a dictionary-based attack against a web server and analyzing the responses works.

DIRB comes with a set of preconfigured attack wordlists for easy usage, but you can use your custom wordlist (like [SecLists](https://github.com/danielmiessler/SecLists)). DIRB can sometimes be used as a classic CGI scanner, but remember, it is a content scanner, not a vulnerability scanner.

DIRB primarily aims to help in professional web application auditing, especially security-related testing. It covers some holes that are not covered by classic web vulnerability scanners. DIRB looks for specific web objects that other generic CGI scanners can't look for. It doesn't search for vulnerabilities, nor does it look for web content that can be vulnerable.

### Burp Suite

[Burp Suite](https://www.kali.org/tools/burpsuite/) is an integrated platform for performing security testing of web applications. Its various tools work seamlessly together to support the entire testing process, from initial mapping and analysis of an application’s attack surface to finding and exploiting security vulnerabilities.

Burp gives you complete control, combining advanced manual techniques with state-of-the-art automation to make your work faster, more effective, and more fun.
