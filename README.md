# Reconnaissance-Fundamentals

## Specialized Search Engines

- [CVE](https://www.cve.org/) - The Common Vulnerabilities and Exposures (CVE) program can be thought of as a dictionary of vulnerabilities. It provides a standardized identifier for vulnerabilities and security issues in software and hardware products. Each vulnerability is assigned a CVE ID with a standardized format, like `CVE-2024-29988`. This unique identifier (CVE ID) ensures that everyone from security researchers to vendors and IT professionals is referring to the same vulnerability, `CVE-2024-29988` in this case.
- [Exploit DB](https://www.exploit-db.com/) - The Exploit Database - Exploits, Shellcode, 0days, Remote Exploits, Local Exploits, Web Apps, Vulnerability Reports, Security Articles, Tutorials and more.
- [Shodan](https://www.shodan.io/) - a search engine for devices connected to the Internet. It allows you to search for specific types and versions of servers, networking equipment, industrial control systems, and IoT devices. Consider visiting [Shodan Search Query Examples](https://www.shodan.io/search/examples) for examples.
- [Censys](https://search.censys.io/) - At first glance, Censys appears similar to Shodan. However, Shodan focuses on Internet-connected devices and systems, such as servers, routers, webcams, and IoT devices. Censys, on the other hand, focuses on Internet-connected hosts, websites, certificates, and other Internet assets. Some of its use cases include enumerating domains in use, auditing open ports and services, and discovering rogue assets within a network. You might want to check [Censys Search Use Cases](https://support.censys.io/hc/en-us/articles/20720064229140-Censys-Search-Use-Cases).
- [VirusTotal](https://www.virustotal.com/) - VirusTotal is an online website that provides a virus-scanning service for files using multiple antivirus engines. It allows users to upload files or provide URLs to scan them against numerous antivirus engines and website scanners in a single operation. They can even input file hashes to check the results of previously uploaded files.
- [Have I Been Pwned](https://haveibeenpwned.com/) - Have I Been Pwned (HIBP) does one thing: it tells you if an email address has appeared in a leaked data breach. Finding one’s email within leaked data indicates leaked private information and, more importantly, passwords. Many users use the same password across multiple platforms. If one platform is breached, other platforms' passwords are also exposed. Indeed, passwords are usually stored in encrypted format; however, many passwords are not that complex and can be recovered using a variety of attacks.
- [GitHub](https://github.com/) - GitHub, a web-based platform for software development, can contain many tools related to CVEs, along with proof-of-concept (PoC) and exploit codes.

## Offensive Operating System

- [Kali Linux](https://www.kali.org/)
- [ParrotOS](https://www.parrotsec.org/)
- [Black Arch Linux](https://blackarch.org/)
- [CommandoVM](https://github.com/mandiant/commando-vm)

## Testing Environments

- [Try Hack Me](https://tryhackme.com/)
- [Hack The Box](https://www.hackthebox.com/)
- [Vulnerable Hub](https://www.vulnhub.com/)
- [bWAPP: bee-box](https://www.vulnhub.com/entry/bwapp-bee-box-v16,53/)

## Information Gathering

**Reconnaissance** utilizes **creativity** and **technical** knowledge to **obtain sensitive**, **personal**, or **publicly** available **information** about a targeted asset. It is the first step in actual engagements and operations. **Reconnaissance** is the most essential part of security assessments, known as penetration testing / red teaming operations. A deep understanding of the target leads to finding and exploiting vulnerabilities.

### [Passive](01.%20Passive%20Reconnaissance)

**Passive reconnaissance** obtains information about the target using **OSINT (Open Source INTelligence)**. **OSINT** is a set of techniques and tools for stealthily obtaining information about a target. **Passive reconnaissance** does not generate traffic to the target side. 

- Stalking Social Networks (Performing requests towards their servers)
- Searching for Code Repositories / Pastebins (Performing requests towards their servers)
- Utilizing third-party scanning tools (like [DNSdumbster](https://dnsdumpster.com/))
- Querying Google and other search engines.


### [Active](02.%20Active%20Reconnaissance)

**Active reconnaissance** obtains information about the
target by utilizing aggressive tools like scanners, fuzzers, and more. **Passive reconnaissance** does generate traffic to the target side. 

- Port scan ([nmap](https://www.kali.org/tools/nmap/), [masscan](https://www.kali.org/tools/masscan/))
- Vulnerability scanning ([nessus](https://www.tenable.com/blog/getting-started-with-nessus-on-kali-linux), [burpsuite](https://www.kali.org/tools/burpsuite/))
- Directory brute-forcing ([gobuster](https://www.kali.org/tools/gobuster/), [dirb](https://www.kali.org/tools/dirb/))
- Parameter fuzzing ([wfuzz](https://www.kali.org/tools/wfuzz/), [ffuf](https://www.kali.org/tools/ffuf/))
- Front-end source code review




