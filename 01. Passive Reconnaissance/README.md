# Passive Reconnaissance

**Passive Reconnaissance** is the art of gathering information about a target without them even realizing it. **Passive Reconnaissance** or **OSINT(Open Source Intelligence)** since it relies on open sources for the whole process. **Open sources** are **not** used in the context of **coding** **but** instead viewed as publicly **accessible resources**, which, by itself, can include code repositories.

**Passive Reconnaissance** is usually the very **first step** of actual engagements and operations. **Passive Reconnaissance** is used to build target context (domains, DNS map, live hosts, whois records, publicly available files, code, and more). **Passive Reconnaissance** requires thinking outside the box. **Passive Reconnaissance** is **incredibly safe** since, if done right, the **target is unaware**.

## Techniques

### Scanning DNS

**Scanning DNS** is one of the first things to do while performing **OSINT**. **DNS enumeration** is essential since it returns valuable **information** about the target's **live hosts and DNS records**. **DNS records** usually **include information** about the target's **mail servers, custom DNS servers, workstations, and web servers**. Peeking at the DNS can obtain information about the target's infrastructure context. 

#### DNS Records

- **A** - Used for mapping string to IPv4 address
- **AAAA** - Used for mapping string to IPv6 address
- **CNAME** - Pointer to another domain instead of an IP
- **NS** - Specifies authoritative DNS servers, which servers the browser should request
- **MX** - Points to the mail servers of a given domain
- **TXT** - Allows the domain owner to store text. Some C2 frameworks are using that field to exfiltrate commands, evading security controls

### Stalking Social Media

If the project is phishing-related, the best place to start is to stalk the target on social media (Facebook, Instagram, Twitter, TikTok, etc.). **Social Media Stalking** can also be applied for pen-testing / red teaming if you can extract something valuable from employees' social media. **Social Media Stalking** can lead to more complex attacks or wordlist crafting. Check if the target's profiles are open and if helpful information is inside, and gather everything (favorite places, friends, tags, profile feeds, etc.).

### Enumerating Usernames / Emails

A list of valid (if possible) usernames/email addresses is always a good idea. Such a list can lead to password spraying, phishing, privilege escalation, etc.

### Enumerating Publicly Available Resources

Enumerate publicly available resources like code repositories, files, paste bins, credentials, SSH keys, etc.

## Tools

### Discover

[Discover](https://github.com/leebaird/discover) - Custom bash scripts automate penetration testing tasks, including recon, scanning, enumeration, and malicious payload creation using Metasploit. For use with Kali Linux.

### Maltego

[Maltego](https://www.maltego.com/) is an all-in-one platform for open-source intelligence (OSINT) and cyber investigations.

### OSINT Framework

The **[OSINT Framework](https://osintframework.com/)** provides a structured approach to gathering publicly available information. Its scope has expanded due to the Internet and digital communications, and it offers tools and techniques for open-source data analysis.

**OSINT tools** within the framework enable effective data harvesting from various online sources, including social media and search engines. They also extend to exploring the Deep and Dark Web, offering insights across multiple sectors.

### Search Engines

[Google hacking](https://www.exploit-db.com/google-hacking-database) is a database of Google (usually) queries that allow you to get detailed information about the target.

### Cross-Linked

[CrossLinked](https://github.com/m8sec/CrossLinked) is a LinkedIn enumeration tool that uses search engine scraping to collect valid employee names from an organization. This technique provides accurate results without using API keys, credentials, or accessing LinkedIn directly!

### DNSdumbster

[DNS dumbster](https://dnsdumpster.com/) is a domain research tool for discovering hosts related to a domain. It can find visible hosts from the attacker's perspective for Red and Blue Teams.



