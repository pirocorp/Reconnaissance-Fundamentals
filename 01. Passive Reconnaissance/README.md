# Passive Reconnaissance

**Passive Reconnaissance** is the art of gathering information about a target without them even realizing it. It is also called **OSINT(Open Source Intelligence)** since it relies on open sources for the whole process. **Open sources** are **not** used in the context of **coding** **but** instead viewed as publicly **accessible resources**, which, by itself, can include code repositories.

**Passive Reconnaissance** is usually the very **first step** of actual engagements and operations. It is used for building up target context (domains, DNS map, live hosts, whois records, publicly available files, code, and more). **Passive Reconnaissance** requires thinking outside the box. It is **incredibly safe** since, if done right, the **target is unaware**.

## Techniques

### Scanning DNS

**Scanning DNS** is one of the first things to do while performing **OSINT**. **DNS enumeration** is essential since it returns valuable information about the target's Live **hosts** and **DNS records**. This usually includes information about the target's **mail servers, custom DNS servers, workstations, and web servers**. Peeking at the **DNS** can obtain information about the **target's infrastructure context**. 

#### DNS Records

- **A** Used for mapping string to IPv4 address
- **AAAA** Used for mapping string to IPv6 address
- **CNAME** Pointer to another domain instead of an IP
- **NS** Specifies authoritative DNS servers, which servers the browser should request
- **MX** Points to the mail servers of a given domain
- **TXT** Allows the owner of the domain to store text. Some C2 frameworks are using that field to exfiltrate commands, evading security controls

### Stalking Social Media

If the project is phishing-related, the best place to start is to stalk the target on social media (Facebook, Instagram, Twitter, Tiktok, etc.)

## Tools

### Discover

[Discover](https://github.com/leebaird/discover) - Custom bash scripts automate penetration testing tasks, including recon, scanning, enumeration, and malicious payload creation using Metasploit. For use with Kali Linux.

### Cross-Linked

[CrossLinked](https://github.com/m8sec/CrossLinked) is a LinkedIn enumeration tool that uses search engine scraping to collect valid employee names from an organization. This technique provides accurate results without using API keys, credentials, or accessing LinkedIn directly!
