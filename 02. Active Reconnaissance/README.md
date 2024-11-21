# Active Reconnaissance

**Active Reconnaissance** involves gathering detailed information about the **target**, including **port**, **service**, **version**, and more. **Active Reconnaissance** is also called **scanning** or **enumeration** since each technique actively generates traffic (in the form of packets), and the results depend on the output. Every scanner sends specifically crafted packets, which can determine the desired results based on their responses. 

**Active Reconnaissance** is usually the next step after passive Reconnaissance. The idea here is to collect **more detailed information about the target**. Using that detailed information is essential for finding vulnerabilities.

## Techniques

### Port Scanning

**Port scanning** is one of the main enumeration techniques used in every engagement. **Port scanning** is usually done with [nmap](https://www.kali.org/tools/nmap/). Port scanning sends packets to different ports and, based on the output, determines if the port is open, closed, or filtrated. While open and closed states are self-explanatory, filtrated means that the port is behind a firewall, and the scanner cannot determine its state.

**Port scanners** like [nmap](https://www.kali.org/tools/nmap/) can send packets on both transport layers (**TCP**, **UDP**) and have extended functionality. With given flags, they can determine the running services on the opened ports. If [nmap](https://www.kali.org/tools/nmap/) fails to enumerate service and version, the port must be manually enumerated with [netcat(nc)](https://www.kali.org/tools/netcat/). 


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

When SSH is enumerated, it is genuinely a skipped service since SSH is designed to be secure by default. You can obtain the service version, and you can guess the OS version from the OS version.

#### Enumerating SMTP

When **SMTP is enumerating**, the target is to obtain the **service version**, **server name**, and **valid commands**.

#### Enumerating HTTP/S

Most often, ports **80** and **443** are opened. These are HTTP/S ports. Web applications can be hosted on them. Web applications are a whole new domain with various specific (for web) vulnerabilities.


## Tools


