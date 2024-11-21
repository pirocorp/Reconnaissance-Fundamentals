# Reconnaissance-Fundamentals

## Offensive Operating System

- [Kali Linux](https://www.kali.org/)
- [ParrotOS](https://www.parrotsec.org/)
- [Black Arch Linux](https://blackarch.org/)
- [CommandoVM](https://github.com/mandiant/commando-vm)

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




