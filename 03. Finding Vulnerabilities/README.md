# Finding Vulnerabilities

**Finding Vulnerabilities** is an art. Here, we must combine and weaponize all the detailed information from previous steps. Seek for something unusual that can be abused or something of order. Examples: an **old version**, **missing field sanitization**, **missing HTTPS**, and many others. This can be done by fuzzing (poking the application with specific "malicious" payloads). 

To find a vulnerability, you must be aware of what vulnerability is and what types of vulnerabilities are there. It would help if you knew what you were trying to find. This means you must create and implement a methodology. Every pentester has his unique methods or way of doing things. Example methodology from hack tricks: [Pentesting Web Methodology](https://hacktricks.boitatech.com.br/pentesting/pentesting-web).

Do not look at finding vulnerabilities like a linear process. It is not going through an extensive checklist. Instead, be as creative as possible and perform illogical and logical things. Force the application to behave unexpectedly, research, and find the bug.


## Active Enumeration

Sometimes vulnerabilities can arise just from **service enumeration**. That's why scanning must be complex and detailed, and it can find the low-hanging fruits like:
  - Obsolete versions
  - Hardcoded credentials
  - Default credentials
  - Backup files with credentials
  - Vulnerable plugins and extensions and more


## Fuzzing Services

Vulnerabilities can appear from **every angle**. It is a must to go through every **single opened service**, trying to determine:
  - What is it, and how it behaves?
  - What happens when you supply strange input?
  - Does this input/output pattern match a vulnerability?
    - If so, continue testing deeper
    - If not, continue testing for different vulnerabilities

Example:
You find **ftp service**, try to connect as **anonymous user**, and if it is successful, try to upload files. If it fails, the service is up to date and has no active exploits available nor sensitive information to get, so you move to **port 80**.

You found a blog web application. You input the search, and the application returns 500 (Internal Server Error). You copy the request with burp suite, run it with sqlmap, and dump the entire database. The application returning 500 was unexpected and proved something was going on. That's finding vulnerability (fuzzing the application for **SQL injection**). 

While fuzzing is excellent at finding vulnerabilities on different components, the most dangerous vulnerabilities are **business logic ones**. **Nessus** and **Burp** are great at fuzzing and can fuzz better
than everyone.


## Business Logic Vulnerabilities

Business logic vulnerabilities are more challenging to find and exploit since you must thoroughly understand the target scope. For example, a regular vulnerability is **SQL injection**, and many automatic tools can fuzz it. On the other hand, business logic vulnerability is, for example, user password reset misconfiguration, weak session management, misconfigured active-directory certificate service, or even chaining multiple attack vectors, like uploading to FTP and execution on the web. 


## Automatic Vulnerability Scanning

Just run an active scan of **Nessus** or **Burp**. They will do the heavy lifting for you. **Nessus** is mainly used for infrastructure scope. **Burp** is used for the scope of the web app. Even though **Nessus** can scan web applications, **Burp Pro** is considered the best.


## Active Reconnaissance Tools

### [Searchsploit / Exploitdb](https://www.kali.org/tools/exploitdb/) 

[Exploit Database](https://www.exploit-db.com/) Archive Search.


### [SQLmap](https://www.kali.org/tools/sqlmap/)

**SQLmap** aims to detect and exploit **SQL injection vulnerabilities** in web applications. Once it detects one or more **SQL injections** on the target host, the user can choose among a variety of options to perform an extensive back-end database management system fingerprint, retrieve DBMS session user and database, enumerate users, password hashes, privileges, databases, dump entire or user’s specific DBMS tables/columns, run his own SQL statement, read particular files on the file system and more.


### [BurpSuite](https://www.kali.org/tools/burpsuite/)

Burp Suite is an integrated platform for performing security testing of web applications. Its various tools work seamlessly together to support the entire testing process, from initial mapping and analysis of an application’s attack surface to finding and exploiting security vulnerabilities.


### [Nessus](https://www.tenable.com/blog/getting-started-with-nessus-on-kali-linux)

Nessus is a vulnerability management tool that helps organizations and network environments identify and address security issues. It helps identify vulnerabilities, potential threats, and irregularities.


### Web Browser

This is one of the main tools for discovering web vulnerabilities. It is also helpful for web enumeration and exploitation. Firefox is the preferred browser.


